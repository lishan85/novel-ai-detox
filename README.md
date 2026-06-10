# Novel AI Detox

A Codex skill for iterative fiction critique and revision that removes AI-like prose while preserving plot facts.

It is designed for web-novel chapters and scene-level rewrites where the goal is not just shorter sentences, but more human-feeling prose: warmer dialogue, less polished functional phrasing, visible micro-expressions, and ending hooks that land inside the scene instead of explaining the scene.

## Install

Clone or download this repository into your Codex skills directory:

```powershell
git clone https://github.com/lishan85/novel-ai-detox.git $env:USERPROFILE\.codex\skills\novel-ai-detox
```

Then start a new Codex session and invoke:

```text
Use $novel-ai-detox to revise this chapter.
```

## What It Enforces

- Preserve plot facts, character actions, and event order.
- Revise only the paragraphs flagged by reader critique.
- Continue critique and revision until no concrete AI-feel issue remains.
- Use parallel reader and revision agents when the text can be split safely.
- Avoid over-polished "competence display" prose.
- Add human warmth to dialogue when it is too clipped.
- End hooks on visible scene beats instead of authorial explanation.
