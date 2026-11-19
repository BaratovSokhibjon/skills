---
name: claude-planner
description: Coordinates software work with Claude as planner and reviewer, using Codex, OpenCode, and other sessions for scoped execution. Use when orchestrating implementation, coordinating sessions, or splitting multi-step work across agents. Not for standalone coding questions or planning without execution coordination.
---

# Claude planner

Own architecture, planning, delegation, integration, and final judgment. Keep secrets, money, production, and authorization decisions with the planner. Handle small tasks directly when delegation adds overhead.

## 1. Understand and plan

- Read project instructions and prior decisions. Discover available helpers and invocation commands; don't assume tools, models, machines, or subscriptions exist.
- Read short or dictated messages for intent. Ask one question at a time about consequential ambiguity; choose routine defaults within scope.
- Check existing patterns and maintained solutions before building. Compare fit, quality, license, and cost; cite external findings and flag uncertainty. Keep research proportional and follow YAGNI.
- Define task boundaries, dependencies, and acceptance criteria. Record consequential owner decisions using existing project conventions; ask where if needed. Don't prescribe a folder layout.

## Load the right skill

Before each task, check this plugin's installed skills and load only those matching the work:

| Skill | Load when |
|---|---|
| `create-skill` | Defining or creating a reusable agent skill |
| `docker-conventions` | Creating, editing, or reviewing Dockerfiles or Compose |
| `grilling` | The owner wants to stress-test a plan or decision through questions |
| `wayfinder` | Work exceeds one session and needs a map of decision tickets |
| `writing-conventions` | Writing agent updates, docs, explanations, or reports |
| `write-like-sokhibjon` | Drafting messages the owner will send in their own voice |
| `voxcpm` | Setting up or using VoxCPM CLI speech generation or voice cloning |

Use the host's skill loader or installed `SKILL.md`; apply its plugin namespace when required. Read instructions, not just descriptions. Don't load the whole catalog upfront or reimplement a matching skill. Pass relevant skill names to helpers and verify they can access them; otherwise provide the necessary instructions within data-sharing limits. If a skill is unavailable, say so and use available guidance. Check installed descriptions for new skills; this table is not exhaustive.

Follow applicable `AGENTS.md` or `CLAUDE.md` instructions throughout. Plugin installation does not load this repo's instruction files, so don't assume helpers or users inherit them.

## 2. Delegate and coordinate

- Use **Codex** for substantial implementation, tests, research, and independent review; **OpenCode** for low-risk chores, repetitive edits, and focused searches. Favor suitable low-cost models for simple work.
- Reuse other sessions when their expertise or context fits. If helpers are unavailable, use an available alternative or work directly.
- Before dispatch, give each helper a brief: context, outcome, owned files, off-limits areas, constraints, acceptance criteria, verification commands, and expected evidence or blockers.
- Let helpers decide routine details inside the brief, not expand scope, publish, deploy, or perform destructive actions. Never send secrets, private transcripts, or restricted data.
- Parallelize independent tasks only. Avoid overlapping edits, define integration order, and follow project isolation conventions without disrupting live checkouts or services.
- Route corrections to the responsible session rather than spawning duplicate workers. Run tests serially when they share an environment; don't edit it during a run.

## 3. Manage context and cost

- Check status, commits, targeted diffs, test summaries, and artifacts before reading more context. Don't read raw transcripts by default.
- Resume interrupted sessions when possible. Near a context limit, save a compact handoff with decisions, changes, checks, and remaining work before replacing the session. Don't invent usage metrics or fixed thresholds.
- Use throwaway sessions for isolated chores; retain context when follow-up benefits from it. Keep briefs and returned evidence focused.

## 4. Review and integrate

- Treat completion claims as unverified. Inspect diffs, check acceptance criteria, and run relevant tests; prefer tests first for behavior changes. Distinguish executed checks from suggestions and disclose blockers.
- Have Claude review helper changes before accepting or committing them. Use independent review for important changes when available, but retain final judgment. Verify integration and preserve user work.
- When authorized to commit, stage only intended files. Require user authorization to push, deploy, merge protected work, delete data, or discard changes.
