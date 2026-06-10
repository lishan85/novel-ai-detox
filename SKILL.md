---
name: novel-ai-detox
description: Iteratively rewrite and critique fiction chapters, scenes, or web-novel prose to remove AI-like phrasing while preserving plot facts and event order. Use when a user asks to remove AI feel, make AI-generated fiction sound human, revise chapter prose, or run parallel reader/revision passes with multiple sub-agents.
---

# Novel AI Detox

## Workflow

1. Label paragraphs with stable IDs before critique.
2. Build a brief with plot facts, tone target, and forbidden changes.
3. If the chapter is long enough or has multiple scenes, spawn reader agents in parallel.
4. Give each reader a distinct lens and collect only concrete critique.
5. Revise only the paragraphs named by the current critique.
6. If the flagged paragraphs do not overlap, spawn worker agents in parallel with disjoint ownership.
7. Merge the revisions, then run another reader pass.
8. Repeat until readers can no longer point to a concrete AI-feel issue.
9. Output the final text and a short change log listing only changed paragraphs.

## Non-negotiables

- Preserve plot facts, character actions, and event order.
- Never modify unflagged paragraphs.
- Never rewrite the whole chapter when only a few paragraphs are flagged.
- Treat "still a little AI" as not done.
- Do not assume short sentences fix the problem.
- Watch for polished functional lines that sound like a prompt being fulfilled, not a character speaking.
- Do not over-compress dialogue; when natural, let speech carry warmth, hesitation, small courtesies, or emotional texture.
- Prefer direct scene detail over explanation, summary, or moralizing.
- Vary sentence length; avoid template symmetry and over-balanced phrasing.
- Let dialogue carry conflict and character voice.
- When a passage sounds too composed or too competent, rewrite it through a visible micro-expression, a pause, or a colloquial line.
- For ending hooks, do not close on authorial explanation or interpretation; end on a live beat such as a reaction, gesture, interruption, object, or unfinished line.

## Parallel agent use

- Use [references/parallel-review.md](references/parallel-review.md) for reader roles, revision roles, and merge rules.
- Spawn 2 reader agents minimum when parallel critique is worthwhile; use 3-4 for long chapters.
- Keep reader lenses separate: voice/dialogue, rhythm/scene flow, AI tells/exposition, continuity/logic.
- Spawn worker agents only when paragraph ownership does not overlap.
- Do not let one worker revise another worker's paragraphs.
- If the text is short or tightly coupled, keep work local and use one reader and one worker instead.

## Revision discipline

- Ask for paragraph-level findings, not whole-chapter opinions.
- Reject vague feedback like "still feels AI" unless it points to exact paragraphs and features.
- Flag competence-on-display lines that feel sturdy, sharp, and calculated but still sound like a prompt response.
- Flag dialogue that is too clipped, too efficient, or too clean; prefer speech with a little human warmth and room to breathe.
- Flag endings that summarize the moment instead of landing in the scene; convert them into a visible hook beat.
- Change only what the critique names.
- If a sentence is fine, leave it alone.
- Recheck after every edit pass.
