---
name: novel-ai-detox
description: Iteratively rewrite and critique fiction chapters, scenes, or web-novel prose to remove AI-like phrasing while preserving plot facts and event order. Use when a user asks to remove AI feel, make AI-generated fiction sound human, revise chapter prose, or run parallel reader/revision passes with multiple sub-agents.
---

# Novel AI Detox

## Workflow

1. Act as the controller agent, not the primary rewriter.
2. Label paragraphs with stable IDs before critique.
3. Build a brief with plot facts, tone target, and forbidden changes.
4. If sub-agents are available and the chapter is splittable, spawn reader agents in parallel.
5. Give each reader a distinct lens and collect only concrete critique.
6. Spawn worker agents for the flagged paragraphs with disjoint ownership.
7. Merge the worker outputs without expanding beyond the flagged paragraphs.
8. Run another reader pass on the merged text.
9. Repeat until readers can no longer point to a concrete AI-feel issue.
10. Output the final text and a short change log listing only changed paragraphs.

## Non-negotiables

- The first agent using this skill is the controller.
- The controller handles briefing, paragraph numbering, delegation, merge, and final inspection.
- The controller does not directly rewrite body paragraphs when sub-agents are available.
- Preserve plot facts, character actions, and event order.
- Never modify unflagged paragraphs.
- Never rewrite the whole chapter when only a few paragraphs are flagged.
- Treat "still a little AI" as not done.
- Do not assume short sentences fix the problem.
- Watch for polished functional lines that sound like a prompt being fulfilled, not a character speaking.
- Do not over-compress dialogue; when natural, let speech carry warmth, hesitation, small courtesies, or emotional texture.
- Keep each natural paragraph tight; aim for roughly 40 Chinese characters or fewer when possible.
- Do not make every paragraph equally short if the scene needs a breath, but avoid long blocks of exposition.
- Do not make dialogue too short; let people talk with a little more room, especially when the scene is social or confrontational.
- Let the protagonist sound lazy, swaggering, and a little overconfident when the scene calls for it.
- Prefer direct scene detail over explanation, summary, or moralizing.
- Vary sentence length; avoid template symmetry and over-balanced phrasing.
- Let dialogue carry conflict and character voice.
- When a passage sounds too composed or too competent, rewrite it through a visible micro-expression, a pause, or a colloquial line.
- For ending hooks, do not close on authorial explanation or interpretation; end on a live beat such as a reaction, gesture, interruption, object, or unfinished line.

## Parallel agent use

- Use [references/parallel-review.md](references/parallel-review.md) for reader roles, revision roles, and merge rules.
- When sub-agents are available, the controller-reader-worker split is mandatory.
- Spawn 2 reader agents minimum when parallel critique is worthwhile; use 3-4 for long chapters.
- Keep reader lenses separate: voice/dialogue, rhythm/scene flow, AI tells/exposition, continuity/logic.
- Spawn worker agents only when paragraph ownership does not overlap.
- Do not let one worker revise another worker's paragraphs.
- If the text is short or tightly coupled, the controller may use fewer sub-agents, but it still stays in management and final-check roles.
- If sub-agents are unavailable, say so and fall back to single-agent execution as an explicit exception.

## Revision discipline

- Reader agents only critique.
- Worker agents only rewrite their owned paragraphs.
- The controller only merges, checks, and decides the next pass.
- Ask for paragraph-level findings, not whole-chapter opinions.
- Reject vague feedback like "still feels AI" unless it points to exact paragraphs and features.
- Flag competence-on-display lines that feel sturdy, sharp, and calculated but still sound like a prompt response.
- Flag dialogue that is too clipped, too efficient, or too clean; prefer speech with a little human warmth and room to breathe.
- Flag endings that summarize the moment instead of landing in the scene; convert them into a visible hook beat.
- Flag paragraphs that run too long; split them into shorter beats when needed.
- Flag the protagonist if the voice sounds too disciplined, too polite, or too careful.
- Change only what the critique names.
- If a sentence is fine, leave it alone.
- Recheck after every edit pass.
