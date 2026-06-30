# LinusGPT

An affectionate, clearly-labeled **parody / homage to the whole Linus Torvalds** — paste your own code and get it roasted in his LKML voice, or talk to him about taste, philosophy, and craft. Intended to be **donated to the Linux Foundation**.

> Parody / satire. Not Linus Torvalds. Not the Linux Foundation. Not affiliated with or endorsed by either. It only ever roasts code *you* submit.

**Start here → [`TASKS.md`](TASKS.md)** — current state, what's done, what's next.

## What's in the box
- **The voice** — [`docs/linusgpt-system-prompt-v5.md`](docs/linusgpt-system-prompt-v5.md): a mode-conditioned persona (roast · "would Linus merge this?" · ask-anything · explain), adversarially validated → [`docs/voice-v5.md`](docs/voice-v5.md).
- **The persona** — [`docs/persona-bible.md`](docs/persona-bible.md) + a cited corpus ([`docs/linus-corpus.md`](docs/linus-corpus.md)): the whole man across seven registers (brutal review, teaching, philosophy, humor, self-deprecation, warmth, the 2018 arc).
- **The stance** — [`docs/POSTURE.md`](docs/POSTURE.md): parody/legal posture + guardrails **G1–G12**.
- **The product** — [`docs/signature-interaction.md`](docs/signature-interaction.md) (the roast wedge), [`docs/experience-spec.md`](docs/experience-spec.md) (the four modes), [`docs/api-spec.md`](docs/api-spec.md) (the engine).
- **Try it now** — the [`/linusmode`](.claude/skills/linusmode/) Claude Code skill (pure prompt, no backend).

## Install & use

The working surface today is the **`/linusmode` Claude Code skill** — pure prompt, **no server, no API key, no build step.**

**Prerequisite:** [Claude Code](https://claude.com/claude-code) installed.

### Option A — try it inside this repo
```bash
git clone https://github.com/baron-3dl/linusgpt.git
cd linusgpt
claude            # open Claude Code here; the project skill auto-loads
```
Then type `/linusmode`. (If it doesn't show up, open `/hooks` once or restart Claude Code to reload skills.)

### Option B — install it globally (use `/linusmode` in any project)
```bash
git clone https://github.com/baron-3dl/linusgpt.git
mkdir -p ~/.claude/skills
cp -r linusgpt/.claude/skills/linusmode ~/.claude/skills/
# …or symlink instead, to track updates:
# ln -s "$(pwd)/linusgpt/.claude/skills/linusmode" ~/.claude/skills/linusmode
```
Restart Claude Code (or open `/hooks`) so the skill registers; then `/linusmode` works anywhere.

### Use
- `/linusmode` — flip into Linus mode: paste code to get it roasted/reviewed, or ask him anything. Say **`exit`** to leave.
- `/linusmode --sfw` — same bite, censored profanity.

## Status
The **voice** and the **`/linusmode` skill** work today. The **API**, **web**, and **chatbot** surfaces are designed and mapped but not yet built. Open decisions and the build order are in [`TASKS.md`](TASKS.md).
