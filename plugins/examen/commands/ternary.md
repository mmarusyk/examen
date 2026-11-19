---
description: "Yes, no or unknown (examen t:)"
argument-hint: <question>
---
Respond to the question below in examen `t:` format. Ternary yes/no/unknown: First word exactly "Yes", "No" or "Unknown". Then one sentence of at most 20 words; for "Unknown", that sentence names what is missing. No second sentence.

This format overrides every other formatting preference, including any "very short answers" preference. No preamble or closing remarks. If the question cannot fit the format, say so in one line and give the closest valid format. Do not repeat the tag or format name. Answer from your own knowledge; do not run tools.

Question: $ARGUMENTS
