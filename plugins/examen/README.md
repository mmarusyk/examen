# examen

A response-format protocol for Claude. Start a message with a one-letter tag and a colon, and Claude answers in exactly that format and nothing else. The tag overrides other formatting preferences, and there's no preamble or closing remarks.

## Tags

| Tag | Format | Example message | Example reply |
|---|---|---|---|
| `y:` | Yes/no: "Yes" or "No" first, then at most one short reason | `y: Is Python dynamically typed?` | Yes. Types are checked at runtime. |
| `t:` | Yes/no/unknown: "Yes", "No" or "Unknown" first; for "Unknown", what is missing | `t: Is the continuum hypothesis true?` | Unknown. It is independent of ZFC, so it can be neither proved nor disproved there. |
| `d:` | Disposition: one verdict from a fixed set, then the condition or blocker | `d: Review this PR description: "Fix stuff."` | Request changes. Say what changed and why. |
| `p:` | Pick one: name the single best option, one line why | `p: Postgres, MySQL or SQLite for a CLI tool's local data?` | SQLite. It needs no server and ships as one file. |
| `m:` | Multi-select: every option that applies, a few words each | `m: Which are prime: 2, 9, 11, 15, 17?` | - 2: only even prime - 11: no divisors - 17: no divisors |
| `o:` | Options: 2-4 bullets with gain and cost, no pick | `o: How should I deploy a small Flask app?` | - Render - git-push deploys / cold starts on free tier - VPS - full control / you patch it |
| `r:` | Rank: ordered list, best first, a few words each | `r: Fastest to slowest: RAM, SSD, HDD` | 1. RAM: nanoseconds 2. SSD: microseconds 3. HDD: milliseconds |
| `h:` | Differential: ranked hypotheses, each with a likelihood word | `h: Why is my sourdough not rising?` | 1. Weak starter - Likely - bubbles slow to appear 2. Cold kitchen - Unlikely - ... |
| `g:` | Rating: `Rating: X/5` (or the scale asked for), then one sentence why | `g: How secure is bcrypt at cost 12?` | Rating: 4/5. Slow by design, but Argon2id resists GPUs better. |
| `e:` | Estimate: point value with a range, then the main uncertainty | `e: How far is the Moon from Earth?` | ≈ 384,400 km (363,000-406,000 km). The orbit is elliptical. |
| `x:` | Compare: one table, items as rows, at most 5 columns | `x: Compare Python, Go and Rust for a CLI tool` | \| Language \| Startup \| Binary \| ... |
| `%:` | Confidence: the answer, then `Confidence: NN%` | `%: What year did the Eiffel Tower open?` | 1889. Confidence: 97% |
| `a:` | Short answer: the bare answer only | `a: Capital of Australia?` | Canberra |
| `1:` | One sentence, exactly | `1: What is a closure?` | A closure is a function that keeps access to the variables of the scope it was created in. |
| `s:` | Steps: numbered, one action each | `s: Undo the last git commit but keep the changes` | 1. Run `git reset --soft HEAD~1`. 2. Check with `git status`. |
| `k:` | Checklist: `- [ ]` items in the order to check, no explanations | `k: Before merging a pull request` | - [ ] Tests pass - [ ] Review approved - [ ] Branch up to date |
| `i:` | Reasoned argument: Issue, Rule, Application, Conclusion, one sentence each | `i: Is a verbal agreement to sell a used car binding?` | Issue: ... Rule: ... Application: ... Conclusion: ... |
| `v:` | Verdict first (BLUF), then supporting detail | `v: Should we cache this endpoint?` | Yes, cache it for 60 seconds. It is read-heavy and tolerates stale data... |
| `?:` | Clarify: don't answer; ask 1-3 questions that would change the answer | `?: Which database should I use?` | What data shape? Expected scale? Hosted or self-run? |

## Modifiers

Append modifiers to any tag, each at most once and in any order, for example `y%:` or `v!^%:`. Each adds one trailer line after the answer, always in the order shown below, so `Confidence` stays last.

| Modifier | Rates | Trailer line | Values |
|---|---|---|---|
| `!` | Force: how strongly the answer pushes its action | `Force: SHOULD NOT` | MUST, SHOULD, MAY, SHOULD NOT, MUST NOT, none |
| `^` | Severity: the stakes of the subject, not the answer | `Severity: High` | Critical, High, Medium, Low, Info |
| `@` | Evidence: how strong the basis is, and how it is known | `Evidence: Moderate · Reported` | High, Moderate, Low, Very low, Insufficient · Verified, Reported, Inferred, Assumed |
| `~` | Likelihood: how sure the answer is, in words | `Likelihood: Likely (55-80%)` | Almost no chance (1-5%) up to Almost certain (95-99%), seven bands |
| `%` | Confidence: how sure the answer is, as a number | `Confidence: 70%` | 1-99 |

With `~` and `%` together, the likelihood band contains the confidence number. examen answers without tools, so `@` says `Verified` only when your message supplies the source.

If the question can't fit the format, Claude says so in one line and uses the closest valid format. A message with an unknown tag (`w:`) is answered normally. Tags are lowercase only, so `X:` or `I:` at the start of a message is ordinary text.

## Commands

Each tag also has a command that takes the question as its argument, for example `/examen:verdict Should we cache this endpoint?`.

| Tag | Command | Alias |
|---|---|---|
| `y:` | `/examen:yes-no` | `/examen:y` |
| `t:` | `/examen:ternary` | `/examen:t` |
| `d:` | `/examen:disposition` | `/examen:d` |
| `p:` | `/examen:pick-one` | `/examen:p` |
| `m:` | `/examen:multi-select` | `/examen:m` |
| `o:` | `/examen:options` | `/examen:o` |
| `r:` | `/examen:rank` | `/examen:r` |
| `h:` | `/examen:differential` | `/examen:h` |
| `g:` | `/examen:rating` | `/examen:g` |
| `e:` | `/examen:estimate` | `/examen:e` |
| `x:` | `/examen:compare` | `/examen:x` |
| `%:` | `/examen:confidence` | `/examen:c` |
| `a:` | `/examen:answer` | `/examen:a` |
| `1:` | `/examen:one-sentence` | `/examen:1` |
| `s:` | `/examen:steps` | `/examen:s` |
| `k:` | `/examen:checklist` | `/examen:k` |
| `i:` | `/examen:argument` | `/examen:i` |
| `v:` | `/examen:verdict` | `/examen:v` |
| `?:` | `/examen:clarify` | `/examen:q` |
| `!` | `/examen:force` | `/examen:f` |
| `^` | `/examen:severity` | `/examen:sev` |
| `@` | `/examen:evidence` | `/examen:ev` |
| `~` | `/examen:likelihood` | `/examen:l` |

## Tags or commands?

- **Tags** (`v: ...`) are handled by the examen skill. Claude loads the skill when your message starts with a tag. This is faster to type and the only way to combine a tag with modifiers. Because Claude decides when to load the skill, it can occasionally miss a tagged message.
- **Commands** (`/examen:verdict ...`) always run, and each holds its full instructions. Use them when the format must be guaranteed.

## Install

```
/plugin marketplace add <owner>/examen-marketplace
/plugin install examen@examen-marketplace
```

## Evals

[`evals/`](evals/) holds one folder per case: a `prompt.md` with the tagged message and a `graders/` folder of regex, LLM-judge and skill-loaded checks. Cases cover every tag, every `%` combination, every modifier and the trailer order, every command and alias, edge cases and messages that must not trigger the skill. Each case also runs without the plugin, so the report shows what examen adds.

```
claude plugin eval plugins/examen -j 8 --no-publish          # all cases
claude plugin eval plugins/examen --case rank --runs 1       # one case
claude plugin eval plugins/examen --tag command              # by tag: tag, combo, command, edge, negative, override
```

Reports go to `evals/results/` (git-ignored). Add `--threshold 0.9` to fail CI below that score.

## Known limits

- Bare short commands (`/y`, `/p`, `/v`) can collide with other plugins' commands. Use the namespaced form (`/examen:y`).
- The skill activates only when the tag starts the message and is followed by a colon. A tag in the middle of a message is ignored, and so is an uppercase one.
