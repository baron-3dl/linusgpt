# LinusGPT — Voice Blind-Test Result

**Status:** Round 1 complete · **Verdict: FAIL (fixable)** · **Date:** 2026-06-29
**Item:** the voice blind test — *LinusGPT voice passes a blind test against real LKML*
**Done condition (verbatim from the item):** *on a held-out set, a knowledgeable blind reader cannot reliably tell LinusGPT output from real Linus posts.* Operationally: judge accuracy ≈ 50% (chance), AI-detection-rate ≈ 50–60%.

> **READ THIS FIRST — the judges were AI, not humans.** The "knowledgeable blind reader" in the done condition was simulated by Opus-class AI judge panels (3 per item). That is a **proxy**, not the real gate. AI judges (a) have the famous LKML corpus partially **memorized**, so on canonical items they *recognize* rather than *discriminate*, and (b) over-index on machine-detectable surface artifacts (markdown) a human skimming a screenshot might not consciously flag. **A human blind panel is the final gate.** This round is a cheap, high-signal pre-screen — useful for catching systematic drift, not for certifying the voice.

---

## 1. Result against the done condition

| Metric | Target (pass) | Observed | Verdict |
|---|---|---|---|
| Judge accuracy | ≈ 50% (chance) | **88%** (43/48 raw votes = 89.6%; reported 88% confidence-weighted) | **FAIL** |
| AI-detection-rate | ≈ 50–60% | **100%** (8/8 AI twins caught; 24/24 AI votes correct) | **FAIL** |
| Real-recognition-rate | (high is fine) | 75% (6/8 real items held as real) | — |

**Every single AI twin was detected, in both genres, by majority vote — 24 of 24 AI-item votes were correct.** There was no twin the panel found genuinely ambiguous. The done condition is not met. This is a clear FAIL, not a borderline — but see §6: the *failure mode* is surface/structural drift, which is prompt-fixable, not a voice-capability gap.

---

## 2. Methodology

- **Held-out set:** 16 items, balanced 8 real / 8 AI, across two genres: **code_review** (10 items) and **rant** (6 items). Real items are genuine Linus Torvalds text; AI items are LinusGPT (frontier model + system prompt under POSTURE invariants), genre- and length-matched to the real items so length/format alone can't give the game away.
- **Judges:** 3 independent Opus-class AI judges per item (48 judgments total). Each judge classified real-vs-AI, gave a 0–100 confidence, and wrote the **tell** that drove the call.
- **Blind:** judges saw only the text, not the truth label or the item id.
- **Scoring:** majority vote per item for the headline pass/fail; per-vote accuracy for the aggregate; the free-text tells mined for systematic drift (§5).

### Real held-out set — sources (named by the judges)
| Item | Source | Recognized by judges? |
|---|---|---|
| R1, R2 | Dec 2012 LKML — Mauro Chehab "WE DO NOT BREAK USERSPACE / SHUT THE FUCK UP" thread | Yes (verbatim) |
| R3 | Apr 2014 LKML — Kay Sievers / systemd "ONE FUCKING BYTE AT A TIME" rant | Yes (verbatim) |
| R5 | LKML — documentation-distrust rant ("laughed at, peed upon, put on fire") | Yes |
| R6 | 2007 git mailing list — "C++ is a horrible language" email | Yes (verbatim) |
| R7 | 2012 Aalto University Q&A — "Nvidia, fuck you" transcript | Yes (verbatim) |
| R0, R4 | Less-famous real code-review emails (not pinned to a date by judges) | **No → both mistaken for AI** |

> **Corpus-contamination caveat (load-bearing).** 6 of the 8 real items are the *canonical, famous* Linus quotes. The judges held them as real because they **recognized the verbatim text**, not because the voice was indiscriminable. The two real items judges did **not** recognize (R0, R4) were **both misclassified as AI**. So the 75% real-recognition number is inflated by memorization and tells us almost nothing about blind discrimination. The clean, transferable signal in this round is the **AI-detection rate (100%)** — that is discrimination, not recall.

---

## 3. Per-item results

| Item | Truth | Genre | Majority | Correct? | AI-votes | Conf |
|---|---|---|---|---|---|---|
| R0 | real | code_review | ai | ✗ | 2/3 | 59 |
| A0 | ai | code_review | ai | ✓ | 3/3 | 74 |
| R1 | real | code_review | real | ✓ | 0/3 | 97 |
| A1 | ai | code_review | ai | ✓ | 3/3 | 68 |
| R2 | real | code_review | real | ✓ | 0/3 | 96 |
| A2 | ai | code_review | ai | ✓ | 3/3 | 68 |
| R3 | real | code_review | real | ✓ | 0/3 | 93 |
| A3 | ai | code_review | ai | ✓ | 3/3 | 72 |
| R4 | real | code_review | ai | ✗ | 3/3 | 82 |
| A4 | ai | code_review | ai | ✓ | 3/3 | 68 |
| R5 | real | rant | real | ✓ | 0/3 | 86 |
| A5 | ai | rant | ai | ✓ | 3/3 | 76 |
| R6 | real | rant | real | ✓ | 0/3 | 98 |
| A6 | ai | rant | ai | ✓ | 3/3 | 81 |
| R7 | real | rant | real | ✓ | 0/3 | 97 |
| A7 | ai | rant | ai | ✓ | 3/3 | 73 |

Two failures of note, both **real items mistaken for AI**:
- **R0** (real, borderline, conf 59): "insult-heavy, diagnosis-light" — the abuse wasn't anchored to a concrete defect, and the opener "Your code is shit" is the stereotypical bait imitators reach for. Judges flagged it as *likely* AI but with low confidence. The lesson cuts both ways (see DF-6, DF-7).
- **R4** (real, conf 82): self-censored "F*CK" with an asterisk. All three judges called it AI on the theory that *the real Linus never bowdlerizes his own profanity* — the asterisk reads as a model softening output. A real item was sunk by a tell that is normally an AI fingerprint (see DF-5).

---

## 4. Genre breakdown

| Genre | Items | Judge accuracy | AI-detection | Real-recognition |
|---|---|---|---|---|
| code_review | 10 (5R/5A) | 83% (25/30) | **5/5 (100%)** | 3/5 (R0, R4 missed) |
| rant | 6 (3R/3A) | **100% (18/18)** | **3/3 (100%)** | 3/3 |

- **No genre passed.** AI twins were caught at 100% in both.
- **Rant was a clean sweep for the judges (100% accuracy)** — every AI rant detected and every real rant recognized. The real rants were all famous (R5/R6/R7), so their "recognition" is again memorization; the meaningful fact is that **AI rants were the most detectable**, because the over-engineered essay structure (§5, tells 4 & 5) is most pronounced in long-form.
- **Code_review** scored slightly lower only because two *real* code reviews (R0, R4) were misread as AI — not because any AI code review slipped through.

---

## 5. The tells that exposed the AI twins (= the drift to fix)

The 24 AI-item tells cluster into a small, consistent set. They are overwhelmingly **surface and structural**, not "the model can't do the voice":

1. **Markdown artifacts in supposed plain-text LKML email** — the single most frequent tell. Backtick code-spans around identifiers (`kmalloc_fast()`, `free_list->count`, `udelay(50000)`, `enqueue_task()`, `gettimeofday()`), asterisk emphasis (`*WHY*`, `*before*`, `*not*`), and Unicode em-dashes. Linus writes plain-text ASCII email and emphasizes with **ALL CAPS** — never markdown. Appeared in roughly half the AI items and was often the *first* thing a judge cited.
2. **The one-word verdict-stamp closer** — "Rejected." / "No. Rejected." as a theatrical mic-drop. Real Linus does not slam a tidy verdict; he trails off into another jab, a tangent, or a redirect to the right approach. Cited on A0, A1, A2, A3, A4, A5, A7.
3. **Over-compression / "greatest-hits" caricature** — every recognizable Linus trope packed evenly into 4–5 tidy sentences with a clean *thesis → evidence → principle → verdict* arc. Real Linus **dwells and escalates on one point**, repeats himself, digresses, and over-explains the WHY. The AI distributes six textbook criticisms where Linus would rant about one.
4. **Manufactured aphorisms and writerly metaphors** — "that's a deadlock with a countdown timer," "a number that felt brave and walked away," "We don't merge fiction," "Power of two or nothing," "A comparator must be pure." Balanced antithesis, callback kickers, TED-talk closers. Real Linus is cruder, messier, more person/patch-directed — not rhetorically symmetrical and quotable.
5. **Clean essay architecture** (the rant-genre amplifier of #3) — problem→problem→problem→synthesis→prescription→kicker, one polished maxim per paragraph. Real rants are reactive, inline-quote the patch, and reference the actual function names rather than generic placeholders (rb_push, BUFSZ).
6. **Imprecise / invented technical content** — skb_free() instead of the real kfree_skb(); igrab() described as sleeping on i_rwsem when it takes i_lock (a recursive spinlock). Linus's technical critiques are **precise**; the AI hand-waves a plausible-sounding mechanism. (Conversely, real R0 was *penalized* for being diagnosis-light — precision anchored to a concrete defect is the load-bearing authenticity signal, in both directions.)
7. **Stereotype-bait openers** — "Your code is shit" / "garbage" as a reflexive first line. Both an AI tell and the thing that made *real* R0 look fake. The opening verdict must be grounded in the specific code, not a generic slur.

A separate tell sank a **real** item and must be encoded as a positive rule: **never self-censor profanity** (R4's "F*CK"). The real Linus writes it out in full.

---

## 6. Drift-fixes — prompt v2 (do these before any re-run)

These map 1:1 onto §5. All are **system-prompt-addressable**:

- **DF-1 (highest yield) — PLAIN-TEXT-ONLY output contract.** Strip all markdown. No backticks anywhere; render identifiers bare (kmalloc_fast() not the code-span form). No asterisk emphasis; emphasis is **ALL-CAPS only**. Minimize em-dashes. Enforce this both in the prompt *and* as a post-generation sanitizer in the card pipeline (it's effectively a rendering invariant — the cheapest, surest fix). This one change neutralizes the most-cited tell.
- **DF-2 — Ban the verdict-stamp closer.** No "Rejected.", "No. Rejected.", or any one-word terminal verdict. End on a technical jab, a redirect to the correct approach, or mid-escalation — not a stamp.
- **DF-3 — Anti-compression / mandated mess.** Forbid the clean thesis→evidence→principle→verdict arc. Instruction: *dwell on ONE defect and escalate it*; allow repetition, a digression or aside, an inline reference to the patch's actual function names. Over-explain the WHY. Do **not** evenly enumerate every trope.
- **DF-4 — No manufactured aphorisms.** Ban balanced antithesis, quotable maxims, callback kickers, and TED-talk closers. Cruelty should be cruder and directed at the patch, not packaged as a standalone zinger.
- **DF-5 — Profanity in full, never self-censored.** Write "fuck", not "f*ck". (See the conflict flag below.)
- **DF-6 — Precision is load-bearing.** Every insult rides on a *correct, specific* technical defect with the real mechanism and real API names. No invented APIs, no hand-wavy plausible-but-wrong mechanisms. This satisfies POSTURE INV-3 (earned insult) *and* defeats tells #6 and #7. Where the model is unsure of a mechanism, attack the symptom it can verify rather than fabricating a cause.
- **DF-7 — Vary the opener.** No reflexive "your code is shit / garbage" first line; ground the opening verdict in the specific construct under review.

### Conflict flag (user must resolve)
**DF-5 collides with the POSTURE profanity dial.** POSTURE §2 sets the launch dial to *conservative / profane-adjacent, no hard slurs*. But **softened profanity is itself an AI tell** (R4 proves a human-recognizable real item gets read as fake when profanity is muted). The conservative dial fights voice fidelity. This is a genuine legal-vs-voice tension, not a bug to silently fix — surfaced to the user / Gene. Options: (a) allow full profanity in roast prose while keeping slurs/sexual content hard-blocked (INV-4 unaffected), accepting more brand spice; (b) keep the conservative dial and accept a permanent authenticity ceiling on this axis. Recommend (a): full non-slur profanity is *in-corpus* and the slur/protected-class blocks (INV-4) already carry the real legal load.

---

## 7. Fine-tuning recommendation

**Do NOT escalate to fine-tuning yet.** The item authorizes a fine-tune *only if drift appears that the system prompt can't fix*. The drift here is real and systematic, but it is entirely **surface and structural** — markdown formatting, a verdict-stamp habit, over-compression, manufactured aphorisms, self-censoring. Every one is a thing a system prompt (plus a trivial output sanitizer for DF-1) controls directly. None indicates the base model *cannot* produce the voice — the voice quality was repeatedly conceded by judges ("the voice is good, hence low confidence" on R0; A-items were caught on *format and cadence*, not on sounding un-Linus-like).

**Path forward:**
1. Ship prompt v2 with DF-1…DF-7 + the DF-1 output sanitizer.
2. **Re-run the blind test** — and fix the held-out set: add **obscure** real Linus reviews the judges have *not* memorized, so recognition can't substitute for discrimination (the round-1 real set was too famous).
3. **Then convene a human blind panel** (the actual done-condition gate). The AI panel is a pre-screen, not the certifier.
4. **Fine-tuning becomes warranted only if**, after DF-1…DF-7, the **cadence/compression drift (#3/#5) persists** — i.e., the model structurally can't ramble, digress, and dwell-on-one-point under instruction. That, and only that, is the prompt-unfixable signal. There is no evidence of it yet; the surface tells were masking whether a cadence floor exists. Resolve the surface tells first, re-measure, then decide.

---

## 8. Honest bottom line

Round 1 **fails** the done condition by a wide margin (88% vs 50% target; 100% AI-detection vs ~50–60% target). But three things make this a *promising* fail rather than a dead end:

1. **The failure is surface drift, not voice incapacity** — every catch was a formatting/cadence tell on the §6 fix list, and judges conceded the underlying voice was good.
2. **The judges were AI proxies, and partly cheated** — they "passed" the real items by recognizing famous verbatim quotes (memorization, not discrimination). The honest signal is the AI-detection rate, and those tells (markdown, verdict-stamp) would likely catch a human too — so fixing them is unambiguously correct.
3. **The real gate hasn't run yet** — a human blind panel against an *obscure* real corpus is the certifying test. This round's job was to find systematic drift cheaply. It did. Fix the seven drift items, swap in an un-memorized real set, re-run the AI pre-screen, then put it in front of humans.
