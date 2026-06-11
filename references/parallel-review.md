# Parallel Reader & Revision Protocol

## Role split

- The first agent is the controller.
- The controller assigns work, merges outputs, and runs the final inspection.
- The controller does not directly rewrite body paragraphs when sub-agents are available.
- Reader agents only critique.
- Worker agents only rewrite their owned paragraphs.

## Paragraph setup

- Number paragraphs before critique.
- Use stable IDs like `P1`, `P2`, `P3`.
- Keep the IDs unchanged through the whole loop.

## Reader pass

- The controller prepares the paragraph IDs and the brief before spawning readers.
- Spawn multiple reader agents when the chapter is long enough to benefit from independent critique.
- Use at least 2 reader agents; use 3 to 4 for long or multi-scene chapters.
- Assign each reader one lens:
  - voice and dialogue
  - rhythm and scene flow
  - AI tells and exposition
  - continuity and logic
  - functional competence lines that feel too polished or too "on task"
- Require this output:
  - paragraph ID
  - exact problem
  - why it feels AI-like
  - concrete fix direction
- Ban rewrite output in the reader pass.

## Revision pass

- The controller groups flagged paragraphs into disjoint ownership sets before spawning workers.
- Group flagged paragraphs into disjoint ownership sets.
- Spawn one worker agent per disjoint set.
- Give each worker only its owned paragraphs plus the relevant critique.
- Require each worker to return revised paragraphs only.
- Forbid workers from editing any unowned paragraph.

## Merge and recheck

- The controller merges worker outputs back into the full chapter.
- Merge all worker outputs into the chapter.
- Run a fresh reader pass on the merged text.
- Repeat until no reader can point to a concrete AI-feel issue.
- The controller performs the last full-chapter inspection before final output.

## Common AI-feel checks

- template-like transitions
- over-balanced sentences
- polished competence lines that feel like a prompt is being fulfilled
- repeated explanation of obvious emotion
- summary or moralizing lines
- characters sounding too similar
- too much exposition, too little scene action
- natural paragraphs that are too long or too heavy
- dialogue that is too brief, too neat, or too efficient for the moment
- protagonist dialogue that lacks swagger, laziness, or arrogant ease
- endings that explain the hook instead of landing on a live beat
- repeated "he knew / he understood / it is not X but Y" patterns

## Rewrite moves for functional prose

- Replace a competence statement with a micro-expression: a glance, a half-smile, a twitch at the mouth, a pause, a hand movement.
- Replace a stiff functional line with spoken reaction: shorter, looser, and tied to the scene.
- Keep the factual meaning, but move the delivery from summary language into visible behavior or natural dialogue.
- If a line sounds like the character is proving they are smart, sharp, steady, or calculating, make it feel like a person in the room instead.
- If dialogue feels too concise, expand it with a natural address, a small reaction, a soft hedge, or a bit of human warmth.
- If a paragraph runs too long, break it into shorter scene beats, usually around 40 Chinese characters or fewer per natural paragraph when possible.
- If the protagonist sounds too tidy, add loose confidence, dismissive ease, or a slightly cocky edge without changing plot facts.

## Ending hook rewrite moves

- Do not end with interpretation.
- End with a reaction, a gesture, a cut-off line, a looked-at object, or a small scene shift.
- If the last line says what the moment means, replace it with what the characters do next or what they fail to say.
- Keep the hook immediate and visible; let the reader infer the danger or tension.

## Stop rule

- Stop only when the readers can no longer point to a specific AI-feel problem in any paragraph.
