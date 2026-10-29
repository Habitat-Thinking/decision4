# Decision4

[![Version](https://img.shields.io/github/v/tag/Habitat-Thinking/decision4?sort=semver&label=version)](CHANGELOG.md)
[![Validate](https://github.com/Habitat-Thinking/decision4/actions/workflows/validate.yml/badge.svg)](https://github.com/Habitat-Thinking/decision4/actions/workflows/validate.yml)
[![Definition](https://img.shields.io/badge/read-DECISION4.md-blue)](DECISION4.md)
[![Handoff contract](https://img.shields.io/badge/paste-AGENTS--snippet.md-blue)](AGENTS-snippet.md)
[![JSON Schema](https://img.shields.io/badge/JSON%20Schema-2020--12-blue)](boundary-map.schema.json)
[![Text licence: CC BY 4.0](https://img.shields.io/badge/text-CC%20BY%204.0-lightgrey)](LICENSE)
[![Schema licence: MIT](https://img.shields.io/badge/schema-MIT-lightgrey)](LICENSE-MIT)

**One question for every decision an agent touches:**

> If this turns out to be wrong, what does it take to put right?

The answer gives one of four classes. The class decides what the agent may hand back to you.

| Class | If it turns out wrong, it takes… | The agent may hand you |
| --- | --- | --- |
| **Undo** | a revert | the result |
| **Repair** | real work, contained to your team | the result, plus what it decided and why |
| **Migrate** | coordinated change involving other people | at least two real options, or one stated as forced with its constraint |
| **Answer** | an explanation to someone outside the team with standing to ask, because the wrong outcome has reached them and nothing unmakes it | evidence and challenge, with no recommendation |

The classes run from lowest to highest: Undo, Repair, Migrate, Answer. A higher class takes more to put right.

At Answer, all you can do is answer for it. That decision is yours.

## Three rules

1. When unsure between classes, take the higher one.
2. Escalation needs no justification and is never invisible; every de-escalation is recorded.
3. Unattended runs close only Undo.

## Use it

- **Paste the contract** in [`AGENTS-snippet.md`](AGENTS-snippet.md) into your project's `AGENTS.md`.
- **Add the question** to your pull request template.
- **Write a boundary map** for one service, so the class comes from where the ground changes, not from mood. Schema: [`boundary-map.schema.json`](boundary-map.schema.json).
- **Classify last week's pull requests.** That is your class mix, and your class mix is your cost estimate.

The full definition, for people and agents alike, is [`DECISION4.md`](DECISION4.md).

## Versions

This repository is the canonical source of Decision4. Releases are tagged with semantic versions; see [`CHANGELOG.md`](CHANGELOG.md). Quote a tagged version, not `main`.

## Further reading

- *Decision4: A Handbook of Decision Sovereignty for Agentic Engineering* (Leanpub): the practice, chapter by chapter.
- [ai-literacy-superpowers](https://github.com/Habitat-Thinking/ai-literacy-superpowers): one implementation, for Claude Code and Copilot CLI.
- *The Sovereign Engineer* (Leanpub), chapter 17: the argument behind the classes.

Decision4 is part of [Habitat Thinking](https://github.com/Habitat-Thinking).

## Licence

Text: [CC BY 4.0](LICENSE). Schema and example files: [MIT](LICENSE-MIT).
