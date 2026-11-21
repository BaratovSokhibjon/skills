---
name: writing-conventions
description: Writes and edits coding-agent updates, technical documentation, concise tickets, summaries, and general reports using the owner's direct communication preferences. Use when composing progress updates, completion reports, task descriptions, agent briefs, explanations, or docs. Not for imitating the owner's personal voice in outgoing messages, which uses write-like-sokhibjon, or changing application behavior.
---

# Writing conventions

## 1. Match the task and audience

Identify the reader, purpose, and requested format from the conversation. Follow applicable project instructions and explicit user requirements first. Ask one focused question if a consequential detail is missing.

Use these defaults even when the repository's `AGENTS.md` is unavailable:

- Keep chat relaxed, direct, and concise. Prefer short, natural wording over formal polish without losing meaning.
- Use "Bro," "man," or "dude" occasionally in conversation with the owner, not automatically in documents or third-party reports.
- When guiding the owner through actions, give one step and wait for their result. Don't turn a self-contained report or document into an unnecessary back-and-forth.
- Don't guess missing facts. Ask when needed; identify uncertainty when it doesn't block useful writing.
- Match the owner's engagement: terse replies usually mean work thoroughly and minimize interruptions, conversational replies invite concise questions, and long briefs call for execution rather than another interview. Use context, not rigid word counts. Don't request repeated validation or treat brevity as permission for extra scope or risky actions. Keep status concise even when execution effort is high.

For messages the owner will send in their own voice, load `write-like-sokhibjon` instead. These conventions govern assistant communication, not personal impersonation.

## 2. Write for the purpose

- **Agent updates:** state the meaningful discovery, decision, or blocker. Skip narration of routine tool calls.
- **Completion reports:** lead with the outcome. Include relevant changed paths, checks actually run, failures or limitations, and commit/push status when applicable. Don't add a fixed report template to every reply.
- **Docs:** explain purpose, prerequisites, and usable instructions with concrete examples where needed. Keep commands, paths, identifiers, and technical qualifications accurate. Don't cut necessary detail merely to be brief.
- **General reports:** lead with the conclusion, then evidence, trade-offs, and needed decisions. Attribute external claims and distinguish facts from assumptions.
- **Tickets and tasks:** keep the description human-readable and concise: what, why, essential acceptance criteria, and a link to `agent-brief.md`. Put detailed execution context in that task's brief, not a wall of text in the ticket. The ticket must remain understandable without opening the brief.

For agent-backed tasks, keep a task-specific `agent-brief.md` with context, scope, relevant code and decisions, constraints, dependencies, verification, and handoff details as needed. Use the project's existing storage convention, give each task a distinct location, and link the brief back to its ticket. Keep human-visible scope and acceptance criteria aligned with the brief; don't hide consequential decisions or duplicate long explanations. Verify the receiving agent can access the linked file. Don't publish or attach private context without authorization.

Prefer plain words, specific statements, and useful headings or lists. Remove filler and repetition; avoid em dashes. Preserve meaning, uncertainty, and safety caveats. Don't mechanically ban passive voice, adverbs, or three-item lists when they improve clarity.

## 3. Review once

Check facts, names, links, commands, and scope. Never invent verification, citations, commits, or completion. Match detail and formality to the reader; remove anything that doesn't help them understand or act.

Only when repetitive or formulaic phrasing needs attention, consult [phrases](references/phrases.md), [structures](references/structures.md), or [examples](references/examples.md). These retained editing references are optional suggestions, not blanket word bans or a scoring requirement; this skill's rules take precedence.

Deliver the requested writing without a style score or commentary about making it sound human. Drafting does not authorize sending, publishing, committing, or pushing.

## License

MIT
