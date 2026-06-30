# LinusGPT — Work Tracker

**Source of truth for project work** (we moved off `rd`). Active multi-step execution mirrors into Claude Code's in-session todo panel. Update checkboxes as work lands.

## Goal
Ship **LinusGPT** — an affectionate parody/homage to **the whole Linus Torvalds** (brilliant, blunt, funny, principled, evolved — not just the angry-rant caricature). Paste your *own* code, get roasted; richer surfaces converse as him. Built cleanly transferable, to be **donated to the Linux Foundation**.

## Done
- [x] Signature interaction — *Paste-Code Roast* (you roast your own code). → `docs/signature-interaction.md`
- [x] Parody / legal posture — defensible parody, provoke freely; homage + self-deprecation. → `docs/POSTURE.md`
- [x] Profanity — full non-slur profanity.
- [x] Persona foundation — curated multi-register **cited corpus** (36 excerpts) + **persona bible** (the whole Linus). → `docs/linus-corpus.md`, `docs/persona-bible.md`
- [x] **Voice v4 — canonical, whole-Linus, multi-register** — system prompt from the bible + corpus few-shot; showcase confirms all registers (roast · measured verdict · philosophy · humor). → `docs/linusgpt-system-prompt-v4.md`, `docs/voice-v4.md`
  - Blind test v1→v4 (88/100 → 100/100): prompt engineering can't fool an adversarial Opus discriminator on cadence — 4 rounds, every lever, **exhausted**. For a clearly-labeled parody that's a fidelity *ceiling*, not a ship gate. v4 is the cleanest prompt; the **human panel** is the real reader; **fine-tune** is held behind it.
  - Earlier roaster-only iterations → `docs/voice-rubric.md`, `docs/voice-eval-set.md`, `docs/voice-blind-test*.md`, `docs/linusgpt-system-prompt-v1/2/3.md`.

## Active — the full Linus experience (built on voice v4)
Decided: LinusGPT is the **full experience** — roast (the signature wedge) **+** converse across registers (ask-Linus-anything, "would Linus merge this?"). Not a reversal of the roast decision; the roast stays the front door.
- [x] **Full-experience spec + conversational guardrails** — 4 modes (roast · merge-verdict · ask-anything · explain), **G5–G12**, subject-gated brutality, and the **share-card gate** (only subject-locked modes get the viral card). → `docs/experience-spec.md` *(draft, review the G5–G12 guardrails)*
- [x] **Voice v5 — mode-conditioned + conversational guardrails** — one router-driven prompt (4 modes), G1–G12, 8 fixed deflections, corpus-not-memory, subject-gated brutality. Adversarially validated (13-probe battery + 3 fix passes); all safety guardrails hold, all routing edges closed. **Canonical voice.** → `docs/linusgpt-system-prompt-v5.md`, `docs/voice-v5.md`
  - Residual routing-*composition* edge cases delegated to the engine input-gate/router (per experience-spec §3), not the prompt.
- [x] **`/linusmode` Claude skill (MVP)** — persistent **Linus-mode toggle** (ala caveman mode) on the **v5** voice: paste code → roast/merge, ask anything → modes 3/4, stays in character till "exit". Pure prompt, no backend. Also the **human-panel vehicle**. Roast verified on v4; *try `/linusmode` after a skill reload to exercise the toggle live.* → `.claude/skills/linusmode/`
- [x] **Linus API — mapped** *(name TBD, not "roast-engine")* — the persona core behind web + chatbot: router → input gate → v5 → output moderation → card (modes 1/2 only). `POST /v1/linus`. → `docs/api-spec.md`
- [ ] **Build the Linus API** — core `POST /v1/linus` (text) → card render → auth/rate-limit. Owns the routing-composition long tail.
- [ ] **Web surface** — paste code at a URL → shareable "Definitely Not Linus" card. *Depends on engine.*
- [ ] **Chatbot surface** — Discord; the full-experience home: roast + *converse* across registers (ask Linus anything). *Depends on engine + experience spec.*

## Voice — remaining open question
- [ ] **Human voice panel** — real kernel/LKML readers judge v4 under natural conditions. The certifying gate (skill is the vehicle).
- [ ] **Fine-tune (armed, not decided)** — corpus is the training set. Trigger: human panel reliably distinguishes AND it measurably costs enjoyment/willingness-to-pay. Else don't spend.

## Backlog
- [ ] **Donation path to the LF** — permissive license, IP assignment, approach, marks (LF can use Linux®/Tux once it's theirs), clean corpus provenance.
- [ ] **POSTURE** — add a short *Endgame: LF donation* note.

## Killed
- ~~Launch agreement / term sheet with Gene Kim~~ — no Gene partnership; pointless for this product.

## Guardrails (always-on, from POSTURE.md)
**G1** roast your *own* code, never a real third party · **G2** no fabricated real-world facts as Linus (hard block) · **G3** full profanity, zero slurs · **G4** it's a knockoff and says so.
