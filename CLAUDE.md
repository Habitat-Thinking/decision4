# decision4: conventions

This repository is the canonical definition of Decision4. Other repositories (the handbook, ai-literacy-superpowers) quote tagged versions of it and never redefine it.

## Changing the definition

- Work on a branch and open a pull request. Never commit to `main` directly.
- Every change updates `CHANGELOG.md` under a heading `## X.Y.Z — YYYY-MM-DD`.
- Version by meaning, not by size of diff:
  - **Major:** a class is renamed, added or removed, or a definition or rule changes meaning.
  - **Minor:** an addition that keeps existing meaning, such as an optional trailer or schema field.
  - **Patch:** wording that clarifies without changing meaning.
- Update the version in the `DECISION4.md` title, the `boundary-map.schema.json` description and the example comment when the version changes.
- Keep `examples/boundary-map.example.yaml` identical to the YAML block in `DECISION4.md` section 10. CI checks this.
- Keep `AGENTS-snippet.md` consistent with sections 3 to 7 of `DECISION4.md`. A change to one is a change to both.
- Tag each release `vX.Y.Z` after merge.

## Style

- British spelling. Short sentences. No hedging.
- The four class names are always capitalised: Undo, Repair, Migrate, Answer.
- Commit messages are concise, say what changed and why, and carry no trailers or attribution lines.
