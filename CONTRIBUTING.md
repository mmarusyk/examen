# Contributing

Thanks for helping improve examen. Bug reports, new tags and doc fixes are all welcome.

## Before you start

- Check the [open issues](https://github.com/mmarusyk/examen/issues) to avoid duplicates.
- For a new tag or a behavior change, open an issue first so we can agree on the format.
- By taking part you agree to follow the [Code of Conduct](CODE_OF_CONDUCT.md).

## Repository layout

```
.claude-plugin/marketplace.json   marketplace manifest
plugins/examen/skills/examen/     the skill that handles tags
plugins/examen/commands/          one command per tag, plus short aliases
plugins/examen/evals/             one folder per eval case
```

## Making a change

1. Fork the repo and create a branch from `main`.
2. Make the smallest change that solves the problem.
3. If you add or change a tag, update all of these together:
   - the skill in `skills/examen/SKILL.md`
   - the command and its alias in `commands/`
   - the tag tables in both READMEs
   - the eval cases: one for the tag, one with `%`, one for the command and one for the alias
4. Run the evals (see below) and fix any regression.
5. Open a pull request using the template.

## Running the evals

```
claude plugin eval plugins/examen -j 8 --no-publish          # all cases
claude plugin eval plugins/examen --case rank --runs 1       # one case
claude plugin eval plugins/examen --tag command              # by tag
```

Reports go to `plugins/examen/evals/results/`, which is git-ignored.

## Commit messages

Use [Conventional Commits](https://www.conventionalcommits.org), for example `feat(examen): add the t: tag` or `fix(examen): stop preamble on y:`.

## Writing style

Keep docs and instructions short and plain. State what happens, not what might.

## License

By contributing, you agree that your contributions are licensed under the [MIT License](LICENSE).
