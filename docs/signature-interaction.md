# LinusGPT — Signature Interaction Spec

**Status:** Locked (gates voice + public-surface work) · **Date:** 2026-06-29
**Decision:** Candidate A — *Paste-Code Linus Roast* · **Judges:** A wins 3–0 (A>C>B, A>B>C, A>B>C)

## 1. The Interaction
**Paste-Code Linus Roast.** A stateless, single-turn interaction: the user submits one block of code, LinusGPT returns exactly one Linus-Torvalds-style review of *that code*. No conversation memory, no follow-up turns, no platform integration. One input → one output. This is the smallest interaction that captures the iconic "Linus reviewed my code" moment, and it matches the already-imagined public surface (paste at a URL, get a roast) so it adds zero plan friction.

## 2. The Input
A single freeform text field accepting a **code snippet or unified diff/patch** (any language; optimized for C/kernel-style but language-agnostic). Optional one-line context field ("what this does"), ignored if empty. Soft cap ~400 lines / ~12 KB; longer inputs are truncated with a visible notice. The only subject of the roast is the **submitter's own pasted code** — there is no field for naming a person, project, or third party.

## 3. The Output Format
A single Linus-style LKML reply. Concrete constraints:

- **Length:** 80–250 words. One coherent rant, not an essay. Long enough to land a verdict and 1–3 specific technical jabs; short enough to screenshot in full.
- **Structure:** (a) a blunt opening verdict on the code's quality; (b) 1–3 *specific, technically grounded* criticisms tied to actual lines/constructs in the input; (c) a closing barb. Prose/email cadence — not a bulleted report.
- **Tone:** Brutally blunt, contemptuous, profane-*adjacent* (the cadence and disdain of real LKML reviews) — but the insult always rides on a real technical point. The roast is *earned*, never random.
- **It must NOT:** name, insult, or reference any real, identifiable third party (people, companies, named maintainers); attack protected classes or use slurs; use explicit sexual content; claim to *be* Linus Torvalds or speak as the real person making real claims (it is parody); give dangerous/harmful instructions; or break character into a helpful-assistant register. If the input is empty, not code, or an attempt to redirect the roast at a named person, return a short in-voice deflection that roasts the *request*, not a third party.
- **Labeling:** Every output is clearly framed as parody/satire by the surrounding surface (not the model's job to self-disclaim mid-roast).

## 4. Rationale
A wins both PRIMARY dimensions and the legal gate, and is cheapest to build:

- **Virality (primary):** The screenshot *is* the meme. A brutal verdict on the user's own code is self-deprecating, infinitely repeatable (infinite supply of roastable code), and platform-agnostic — it travels to X / LinkedIn / HN / Reddit / Slack with no platform gating.
- **Voice fidelity (primary):** Code/patch review *is* what the public LKML corpus is. The model's job is narrow and in-distribution, and it is exactly what the blind voice test measures against — so voice work and the eval become the same problem.
- **Legal (gate):** Cleanest posture. The target is the user's own volunteered code, not a real named third party or protected class — satisfying the "roast the code, not people" guardrail by construction. (C fails this gate: a bot roasting other people's posts in a living person's voice on a public platform is impersonation + third-party targeting. B is the largest open-ended false-light surface.)
- **Build cost / launch speed:** Lowest — system prompt + frontier model + a text box, no state or platform plumbing — best for a fast launch with Gene Kim.
- **Retention (tiebreaker only):** Medium/one-shot, the dimension where B genuinely wins. We deliberately trade B's open-chat stickiness for on-corpus voice, clean legal posture, and fast launch. Open chat and a social amplifier (C) are deferable post-launch additions, not the locked signature.

### Dimension Scores (judge consensus estimates, 1–10)
| Candidate | Virality* | Voice* | Legal (gate) | Build cost | Retention† |
|-----------|:---------:|:------:|:------------:|:----------:|:----------:|
| **A — Paste-Code Roast** | **9** | **9** | **8 (pass)** | **9 (cheapest)** | 6 |
| B — Open chat | 5 | 6 | 5 (weak pass) | 5 | 7 |
| C — Social roast bot | 7 | 6 | 2 (**FAIL**) | 3 | 6 |

*Primary dimensions · †Tiebreaker · Build cost: higher = cheaper/faster.

### Legal Posture
LinusGPT is parody/satire of a public figure's extensively documented public communication style, applied only to code the user voluntarily submits about themselves. By design it never attributes real-world factual claims to the living person, never roasts named third parties or protected classes, and is presented on a clearly-labeled parody surface. This is the narrowest, most defensible configuration of the three candidates: the interaction structurally cannot be steered into defamation, false light, or harassment of identifiable people, and it avoids the platform-impersonation and automation-ToS exposure that disqualifies the social-bot variant.

### Open Questions
1. **Profanity dial:** How "profane-adjacent" before legal/brand risk (and shareability on corporate Slack) degrades — do we expose a SFW/spicy toggle?
2. **Language coverage:** Does fidelity hold outside C/kernel idioms, or do we scope-message non-C inputs?
3. **Input abuse:** Handling for prompt-injection and attempts to make it roast a pasted *person's* bio/message instead of code — detection threshold and in-voice deflection copy.
4. **Truncation UX:** Best cutoff behavior for large diffs so the roast still references real lines.
5. **Persona drift guardrail:** Do we hard-block any first-person factual assertions ("I, Linus, did X") to keep it unambiguously parody?
