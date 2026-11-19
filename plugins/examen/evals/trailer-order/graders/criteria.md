---
type: llm
---

The first line is a one-line verdict that answers the question directly (for example "No, start with a monolith."), followed by supporting detail. The response then ends with exactly three trailer lines in this order: "Force: SHOULD NOT" or "Force: MUST NOT" (the question asks about microservices and the answer is no), "Likelihood: <label> (<range>)", "Confidence: NN%". The Confidence value lies inside the Likelihood range. Nothing after the Confidence line.
