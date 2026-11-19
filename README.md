# examen-marketplace

A one-plugin marketplace for Claude Code that hosts **examen**, a response-format protocol. Start a message with a one-letter tag and a colon, and Claude answers in exactly that format and nothing else:

```
y: Is Python dynamically typed?
Yes. Types are checked at runtime.
```

Tags: `y:` yes/no, `t:` yes/no/unknown, `p:` pick one, `o:` options without a pick, `r:` rank, `e:` estimate with a range, `x:` comparison table, `%:` confidence, `a:` short answer, `1:` one sentence, `s:` steps, `k:` checklist, `v:` verdict first, `?:` clarifying questions. Each tag also has a command, such as `/examen:verdict`.

Modifiers add a rating line after the answer: `!` force (MUST to MUST NOT), `~` likelihood in words, `%` confidence as a number. Append them to any tag, for example `v!%:`.

See the [plugin README](plugins/examen/README.md) for every format, examples and the full command list.

## Install

```
/plugin marketplace add mmarusyk/examen
/plugin install examen@examen-marketplace
```

## Layout

```
.claude-plugin/marketplace.json   marketplace manifest
plugins/examen/                   the plugin: skill, commands, evals, README
```
