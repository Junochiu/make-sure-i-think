# Configuration and first-run setup

Read this when the skill activates and no stored config is found, or when the user says
"reconfigure make sure I think."

## The two settings

**gate strength** — how hard the check gates the conversation.
- `soft` (default): pose the check, but if the user bypasses it, continue anyway and fold a
  one-line explanation into the answer. Lowest friction.
- `firm`: wait for the user to attempt an answer before continuing. Higher friction, more learning.
  Never punitive — once they attempt (even "I don't know"), always teach and continue.

**question format** — the default style of comprehension check.
- `predict`: "what do you think happens if…". Builds intuition about behavior.
- `explain`: "say the idea back in your own words" (Feynman style). Cements a concept they think
  they already get.
- `tradeoff`: "why this and not the alternative?". Builds judgment.
- `adaptive` (default): choose whichever fits the concept in front of you.

## Running first-run setup

Ask the user these two questions once, conversationally — a 20-second setup, not a form. Use a
tappable-choice UI if one is available; otherwise ask in prose.

1. **Gate strength:** "How hard should I hold the line? *soft* — I ask, but never block you. *firm*
   — I wait for your best guess before I continue."
2. **Question format:** "What kind of check helps most? *predict* (guess the outcome), *explain*
   (say it back in your words), *tradeoff* (why this over that), or *adaptive* (I pick)."

Confirm the choices in one line, then persist them. If the user declines, use `soft` + `adaptive`
and move on.

## Persisting the config

Store the choices so you don't ask again, using whatever durable store the environment offers:

- **Claude Code / a project directory:** write a small block to `CLAUDE.md`/`AGENTS.md` at the repo
  root, or a `.make-sure-i-think.json` file. Do **not** write inside the installed skill directory.

  ```
  <!-- make-sure-i-think config -->
  gate_strength: firm
  question_format: predict
  ```

- **Claude.ai / assistant with memory:** record it in memory, e.g. "For make-sure-i-think, the user
  prefers a firm gate and predict-style checks."
- **No durable store:** use the values for the session and note once they won't persist.

## Loading and reconfiguring

Before the first check in a session, look for stored config in those locations and honor it
silently. If none is found, run setup. If the user says "reconfigure make sure I think," re-run the
two questions and overwrite the stored config.
