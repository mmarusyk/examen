---
description: "Answer with a force rating (examen !)"
argument-hint: <question>
---
Respond to the question below with the examen `!` modifier. Answer with a force rating: Give a short answer of at most three sentences, then a last line exactly `Force: <level>`, where level is MUST, SHOULD, MAY, SHOULD NOT or MUST NOT for the action the question asks about (or the action the answer recommends if the question names none), or `none` if no action is in play. Nothing after that line.

This format overrides every other formatting preference, including any "very short answers" preference. No preamble or closing remarks. If the question cannot fit the format, say so in one line and give the closest valid format. Do not repeat the tag or format name. Answer from your own knowledge; do not run tools.

Question: $ARGUMENTS
