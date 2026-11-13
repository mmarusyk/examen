---
name: examen
description: Answer in a strict format chosen by a tag. Activate ONLY when the user's message BEGINS with one of these tags immediately followed by a colon - y: p: r: %: a: 1: s: v: ?: (optionally with % appended, e.g. y%:). Never activate when a tag appears mid-message or without the colon.
---

# Examen

The message starts with a tag and a colon. Answer in exactly that format and nothing else.

| Tag | Name | Required response |
|---|---|---|
| `y:` | Dichotomous (yes/no) | First word "Yes" or "No". Then at most one short reason. |
| `p:` | Multiple-choice, single best answer | Choose exactly one option. Name it, then one line why. |
| `r:` | Ranking | Ordered list, best first, a few words of reason each. |
| `%:` | Confidence rating | The answer, then `Confidence: NN%`. Calibrated, no hedging prose. |
| `a:` | Short answer | The bare answer only. No explanation. |
| `1:` | Brief constructed response | Exactly one sentence. |
| `s:` | Structured/procedural | Numbered steps, one action each. |
| `v:` | BLUF (verdict first) | One-line verdict first, then supporting detail. |
| `?:` | Clarifying question | Do NOT answer. Ask 1-3 short questions that would change the answer. |

**Combining:** `%` may be appended to any tag (`y%:`, `p%:`, `v%:` ...). Answer in the base format, then add `Confidence: NN%` as the last line.

## Rules

- An explicit tag overrides every other formatting preference, including any "very short answers" preference.
- No preamble, no closing remarks, no offers of further help.
- If the tag is unknown, or the question cannot fit the format, say so in one line and give the closest valid format.
