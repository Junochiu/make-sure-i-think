# make-sure-i-think

A Claude skill that gets you thinking for yourself instead of passively taking answers — for any subject, not just coding.

Claude is so fluent that you never have to *generate* anything yourself, and generation is where
learning happens. You end up with correct answers and a hollow mental model: you read the
explanation, but you can't reconstruct it, apply it, or see how it connects to anything else. This
skill reintroduces a small amount of *productive friction* at the moments that matter: before
handing over the full answer or moving on, it surfaces the concept underneath and asks you to
reason about it first — then continues, with your mental model instead of around it.

It works whether you're working through a concept, asking for an explanation, studying a subject, or
writing code, and it behaves the same everywhere Claude runs — the app, Claude Code, and the API.
Grounded in learning science: active recall, the generation effect, predict-then-verify,
elaboration, and desirable difficulty.

## What it does

- Detects when a turn touches a *learnable concept* — and stays quiet when it doesn't (definitions,
  lookups, when you just need the answer to move on).
- Poses **one** short, generative check *before* giving you the full answer.
- Validates your answer, corrects misconceptions warmly, then continues with the concept anchored.
- **Concept maps:** consolidates a topic by mapping the core ideas and the *relationships* between
  them as directed "A → relationship → B" links — ideally written by you and checked by Claude,
  reversed arrows included.
- Eases off automatically if you keep skipping. It's a tutor, not a nag.

## Configuration

On first use it runs a 20-second setup and remembers your answers:

| Setting | Values | Default |
|---|---|---|
| gate strength | `soft` (asks, never blocks) / `firm` (waits for your guess) | `soft` |
| question format | `predict` / `explain` / `tradeoff` / `adaptive` | `adaptive` |

Say **"reconfigure make sure I think"** anytime to change them.

## Install

**Claude.ai / Claude Desktop:** enable *Code execution and file creation* in Settings → Capabilities,
then go to Customize → Skills, add the packaged `make-sure-i-think.skill` (or this folder zipped
with the folder as the zip root), and toggle it on.

**Claude Code:** clone into your skills directory:

```bash
git clone https://github.com/<you>/make-sure-i-think.git ~/.claude/skills/make-sure-i-think
```

## Use

Turn it on with any learning-intent phrase — "help me understand X," "teach me as we go," "make
sure I learn" — and it stays active for the session.

## Repo layout

```
make-sure-i-think/
├── SKILL.md                     # triggering + the core loop + concept maps
├── references/
│   └── configuration.md         # first-run setup + how config is stored
├── README.md
└── LICENSE
```

## Contributing

Issues and PRs welcome. Good contributions: better checks for a subject area, refinements to the
"when NOT to check" heuristics, and concept-map patterns. Keep `SKILL.md` under ~500 lines and push
detail into `references/`.

## License

MIT — see [LICENSE](LICENSE).
