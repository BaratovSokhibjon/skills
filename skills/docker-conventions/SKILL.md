---
name: docker-conventions
description: Creates and reviews Dockerfiles and Docker Compose setups using the user's container conventions across languages and frameworks. Use when containerizing an app, adding or editing Dockerfiles or compose.yml, or auditing Docker configuration. Do not use for Kubernetes, installing Docker, general application implementation, or configuring log rotation and retention.
---

# Docker conventions

## 1. Inspect and choose the workflow

Inspect the app's runtime, dependency manifests, startup commands, Dockerfiles, Compose files, ignore rules, and existing storage. Do not print secret values or load private environment files into the conversation.

- **New setup:** create the files needed for the actual app using the conventions below.
- **Existing setup:** report violations first, with file paths, impact, and proposed changes. Ask whether to fix them; wait for approval before modifying files. Do not silently rewrite existing layouts or move persisted data.

Ask one focused question at a time when a required decision is unclear. Preserve working application behavior and avoid adding unrelated services or dependencies.

## 2. Consult relevant context

Use [Docker's documentation index](https://docs.docker.com/llms.txt) to locate official guidance relevant to the task. Fetch only the necessary pages, such as the Dockerfile reference, Compose file reference, or bind-mount documentation. Do not download the full corpus by default.

Use [rest-fastapi-orm-template](https://github.com/bybatkhuu/rest-fastapi-orm-template) as inspiration for multi-stage builds, environment-driven configuration, and service-specific bind mounts. Do not copy its Python-specific commands, identifiers, fallback passwords, extra runtime tools, or override-file layout. The reference is context, not a dependency or a substitute for these conventions.

Check image-specific documentation for supported runtime users, UID/GID options, data directories, and logging configuration. If network access is unavailable, state that limitation and avoid inventing image behavior.

## 3. Apply Dockerfile conventions

1. Use multi-stage builds when they remove build tools or dependencies from the runtime image. A simple app can use one stage when additional stages offer no benefit.
2. Choose a base image compatible with the app. Install only required runtime dependencies in the final image and preserve the project's dependency locking approach.
3. Run the application as a non-root user by default. Set ownership for files and writable directories intentionally. Use explicit UID/GID configuration where supported; do not assume arbitrary `UID` or `GID` environment variables change a container's user.
4. For third-party images, respect their documented user and entrypoint behavior. Some initialize as root before dropping privileges; do not force a Compose `user` value that breaks initialization. Explain exceptions instead of claiming every process is non-root.
5. Keep real credentials out of build arguments, environment defaults, image layers, and committed files. Use BuildKit secret mounts if a build genuinely requires a secret.
6. Use startup commands and entrypoints that deliver termination signals to the application. Keep source copying, dependency installation, and build context appropriate to the language rather than assuming FastAPI.
7. Add or update `.dockerignore` to exclude secrets, Git metadata, host storage, and unnecessary generated files without excluding required build inputs.

## 4. Apply Compose, storage, and configuration conventions

1. Use a single `compose.yml`. Do not introduce dev/prod override files. For existing alternative layouts, report the mismatch and ask before migrating them.
2. Use kebab-case service and directory names. Define only services the app needs. Match container paths to each image's documented requirements.
3. Use bind mounts under `./volumes/storage/<service-name>/`, not named volumes by default. Separate data and logs into subdirectories when needed.
4. Create a tracked `volumes/storage/<service-name>/.gitkeep` before Docker can auto-create the host directory as root. Add `.gitkeep` to any otherwise-empty mounted child directories too. Prefer Compose bind syntax with `bind.create_host_path: false` when supported, so missing paths fail rather than becoming root-owned directories.
5. Treat `.gitkeep` only as a way to preserve directories in Git. It does not store ownership or guarantee container write access. Inspect host and container UID/GID compatibility, including rootless or user-namespace mappings where applicable. Ask before changing existing host ownership or permissions. Never use `chmod 777` as a shortcut.
6. Mount `./volumes/storage/<service-name>/logs/` at `/logs`. Configure the service's actual logger to write there where supported; a mount alone does not redirect logs. If an image cannot use `/logs`, report the limitation and ask about an exception. Log rotation and retention are outside this skill's scope.
7. Keep runtime data and log contents out of Git while retaining `.gitkeep` files. Review ignore rules to ensure both requirements hold; do not erase existing contents or tracked files.
8. Use a gitignored `.env` and tracked `.env.example` with documented variable names and safe placeholders. Never commit real credentials or provide fallback passwords. Require mandatory secrets explicitly, for example `${DB_PASSWORD:?Set DB_PASSWORD in .env}`. Do not overwrite an existing `.env`.
9. Preserve the app's dependency readiness requirements. Do not claim `depends_on` alone means a database is ready; use supported health checks or application retry behavior when readiness is required.

## 5. Build and verify

Build and verify approved changes without requiring another approval for routine local checks. This does not authorize production deployment, destructive operations, or changes to unrelated running workloads.

1. Check that Docker, the daemon, and Compose are available. If unavailable, report the blocker rather than installing or reconfiguring Docker automatically.
2. Validate Compose with `docker compose -f compose.yml config --quiet` so expanded secrets are not printed. If required values are missing, ask the user to supply them locally without posting secrets in chat.
3. Build the affected services with `docker compose -f compose.yml build <services>`. Use equivalent `docker build` commands for Dockerfile-only tasks. Diagnose build failures before retrying; do not bypass checks or remove security constraints to make a build pass.
4. Before runtime checks, inspect port conflicts, mounts, and data destinations. Use a distinct local Compose project name and disposable test storage where practical. Do not let verification run migrations against production or existing valuable data. Ask when safe isolation is not possible.
5. Start the required test services and verify startup, documented health or smoke checks, effective application user, mounted-directory write access, and actual log output under the host `logs/` folder. Do not infer success from a successful build alone. Redact any secrets encountered in output.
6. Stop and remove only test containers and networks created by this verification. Do not delete volumes, bind-mounted data, images, or unrelated resources without approval. Never run broad prune commands or `down --volumes` as routine cleanup.

## 6. Report

Summarize changed files, checks actually run, results, and remaining blockers or approved exceptions. Distinguish static validation, image build success, and runtime verification. Do not claim unexecuted checks passed. Do not commit, push, or deploy unless authorized.
