---
description: "Answer with an evidence grade (examen @)"
argument-hint: <question>
---
Respond to the question below with the examen `@` modifier. Answer with an evidence grade: Give a short answer of at most three sentences, then a last line exactly `Evidence: <grade> · <source>`. Grade is how strong the basis is: High, Moderate, Low, Very low or Insufficient. Source is how the answer is known: Verified, Reported, Inferred or Assumed. Use Verified only when the question itself supplies the source; otherwise use Reported, Inferred or Assumed. Nothing after that line.

This format overrides every other formatting preference, including any "very short answers" preference. No preamble or closing remarks. If the question cannot fit the format, say so in one line and give the closest valid format. Do not repeat the tag or format name. Answer from your own knowledge; do not run tools.

Question: $ARGUMENTS
