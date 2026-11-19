# skills

Personal library of reusable agent skills. All skills live under `skills/`.
Approved = merged to `main`.

## Catalog

| Skill | What it does |
|---|---|
| [`write-like-sokhibjon`](skills/write-like-sokhibjon/) | Draft or revise messages in Sokhibjon's personal writing style |

## Install

### Claude Code marketplace

```bash
claude plugin marketplace add BaratovSokhibjon/skills
claude plugin install sokhibjon-skills@sokhibjon-skills
```

Invoke the writing skill as `/sokhibjon-skills:write-like-sokhibjon`.
Inside a Claude Code session, the equivalent commands start with `/plugin`.

### Codex marketplace

```bash
codex plugin marketplace add BaratovSokhibjon/skills
```

In supported ChatGPT desktop clients, open the Plugins Directory, select
**Sokhibjon Skills**, and install the plugin. Marketplace UI and installation
support vary by client version. This repo is a Git-backed marketplace, not a
listing in the public ChatGPT plugin directory.

### Individual skills across agents

Use the [skills CLI](https://github.com/vercel-labs/skills) to select skills and agents:

```bash
npx skills add BaratovSokhibjon/skills
npx skills add BaratovSokhibjon/skills --list
npx skills add BaratovSokhibjon/skills --skill write-like-sokhibjon -a claude-code
npx skills add BaratovSokhibjon/skills --skill write-like-sokhibjon -a codex
```

Installation is project-local by default. Add `-g` to install across projects.
Avoid installing the same skill through both a plugin and the skills CLI in
the same agent, since it can appear twice.

## Marketplace maintenance

The repository root is one plugin containing the full `skills/` catalog.
Skills remain in one place; the manifests only package them for each host:

- `.claude-plugin/marketplace.json`: Claude Code marketplace catalog.
- `.claude-plugin/plugin.json`: Claude Code plugin manifest.
- `.agents/plugins/marketplace.json`: Codex marketplace catalog.
- `plugin.json`: portable Agent Plugins manifest for Codex and compatible hosts.

Keep plugin names and versions synchronized between both plugin manifests.
Bump the version when releasing skill changes. New skills under `skills/`
join the bundle automatically; update the catalog above too.

Validate locally before publishing:

```bash
claude plugin validate .
npx skills add . --list
```

To test Claude Code without installing into your settings:

```bash
claude --plugin-dir .
```

GitHub installation commands use the pushed repository, not uncommitted local
changes. For local marketplace testing, replace `BaratovSokhibjon/skills` with `.`.

## Adding a skill

1. Create a branch and add `skills/<name>/SKILL.md`, with optional resources alongside it.
2. Include a globally unique `name` and a clear `description` in YAML frontmatter.
3. Update the catalog above and open a PR. Merging is the approval.

## Separate application

The Lib dashboard, bot, resource processing, backlog, and runtime data live in
the private [`BaratovSokhibjon/lib`](https://github.com/BaratovSokhibjon/lib)
repository, not here.
