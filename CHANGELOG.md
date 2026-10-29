# Changelog

Decision4 uses semantic versions:

- **Major**: a class is renamed, added or removed, or a definition or rule changes meaning. Adopters must migrate.
- **Minor**: something is added without changing existing meaning, such as a new optional annotation or schema field.
- **Patch**: wording that clarifies without changing meaning.

## 1.0.1 — 2026-10-29

- Clarify the Answer evidence labels. Observed covers any direct check of the system, not only what was seen. Inferred is reasoned from what was observed.
- State that general knowledge, including an agent's training, is not evidence about the case: check it and label it observed, or label it unknown.
- State why unknown is listed: it marks a gap material to the decision, so silence is not read as safety.

## 1.0.0 — 2026-10-29

- The question, the four classes and what each lets an agent hand back.
- Definitions, the three rules, who classifies, the evidence labels and the choice story.
- The handoff contract for `AGENTS.md`.
- The annotation trailers, the class-aware decision record and the boundary-map schema.
