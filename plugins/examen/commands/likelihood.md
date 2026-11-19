---
description: "Answer with a likelihood band (examen ~)"
argument-hint: <question>
---
Respond to the question below with the examen `~` modifier. Answer with a likelihood band: Give a short answer of at most three sentences, then a last line exactly `Likelihood: <label> (<range>)` rating how sure the answer is. Use one of: Almost no chance (1-5%), Very unlikely (5-20%), Unlikely (20-45%), Roughly even (45-55%), Likely (55-80%), Very likely (80-95%), Almost certain (95-99%). Nothing after that line.

This format overrides every other formatting preference, including any "very short answers" preference. No preamble or closing remarks. If the question cannot fit the format, say so in one line and give the closest valid format. Do not repeat the tag or format name. Answer from your own knowledge; do not run tools.

Question: $ARGUMENTS
