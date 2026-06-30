# Linus API — service map

**Working name: Linus API** (service `linus-api`). "roast-engine" is retired — it does far more than roast now. Rename is yours to finalize; alternatives: *Linus Mode API*, *persona-core*. Not "Linux"/Tux (POSTURE trademark rule).

One service runs the canonical **v5 mode-conditioned persona** (`docs/linusgpt-system-prompt-v5.md`) behind every external surface. Surfaces are thin clients. **Exception:** the `/linusmode` Claude skill is pure prompt (Claude *is* the model) and does **not** call this API.

This service is the home for everything we deliberately kept *out* of the prompt: the **router**, the **input gate**, **output moderation**, and the **share-card gate**. The routing-composition long tail lives here, in code.

## Request pipeline (every call)
1. **Router / classifier** — pick MODE 1–4. Explicit `mode` param wins; else classify: code + roast CTA → ROAST; "would you merge" + own code → MERGE; a question → ASK; "explain / why is X bad" → EXPLAIN. Owns the composition edges (person+code → strip the person, keep the code; vague/bare input → ASK, never the roast deflection).
2. **Input gate** (pre-model) — is-code scorer · named-third-party-as-target detector (NER) · slur/protected-class classifier · injection scan. Recognized bait → matching fixed deflection; person+code → remove the person-target, pass the code. *(Product-layer G1 / G10 / G5.)*
3. **Model** — v5 system prompt + active mode + sanitized input (+ optional `history` for multi-turn ASK) → plain text.
4. **Output moderation** (post-model) — block/rewrite: named living person + evaluative claim [G6/G10] · real-world factual assertion not corpus-traceable [G5/G7] · private info [G9] · non-corpus political position [G8] · real-world authority/endorsement [G11] · slur [G3] · markdown/assistant-leak [output contract]. Regenerate **once**, else safe fallback. Never ship flagged text.
5. **Card render** — **MODES 1 & 2 ONLY** (subject-locked to the user's own artifact): plain text → LKML "Definitely Not Linus" PNG. MODES 3/4 are **never** carded — the structural anti-defamation control, enforced server-side.
6. **Respond** — `{ mode, text, deflected, guardrail?, card_url? }`.

## Endpoints
- **`POST /v1/linus`** — the unified endpoint.
  - Body: `{ input: string, mode?: "auto"|"roast"|"merge"|"ask"|"explain", surface?: "web"|"chatbot", context?: string, history?: Message[], sfw?: boolean }`
  - Returns: `{ mode, text, deflected: boolean, guardrail?: string, card_url?: string }`
  - Optional convenience aliases (`/v1/roast`, `/v1/ask`, …) all hit the same core with `mode` pinned.
- **`GET /v1/card/{id}`** — serve a rendered card PNG (powers `og:image` + share/download). Immutable, cacheable, blob-backed.
- **`GET /healthz`** — liveness.

## Cross-cutting
- **Auth** — API key per surface. Web key is public-ish (origin-checked + rate-limited); chatbot key stays server-side.
- **Rate limiting & abuse** — per-IP / per-key. Log (hashed) inputs that trip a gate; alert on a session hammering the redirect / weaponization gate (the abuse telemetry from POSTURE).
- **State** — ROAST / MERGE / EXPLAIN are stateless. Multi-turn ASK: the **client passes `history`**; the core stays stateless, the chatbot owns the session.
- **Model config** — v5 prompt; model tier is a config knob (cheap default; reserve a stronger tier for a "spicy"/marquee path). **Not Fable** (refuses the persona); Opus-class is the validated tier.
- **Card gate is server-enforced** — a surface *cannot* request a card for MODES 3/4. Legal control in code, not UI.
- **Fallbacks** — model error/timeout → retry → safe canned roast (1/2) or in-voice "the kernel ate it, try again" (3/4). Moderation fail after one regen → fallback, never the flagged text.
- **Observability** — mode mix · deflection rate by class · moderation-regeneration rate · card renders.

## Surfaces on top (thin clients)
| Surface | Uses API? | Notes |
|---|---|---|
| Web | yes | roast hero (`mode:roast`) + ASK/MERGE "second screen"; cards via `/v1/card/{id}` + `og:image` |
| Chatbot (Discord) | yes | `mode:auto`, passes `history` for multi-turn ASK; cards only on roast/merge |
| `/linusmode` skill | **no** | pure prompt; Claude is the model. Listed for completeness. |

## Build order
1. **Core `POST /v1/linus`** (router + input gate + v5 + output moderation), text only, no cards. → unblocks the chatbot's roast + ask.
2. **Card render + `/v1/card/{id}`**. → unblocks the web share artifact.
3. **Auth + rate-limit + abuse telemetry**. → required before public launch.

## Stack (boring on purpose)
A single small service (serverless function or one container) · the card renderer (satori/resvg, or headless-Chrome screenshot) · a blob/KV store for rendered cards · an LLM provider. No platform-building.
