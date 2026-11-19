---
name: create-skill
description: Help the user define and create a reusable agent skill through a guided, one-question-at-a-time conversation. Use when the user asks to create a skill, turn a workflow into a skill, or needs help deciding what a skill should do. Not for creating agents, configuring plugins, or ordinary task execution.
---

# Create a skill

Help the user turn an idea into a focused, reusable skill. Start with a conversation, not a generated template.

## Interview

Read the current conversation first. Reuse facts the user has already provided rather than asking them to repeat themselves.

Ask **one focused question per turn**, then wait for the answer. Do not present the whole interview or a long questionnaire. Start with the biggest missing piece, usually:

> What task do you want this skill to help you do? A recent example is enough.

Through follow-up questions, establish:

- The task and why the user wants it reusable.
- When the skill should trigger, and when it should not.
- Inputs, available tools or resources, and the expected output.
- The workflow, important constraints, and actions requiring approval.
- A realistic example and what would make its result good or bad.

These are topics to cover, not a script to recite. Skip questions already answered. If the idea is vague, offer two or three concrete options for the current question. If the scope contains unrelated jobs, suggest narrowing it before proceeding. Ask rather than inventing consequential requirements.

Distinguish a skill from always-on instructions: a skill is loaded for a matching task, not guaranteed to apply to every conversation. If the user needs a permanent rule, explain that distinction before continuing.

## Confirm the brief

Once the essentials are clear, give a short summary of the proposed name, purpose, triggers, inputs, output, and boundaries. Ask the user to confirm or correct it. Do not create files until they approve the brief.

Confirm the destination if the repository's conventions or the user's request do not establish it. Inspect an existing skill before modifying it; never overwrite user work without approval.

## Write the skill

Create `<skill-name>/SKILL.md` in the agreed skills directory. Use a unique kebab-case name and this frontmatter:

```yaml
---
name: skill-name
description: Explain what the skill does, when to use it, and important exclusions.
---
```

- Write clear, imperative instructions for another agent, not a transcript of the interview.
- Include the agreed workflow, input handling, output expectations, and approval boundaries.
- Keep it focused and concise. Avoid speculative features, tools, dependencies, or abstractions.
- Add scripts only for necessary deterministic work. Add references or assets only when the skill needs them, and link to files that actually exist inside the skill folder.
- Do not embed credentials, private conversation history, or personal examples without permission. Do not claim unavailable tools or permissions.
- Follow the destination repository's conventions and update its skill catalog when applicable.

## Verify and hand back

Check that frontmatter parses, the name is unique, and referenced resources exist. Use the repository's validation commands if available.

Suggest a small set of realistic trial prompts, including a matching task and a near-miss that should not trigger. Ask whether the user wants to run them before launching evaluations or other agents. Do not report suggested tests as executed tests.

Report the created path and checks actually performed. Ask for feedback before expanding the skill. Do not commit, publish, install globally, or send anything unless authorized.
