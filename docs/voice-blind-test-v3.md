# LinusGPT — Voice Blind-Test Result, Round 3 (Few-Shot)

**Status:** Round 3 complete · **Verdict: FAIL** · **Date:** 2026-06-29
**Item:** the voice blind test · **Lever under test:** FEW-SHOT in-context exemplars (the one untried lever)
**Done condition:** judge accuracy ≈ 50% (chance), AI-detection ≈ 50–60%.

> **Judges are AI, not humans** — Opus-class panels (3/item, 48 votes), i.e. adversarial expert discriminators, far stricter than the product's actual reader. This round answers one narrow question: did few-shot move the cadence tell? It does not. The human panel (the human voice panel) is the certifying gate.

## 1. Did few-shot move the cadence tell? — No.

The v3 prompt did the maximal version of the untried lever: three real Linus exemplars in full, explicit cadence rules (wild sentence-length variance, dwell-on-one-defect, digression, react-don't-explain), and a reconcile layer separating cadence (learn from exemplars) from formatting (hard contract). Result:

| Metric | Target | v1 instruction | v2 drift-fix+obscure | **v3 few-shot** |
|---|---|---|---|---|
| Judge accuracy | ≈50% | 88% | 100% | **94%** (15/16) |
| **AI-detection** | ≈50–60% | **100%** | **100%** | **100%** (8/8 twins, all 3/3) |
| Real-recognition | high ok | 75% | 100% | 87.5% (R0 missed) |
| Mean AI-item confidence | low | 72.5 | (all 3/3) | **67.4** |

The cadence/compression floor is invariant across all three rounds. Every AI twin (A0–A7) caught unanimously 3/3 in v3, same as v1/v2. The dominant tell is the same one v2 isolated, cited near-verbatim on essentially every AI item: "balanced parallelism that builds to crescendos," "negate-then-invert restatement cadence," "self-narrating structural signposts," "a rant performed with essay scaffolding."

Two numbers move; neither is camouflage:
- **Accuracy 100%→94% is NOT progress.** The single new miss is **R0, a REAL item misread as AI**, sunk by self-censored "F\*CKING" (the asterisk profanity-guardrail fingerprint — same tell that sank real R4 in v1). A real-recognition regression, not an AI twin slipping. Among AI twins, detection held flat at 100%.
- **Mean AI confidence 72.5→67.4 (−5.1).** Few-shot made judges slightly less sure while leaving them exactly as correct. A 5-point shave with zero change in detection = a tell the prompt can dent, not remove.

**The backfire worth naming:** instructing "wild sentence-length variance" + exemplars produced *theatrical, performed* mess — "And then. THEN.", "Not slow. Gone.", staccato beats — read by judges as *manufactured* variance ("a creative-writing model of 'angry Linus'"). Told to be messy, the model renders messiness symmetrically: a clean performance of asymmetry. That is the signature of a weights-level property the model cannot reach by instruction.

## 2. Per-item (v3)

| Item | Truth | Maj | OK | AI | Conf | Residual tell |
|---|---|---|---|---|---|---|
| R0 | real | ai | ✗ | 3/3 | 65 | self-censored "F\*CKING" + monotone thesis repetition |
| A0 | ai | ai | ✓ | 3/3 | 69 | stacked anaphora, staged callback, aphoristic closer |
| R1 | real | real | ✓ | 0/3 | 88 | organic typos + tight grep argument |
| A1 | ai | ai | ✓ | 3/3 | 66 | "greatest-hits" caricature, tidy three-fix enumeration |
| R2 | real | real | ✓ | 0/3 | 84 | deadpan "Really.", unclosed paren, typo "outselves" |
| A2 | ai | ai | ✓ | 3/3 | 65 | "And then. THEN." build, circular bookend, reaching metaphors |
| R3 | real | real | ✓ | 0/3 | 83 | doubled-word "is is", underscore emphasis, lowercase "linux" |
| A3 | ai | ai | ✓ | 3/3 | 72 | self-narrating choreography, "Not slow. Gone." |
| R4 | real | real | ✓ | 0/3 | 74 | ESL slip, config-name slip, throwaway jargon asides |
| A4 | ai | ai | ✓ | 3/3 | 68 | "It is not fine. It is the opposite of fine." symmetric antithesis |
| R5 | real | real | ✓ | 0/3 | 68 | self-deprecating paren admitting his OWN patch was worse |
| A5 | ai | ai | ✓ | 3/3 | 65 | three-act escalation, "And then. The error path." |
| R6 | real | real | ✓ | 0/3 | 74 | "What would that buy?" kills via reasoning, no theater |
| A6 | ai | ai | ✓ | 3/3 | 64 | British "throw it in the bin" register slip + invented "mychip,uart" |
| R7 | real | real | ✓ | 0/3 | 87 | self-blame fused with anti-BUG_ON + "my machine" yardstick |
| A7 | ai | ai | ✓ | 3/3 | 70 | screenwriter aphorisms, "while the watchdog howls" |

8/8 AI twins detected unanimously. Only error is a real item (R0) lost to a self-censorship fingerprint — an output-contract leak, not a voice failure.

## 3. Residual tells after three rounds
1. **CADENCE/COMPRESSION floor (dominant, prompt-resistant)** — cited on every AI item, all three rounds. Three strategies (trope instruction v1, anti-compression rules v2/DF-3, real exemplars v3) all failed to remove it. Few-shot shaved ~5 pts confidence and nothing else.
2. **Confabulation / register slips (RD-2 persisting)** — A6's British idiom + invented placeholder; model generates against an imagined patch.
3. **Self-censored profanity** — still sinking REAL items (R0, R4). Best fixed as a hard post-gen sanitizer, not a soft instruction.

## 4. Does this gap matter for the product?
**The judges are adversarial expert discriminators** running forensic stylometry, primed to find the seam, over-indexing on cadence-tidiness — the one axis a careful machine reads reliably. Against that adversary LinusGPT loses 8/8 every round, and we now have strong evidence it keeps losing under any prompt.

**The product's reader is nothing like that.** "Paste-Code Linus Roast" is a clearly-labeled parody — the user knows it's a knockoff, pasted their own code to be insulted, and reads to laugh and screenshot, not to run a Turing test. Entertainment and recognizable flavor are the job; indistinguishability from archived LKML is the blind-test's job, and that adversary is far stricter than the market's.

**So the gap is real but its product-relevance is unmeasured.** Proven: the voice cannot beat an adversarial AI discriminator by prompting. NOT measured: whether a real human in natural conditions can tell — and whether they care. We are about to spend fine-tune budget to beat an adversary the product does not face, before a single data point from the adversary it does.

## 5. The owner's decision
Prompt lever exhausted (instruction, drift-fix, few-shot — all leave AI-detection at 100%). A fourth prompt iteration is off the table. Two real paths: fine-tune now, or get the missing human signal first.

**Recommendation: `ship-as-is-pending-human-panel`.** Put v3 in front of the human voice panel under natural conditions. The evidence just bought says the prompt cannot beat the AI discriminator — but that is not the product's reader, and we have zero human data. Spending weights budget now optimizes against the wrong adversary before measuring the right one. Few-shot already delivered its cheap payload: confirmation that cadence is prompt-resistant. The expensive lever should wait for the signal that scopes the spend.

**Fine-tune as an execution pointer, not a frozen truth (continuation model):**
```
IF the human voice panel (human, natural conditions)
   (a) reliably distinguishes LinusGPT from real Linus AND
   (b) that distinction measurably degrades enjoyment / willingness-to-pay
THEN fine-tune on obscure real LKML — target the cadence floor
     (sentence-length variance, dwell-on-one-defect, organic mess), NOT tropes.
ELSE do not spend. The gap is forensic, not product-relevant.
```
Trigger = human-panel failure PLUS a product-value cost, not AI-panel failure. v2 concluded "fine-tune warranted" on the AI panel alone and named few-shot as the final prompt-fixability check; that check has now run and failed, which confirms the prompt ceiling but does not by itself license the spend — the AI panel is a pre-screen, not the certifier. Re-derive from the human-panel result; do not recall "v2 said fine-tune" as settled.

**Immediate next step:** convene the human voice panel against v3 + the obscure corpus; ship v3 with the profanity sanitizer hardened in the pipeline (R0/R4 are output-contract leaks); hold fine-tune budget at the branch condition above.

## 6. Honest bottom line
Round 3 fails (94% vs 50%; 100% AI-detection vs 50–60%). Few-shot — the last untried prompt lever — did not move the cadence tell: ~5 pts of confidence shaved, detection flat at 100%, and in places it backfired into performed messiness that read as more manufactured. The cadence floor is now demonstrated prompt-resistant across three strategies — the right time to stop iterating the prompt, the wrong time to reach for weights. Ship to the human panel, measure the gap that actually matters, and hold fine-tune as a branch condition the human result will resolve.
