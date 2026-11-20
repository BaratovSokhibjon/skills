---
name: create-skill
description: Defines and creates reusable agent skills through a guided, one-question-at-a-time interview. Use when the user asks to create an agent skill, turn a workflow into a skill, or clarify what a proposed skill should do. Do not use for ordinary task execution, creating agents, configuring plugins, or setting always-on preferences.
---

# Create a skill

Help the user turn an idea into a focused, reusable skill. Start with a conversation, not a generated template.

## 1. Interview

Read the current conversation first. Reuse facts the user has already provided rather than asking them to repeat themselves.

Match engagement: very short replies usually mean carry more of the work, not seek more confirmations; conversational replies suit concise collaboration; long multi-sentence briefs call for thorough execution using the supplied requirements. Treat these as contextual signals, not rigid counts. Investigate and choose reversible defaults within scope; ask only for consequential missing decisions or required authorization. Never infer permission for destructive actions or publishing from message length.

When an interview is needed, ask **one focused question per turn**, then wait. Skip it when the brief already supplies the essentials. Do not present the whole interview or a long questionnaire. Start with the biggest missing piece, usually:

> What task do you want this skill to help you do? A recent example is enough.

Through follow-up questions, establish:

- The task and why the user wants it reusable.
- When the skill should trigger, and when it should not.
- Inputs, available tools or resources, and the expected output.
- The workflow, important constraints, and actions requiring approval.
- A realistic example and what would make its result good or bad.
- Likely failure cases, missing inputs, and what to do when required tools are unavailable.

These are topics to cover, not a script to recite. Skip questions already answered. When offering choices, use a short numbered list so the user can reply with just a number. Put a recommended option first when appropriate and label it; accept a custom answer too. If the idea is vague, offer two or three concrete options for the current question. If the scope contains unrelated jobs, suggest narrowing it before proceeding. Ask rather than inventing consequential requirements.

Distinguish a skill from always-on instructions: a skill is loaded for a matching task, not guaranteed to apply to every conversation. If the user needs a permanent rule, explain that distinction before continuing.

## 2. Confirm the brief

Once the essentials are clear, summarize the proposed name, purpose, triggers, inputs, output, and boundaries. If the user already authorized creation with those requirements, proceed without another confirmation. Otherwise ask for confirmation once. Don't reopen approved choices; use reversible defaults for minor details.

Confirm the destination if the repository's conventions or the user's request do not establish it. Inspect an existing skill before modifying it; never overwrite user work without approval.

## 3. Write the skill

Create `<skill-name>/SKILL.md` in the agreed skills directory. Use a unique kebab-case name: 1-64 lowercase letters, digits, and hyphens, with no leading, trailing, or consecutive hyphens. Match the frontmatter name to the parent directory exactly. Use this frontmatter:

```yaml
---
name: skill-name
description: Describes the capability, specific triggering tasks, and important exclusions.
---
```

- Write the description in third person, under 1,024 characters, with concrete triggers and nearby tasks to exclude.
- Write numbered, chronological steps using direct commands. State decision branches and stop conditions explicitly; do not require the agent to invent missing steps.
- Include the agreed workflow, input handling, output expectations, and approval boundaries.
- Keep `SKILL.md` under 500 lines. Remove generic advice the agent already follows reliably. Avoid speculative features, tools, dependencies, or abstractions.
- Move bulky domain details into `references/` and reusable output templates into `assets/`. Keep supporting files one level below those directories, link directly from `SKILL.md` using relative paths with forward slashes, and say exactly when to read each file. Do not load every resource upfront.
- Add tiny, single-purpose scripts only for fragile or repetitive deterministic operations. State prerequisites, invocation, expected output, and recovery from failure. Use descriptive errors and exit codes; keep reusable library code outside the skill.
- Create only resources the workflow actually needs. Do not add per-skill README, changelog, or installation-guide files. A repository-level catalog is separate.
- Do not embed credentials, private conversation history, or personal examples without permission. Do not claim unavailable tools or permissions.
- Follow the destination repository's conventions and update its skill catalog when applicable.

## 4. Verify

Check that frontmatter parses, name and directory match, names are unique in the destination catalog, length limits are met, and referenced resources exist. Use the repository's validation commands if available. Do not silently rename existing skills to satisfy a check.

Review the workflow for missing inputs, unavailable tools, ambiguous branches, and unsafe side effects. Report blockers with concise reasons, not hidden reasoning traces. Return to the interview with one question if a consequential choice is still unresolved.

Propose three matching prompts and three plausible near-misses to check routing from the description alone. Include an ordinary task and a failure case for workflow testing, with observable success criteria. Ask whether the user wants to run these tests before launching evaluations or other agents. Do not report suggested tests or a manual review as executed behavioral tests.

If tests are approved, compare behavior with and without the skill using the same inputs, check the agreed criteria, and report failures. Revise based on evidence rather than adding rules for every hypothetical edge case.

## 5. Hand back

Report the created path and checks actually performed. Ask for feedback before expanding the skill. Do not commit, publish, install globally, or send anything unless authorized.

## Source

Adapted from [Skills best practices](https://github.com/mgechev/skills-best-practices). This link is attribution, not a runtime dependency.
