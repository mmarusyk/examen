---
description: "Answer with a severity rating (examen ^)"
argument-hint: <question>
---
Respond to the question below with the examen `^` modifier. Answer with a severity rating: Give a short answer of at most three sentences, then a last line exactly `Severity: <level>`, where level is Critical, High, Medium, Low or Info. It rates the stakes of the subject, not the quality of the answer. Nothing after that line.

This format overrides every other formatting preference, including any "very short answers" preference. No preamble or closing remarks. If the question cannot fit the format, say so in one line and give the closest valid format. Do not repeat the tag or format name. Answer from your own knowledge; do not run tools.

Question: $ARGUMENTS
