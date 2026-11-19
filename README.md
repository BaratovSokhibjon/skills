# skills

Agent skills marketplace. All skills live in `skills/`.

## Skills

| Skill | What it does |
|---|---|
| `create-skill` | Define and create a skill through a guided interview |
| `write-like-sokhibjon` | Draft messages in Sokhibjon's voice |
| `grilling` (`grill-me/`) | Stress-test a plan by grilling the user |
| `stop-slop-writing` | Remove AI writing patterns from prose |
| `wayfinder` | Map big work as decision tickets, resolve one at a time |

## Install

```bash
# Claude Code
claude plugin marketplace add BaratovSokhibjon/skills
claude plugin install sokhibjon-skills@sokhibjon-skills

# Codex
codex plugin marketplace add BaratovSokhibjon/skills

# Any agent, individual skills
npx skills add BaratovSokhibjon/skills -a claude-code
npx skills add BaratovSokhibjon/skills -a codex
```

Use `-g` with the skills CLI for global install.

This marketplace also offers Corey Haines's
[`marketing-skills`](https://github.com/coreyhaines31/marketingskills) from upstream
`main`:

```bash
claude plugin install marketing-skills@sokhibjon-skills
claude plugin marketplace update sokhibjon-skills
codex plugin marketplace upgrade sokhibjon-skills
```

It's optional and not installed with the main bundle.

## Maintain

- Root is one plugin bundling `skills/`. Manifests: `.claude-plugin/`, `.agents/plugins/marketplace.json`, `plugin.json`.
- Keep plugin names and versions in sync. Bump version for releases.
- New skills join the bundle automatically. Add them to the table above.
- Check with `claude plugin validate .` and `npx skills add . --list`.
- Lib app and data live in [`BaratovSokhibjon/lib`](https://github.com/BaratovSokhibjon/lib).
