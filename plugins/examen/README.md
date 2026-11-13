# examen

A response-format protocol for Claude. Start a message with a one-letter tag and a colon, and Claude answers in exactly that format and nothing else. The tag overrides other formatting preferences, and there's no preamble or closing remarks.

## Tags

| Tag | Format | Example message | Example reply |
|---|---|---|---|
| `y:` | Yes/no: "Yes" or "No" first, then at most one short reason | `y: Is Python dynamically typed?` | Yes. Types are checked at runtime. |
| `p:` | Pick one: name the single best option, one line why | `p: Postgres, MySQL or SQLite for a CLI tool's local data?` | SQLite. It needs no server and ships as one file. |
| `r:` | Rank: ordered list, best first, a few words each | `r: Fastest to slowest: RAM, SSD, HDD` | 1. RAM: nanoseconds 2. SSD: microseconds 3. HDD: milliseconds |
| `%:` | Confidence: the answer, then `Confidence: NN%` | `%: What year did the Eiffel Tower open?` | 1889. Confidence: 97% |
| `a:` | Short answer: the bare answer only | `a: Capital of Australia?` | Canberra |
| `1:` | One sentence, exactly | `1: What is a closure?` | A closure is a function that keeps access to the variables of the scope it was created in. |
| `s:` | Steps: numbered, one action each | `s: Undo the last git commit but keep the changes` | 1. Run `git reset --soft HEAD~1`. 2. Check with `git status`. |
| `v:` | Verdict first (BLUF), then supporting detail | `v: Should we cache this endpoint?` | Yes, cache it for 60 seconds. It is read-heavy and tolerates stale data... |
| `?:` | Clarify: don't answer; ask 1-3 questions that would change the answer | `?: Which database should I use?` | What data shape? Expected scale? Hosted or self-run? |

Append `%` to any tag to add the confidence line, for example `y%:` or `v%:`.

If the tag is unknown or the question can't fit the format, Claude says so in one line and uses the closest valid format.

## Commands

Each tag also has a command that takes the question as its argument, for example `/examen:verdict Should we cache this endpoint?`.

| Tag | Command | Alias |
|---|---|---|
| `y:` | `/examen:yes-no` | `/examen:y` |
| `p:` | `/examen:pick-one` | `/examen:p` |
| `r:` | `/examen:rank` | `/examen:r` |
| `%:` | `/examen:confidence` | `/examen:c` |
| `a:` | `/examen:answer` | `/examen:a` |
| `1:` | `/examen:one-sentence` | `/examen:1` |
| `s:` | `/examen:steps` | `/examen:s` |
| `v:` | `/examen:verdict` | `/examen:v` |
| `?:` | `/examen:clarify` | `/examen:q` |

## Tags or commands?

- **Tags** (`v: ...`) are handled by the examen skill. Claude loads the skill when your message starts with a tag. This is faster to type and the only way to combine tags with `%`. Because Claude decides when to load the skill, it can occasionally miss a tagged message.
- **Commands** (`/examen:verdict ...`) always run, and each holds its full instructions. Use them when the format must be guaranteed.

## Install

```
/plugin marketplace add mmarusyk/examen
/plugin install examen@examen-marketplace
```

## Evals

[`evals/`](evals/) holds one folder per case: a `prompt.md` with the tagged message and a `graders/` folder of regex, LLM-judge and skill-loaded checks. Cases cover every tag, every `%` combination, every command and alias, edge cases and messages that must not trigger the skill. Each case also runs without the plugin, so the report shows what examen adds.

```
claude plugin eval plugins/examen -j 8 --no-publish          # all cases
claude plugin eval plugins/examen --case rank --runs 1       # one case
claude plugin eval plugins/examen --tag command              # by tag: tag, combo, command, edge, negative, override
```

Reports go to `evals/results/` (git-ignored). Add `--threshold 0.9` to fail CI below that score.

## Known limits

- Bare short commands (`/y`, `/p`, `/v`) can collide with other plugins' commands. Use the namespaced form (`/examen:y`).
- The skill activates only when the tag starts the message and is followed by a colon. A tag in the middle of a message is ignored.
