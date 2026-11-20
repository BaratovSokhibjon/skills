# skills

Agent skills marketplace. All skills live in `skills/`.

## Skills

| Skill | What it does |
|---|---|
| `claude-planner` | Coordinate software work across Claude, Codex, OpenCode, and agent sessions |
| `create-skill` | Define and create a skill through a guided interview |
| `docker-conventions` | Create and review Dockerfiles and Compose using personal conventions |
| `write-like-sokhibjon` | Draft messages in Sokhibjon's voice |
| `grilling` (`grill-me/`) | Stress-test a plan by grilling the user |
| `writing-conventions` | Write concise agent updates, docs, explanations, and reports |
| `wayfinder` | Map big work as decision tickets, resolve one at a time |
| `voxcpm` | Set up the VoxCPM CLI for speech generation, voice design, and cloning |
| `tesseract` | Install, run, and troubleshoot image OCR with the Tesseract CLI |

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

## Maintain

- Root is one plugin bundling `skills/`. Manifests: `.claude-plugin/`, `.agents/plugins/marketplace.json`, `plugin.json`.
- Keep plugin names and versions in sync. Bump version for releases.
- New skills join the bundle automatically. Add them to the table above.
- Check with `claude plugin validate .` and `npx skills add . --list`.
- Lib app and data live in [`BaratovSokhibjon/lib`](https://github.com/BaratovSokhibjon/lib).
