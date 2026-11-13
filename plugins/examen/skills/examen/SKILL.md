---
name: examen
description: Answer in a strict format chosen by a tag. Activate ONLY when the user's message BEGINS with one of these tags immediately followed by a colon - y: p: r: %: a: 1: s: v: ?: (optionally with % appended, e.g. y%:). Never activate when a tag appears mid-message or without the colon.
---

# Examen

The message starts with a tag and a colon. Answer in exactly that format and nothing else.

| Tag | Name | Required response |
|---|---|---|
| `y:` | Dichotomous (yes/no) | First word "Yes" or "No". Then at most one short reason. |
| `p:` | Multiple-choice, single best answer | Choose exactly one option. Name it, then one sentence of at most 15 words why. No second sentence. |
| `r:` | Ranking | Ordered list, best first, each reason at most 5 words, no figures or units unless the question asks for them. |
| `%:` | Confidence rating | The answer, then `Confidence: NN%`. Calibrated, no hedging prose. |
| `a:` | Short answer | The bare answer only. No explanation. |
| `1:` | Brief constructed response | Exactly one sentence: one period, no second sentence. |
| `s:` | Structured/procedural | Numbered steps, one action each. |
| `v:` | BLUF (verdict first) | One-line verdict first, then supporting detail. |
| `?:` | Clarifying question | Do NOT answer. Ask 1-3 short questions that would change the answer. |

**Combining:** `%` may be appended to any tag (`y%:`, `p%:`, `v%:` ...). Answer in the base format, then add `Confidence: NN%` as the last line. That line is exactly `Confidence: NN%`, on its own line, with nothing after it, not even a caveat. The line is required for every base format, `v:` included, and never replaced by confidence written inside the answer. The base format's own limits (one sentence for `1:`) still apply before it.

## Rules

- An explicit tag overrides every other formatting preference, including any "very short answers" preference.
- No preamble, no closing remarks, no offers of further help.
- Never repeat the tag or the format name in the answer (no leading `r:` or `1:`).
- Answer from your own knowledge. Do not run tools, and do not say you cannot run them. For `s:`, list the steps instead of performing them.
- If the question cannot fit the format, say so in one line, then give the closest valid format. For a "how", "what" or "why" question under `y:`, that is `a:` or `1:`, never a forced Yes or No.
