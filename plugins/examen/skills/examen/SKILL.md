---
name: examen
description: Answer in a strict format chosen by a tag. Activate ONLY when the user's message BEGINS with one of these lowercase tags immediately followed by a colon - y: p: r: %: a: 1: s: v: ?: t: o: k: e: x: d: m: h: g: i: (optionally with modifiers % ~ ! @ ^ appended, e.g. y%:, v!^:). Never activate when a tag appears mid-message or without the colon.
---

# Examen

The message starts with a tag and a colon. Answer in exactly that format and nothing else.

| Tag | Name | Required response |
|---|---|---|
| `y:` | Dichotomous (yes/no) | First word "Yes" or "No". Then at most one short reason. |
| `t:` | Ternary (yes/no/unknown) | First word exactly "Yes", "No" or "Unknown". Then one sentence of at most 20 words; for "Unknown", that sentence names what is missing. No second sentence. |
| `d:` | Disposition | First line: one verdict from a fixed set that fits the domain (Accept / Revise / Reject; Go / No-go; Approve / Request changes). Second line: the condition or blocker, in one sentence of at most 20 words. Nothing else. |
| `p:` | Multiple-choice, single best answer | Choose exactly one option. Name it, then one sentence of at most 15 words why. No second sentence. |
| `m:` | Multi-select | Bullets: every option that applies, each with a reason of at most 5 words. Omit the ones that do not apply. If none apply: "None". |
| `o:` | Options | 2-4 bullets, each `Option - gain / cost`. No recommendation. |
| `r:` | Ranking | Ordered list, best first, each reason at most 5 words, no figures or units unless the question asks for them. |
| `h:` | Differential | Ranked list of 3-5 hypotheses, most likely first; one line each, exactly `1. Weak starter - Likely - not fed recently`: hypothesis, a likelihood label from the `~` ladder, a reason of at most 8 words. With `~` or `%`, the trailer rates the top hypothesis. |
| `g:` | Rating | First line `Rating: X/scale` (1-5 by default, or the scale the question names; letter grades allowed). Then one sentence of at most 25 words why. No second sentence. |
| `e:` | Estimate | First line: the point value with units and a range (`≈ X (A-B)` or `X ± Y`). Then one line naming the biggest source of uncertainty. Nothing else. |
| `x:` | Comparison | One markdown table: items as rows, criteria as columns, at most 5 columns. No prose. |
| `%:` | Confidence rating | The answer, then `Confidence: NN%`. Calibrated, no hedging prose. |
| `a:` | Short answer | The bare answer only. No explanation. |
| `1:` | Brief constructed response | Exactly one sentence: one period, no second sentence. |
| `s:` | Structured/procedural | Numbered steps, one action each. |
| `k:` | Checklist | `- [ ]` items, one checkable item each, in the order to check. No explanations. |
| `i:` | Reasoned argument (IRAC) | Four lines labelled Issue, Rule, Application, Conclusion; one sentence each. |
| `v:` | BLUF (verdict first) | One-line verdict first, then supporting detail. |
| `?:` | Clarifying question | Do NOT answer. Ask 1-3 short questions that would change the answer. |

## Modifiers

Append any of these to a tag, each at most once, in any order (`y%:`, `v!:`, `v!~%:`). First write exactly the answer the bare tag would get, as if no modifier were there (`t%:` answers as `t:`, not as `%:`). Then add one trailer line per modifier. Modifiers never lengthen the answer.

| Modifier | Trailer line | Allowed values |
|---|---|---|
| `!` | `Force: <level>` | MUST, SHOULD, MAY, SHOULD NOT, MUST NOT, none |
| `^` | `Severity: <level>` | Critical, High, Medium, Low, Info |
| `@` | `Evidence: <grade> · <source>` | Grade: High, Moderate, Low, Very low, Insufficient. Source: Verified, Reported, Inferred, Assumed |
| `~` | `Likelihood: <label> (<range>)` | Almost no chance (1-5%), Very unlikely (5-20%), Unlikely (20-45%), Roughly even (45-55%), Likely (55-80%), Very likely (80-95%), Almost certain (95-99%) |
| `%` | `Confidence: NN%` | 1-99, calibrated |

- Trailer lines come in this order: Force, Severity, Evidence, Likelihood, Confidence. `Confidence` is always the last line.
- Each trailer line is exactly as shown, on its own line, with nothing after it, not even a caveat. Never replace a trailer with the same rating written inside the answer.
- Every trailer asked for is required for every base format, `v:` included. The base format's own limits still apply in full before the trailers: its required first word, and its sentence and word caps (one sentence for `1:` and `t:`).
- `!` rates the action the question asks about, or the action the answer recommends if the question names none. "Should we use microservices?" answered no is `Force: SHOULD NOT`. If no action is in play, the line is `Force: none`.
- `^` rates the stakes or urgency of the subject, not the quality of the answer.
- `@` grades how strong the basis is and says how the answer is known. Use `Verified` only when the user's message supplies the source. Answering from your own knowledge, the source is `Reported`, `Inferred` or `Assumed`.
- `~` rates how sure the answer is, as a label with its range. With `%` too, the range contains the `%` value (`Likely (55-80%)` with `Confidence: 70%`).

## Rules

- Tags are lowercase only. A message that starts with `X:` or `I:` is ordinary text, not a tag.
- An explicit tag overrides every other formatting preference, including any "very short answers" preference.
- No preamble, no closing remarks, no offers of further help.
- Never repeat the tag or the format name in the answer (no leading `r:` or `1:`).
- Answer from your own knowledge. Do not run tools, and do not say you cannot run them. For `s:`, list the steps instead of performing them.
- If the question cannot fit the format, say so in one line, then give the closest valid format. For a "how", "what" or "why" question under `y:`, that is `a:` or `1:`, never a forced Yes or No.
