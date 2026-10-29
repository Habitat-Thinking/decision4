# Decision4 (version 1.0.1)

Decision4 governs decisions made with and by agents. It asks one question of each decision, reads a class from the answer, and fixes what an agent may hand back for that class. This document is the canonical definition. It is written to be read by people and followed by agents.

## 1. The question

> If this turns out to be wrong, what does it take to put right?

Ask it of every decision before acting on it.

## 2. What counts as a decision

A decision is a choice among viable alternatives that commits people or systems, and that someone could later ask about.

## 3. The four classes

| Class | If it turns out wrong, it takes… | The agent may hand you |
| --- | --- | --- |
| **Undo** | a revert | the result |
| **Repair** | real work, contained to your team | the result, plus what it decided and why |
| **Migrate** | coordinated change involving other people | at least two real options, or one stated as forced with its constraint |
| **Answer** | an explanation to someone outside the team with standing to ask, because the wrong outcome has reached them and nothing unmakes it | evidence and challenge, with no recommendation |

At Answer, all you can do is answer for it. The class is not a permission tier. It sets the shape of what comes back.

## 4. Reading the question

- **Highest class wins.** A change takes the class of its highest decision. Slicing a change exists to pull its decisions apart.
- **Ask as of when you would find out.** Answer the question as of the moment you would most likely discover you were wrong. The class rises with exposure and with the time it takes to notice. Shortening detection (flags, canaries, holdout checks) is a way of lowering a class.

## 5. The three rules

1. When unsure, take the higher class.
2. Escalation needs no justification and is never invisible; every de-escalation is recorded.
3. Unattended runs close only Undo.

## 6. Who classifies

- The **boundary map** sets a floor for each part of a system (section 10).
- A person may raise a class. An agent proposes a class only at or above the floor.
- Unmapped or unsure ground takes the higher class and logs a **map gap**.
- Unclassified is never Undo. A change nobody has classified is treated as at least Repair until someone classifies it.
- When two people disagree, the higher class holds for now and the disagreement goes to whoever curates the map, as a question about the map.
- **Break-glass.** In a live incident, the incident lead acts on the evidence to hand. The classification and the record follow within a window the team sets.
- Every escalation names who it pulls in. Every de-escalation is recorded with who lowered it and why.

## 7. What comes back

**Undo.** The result.

**Repair.** The result and a **choice story**:

- **Chose:** what was decided
- **Over:** the alternative not taken
- **Because:** why
- **Commits us to:** what this now ties the team to

**Migrate.** At least two real options, each viable, with what each commits to. A single option is allowed only when stated as forced, with the constraint that forces it. The person accountable chooses, on the record.

**Answer.** Evidence and challenge. No recommendation, no ranking. Every claim carries one of four labels:

- **observed:** checked directly in the system, by reading, running or measuring it
- **inferred:** reasoned from what was observed
- **asked:** told by a person who was asked
- **unknown:** material to the decision and not established by anyone. Listing it marks the gap, so silence is not read as safety.

General knowledge, including an agent's training, is not evidence about this case. Check it and label it observed, or label it unknown.

Challenges name what would make the decision wrong. The decision, and what it commits to, are written by a person with standing to answer for it.

### The handoff contract

The text in [`AGENTS-snippet.md`](AGENTS-snippet.md) states sections 3 to 7 for an agent, ready to paste into `AGENTS.md`.

## 8. Annotation

Classes travel with changes as commit trailers, or as pull request labels with the same names.

```text
Decision-Class: Migrate
Put-right: Finance must re-run two monthly reports and re-issue refunds
Answerer: Head of Finance Engineering
Class-Change: Repair -> Migrate; raised by J. Patel; finance reports on rounding
```

| Field | Required |
| --- | --- |
| `Decision-Class` | on every change: `Undo`, `Repair`, `Migrate` or `Answer` |
| `Put-right` | at Repair and above: one line saying what it would take |
| `Answerer` | at Migrate and Answer: the person or role who answers for it |
| `Class-Change` | whenever a class is lowered; recommended when it is raised. Format: `<from> -> <to>; <lowered or raised> by <who>; <why>` |

## 9. Decision records

| Class | Record | Who writes what |
| --- | --- | --- |
| Undo | none | — |
| Repair | the choice story, in the pull request | anyone, including an agent describing what it actually did |
| Migrate | a class-aware decision record with at least two real options | an agent may draft the context and options; the accountable owner chooses |
| Answer | a class-aware decision record | the agent supplies evidence and challenge; only a person with standing writes the Decision and Commits us to |

A **class-aware decision record** has Nygard's Title, Status, Context and Decision, and these fields:

- **Class**, with its put-right answer
- **Who answers**
- **The rejected alternative**, which must have been viable
- **Provenance:** what the agent proposed (at Answer, the evidence and challenge it supplied) against what the person chose
- **Class history:** escalations, recorded de-escalations, and any design that lowered the class
- **Commits us to**, in place of Consequences: what this ties the team to, and how it could fail later
- **Last validated**
- **Revisit when:** a condition, not only a date

Class, Who answers and Commits us to are required at Migrate. All fields are required at Answer. A record is written before approval, never after.

Records serve people and agents. A person reads a record to find the reasoning and the person who holds it. An agent reads it as context and constraint, and follows a stale record as faithfully as a current one, so records are kept current: superseded, retired or re-validated. Retiring a record is a recorded Repair decision; reversing what it decided takes the class of the original decision.

## 10. The boundary map

The boundary map records where the ground changes: which parts of a system carry which floor. It is machine-readable; the schema is [`boundary-map.schema.json`](boundary-map.schema.json).

```yaml
# boundary-map.yaml (Decision4 1.0.1)
version: 1
precedence: highest-floor-wins
entries:
  - select: { paths: ["billing/**"] }
    floor: Repair
    put_right: "Fix forward inside the billing team"
    answerer: "Billing team lead"
  - select: { config_keys: ["refunds.rounding_mode"] }
    floor: Migrate
    put_right: "Finance reports on it; changing it back needs finance"
    answerer: "Head of Finance Engineering"
    records: ["docs/adr/0042-refund-rounding.md"]
  - select: { credentials: ["prod-db-write"], environments: ["production"] }
    floor: Answer
    put_right: "Customer data lost or exposed; nothing unmakes it"
    answerer: "CTO"
```

- **Selectors:** `paths`, `config_keys`, `data_stores`, `external_apis`, `credentials`, `environments`. An entry may combine kinds; it matches when all of them match.
- **Precedence:** when several entries match, the highest floor wins.
- **Changing the map** is a recorded Repair decision. Nothing lowers a class below the floor except a recorded map change.
- A map is not a register of every decision. It marks the ground; the class is read for each decision on that ground.

## 11. Unattended work

An unattended run (a loop, a scheduled job, a bot) may close only Undo work. It may prepare a Repair, Migrate or Answer handoff; closing one needs a person to receive it. How high a run may close on its own is its **ceiling**, and the default ceiling is Undo. Raising a ceiling is a recorded decision.

Credentials set the hard ceiling: an agent cannot reach Answer ground through a token that cannot touch it.

## 12. Terms

| Term | Meaning |
| --- | --- |
| Class | One of Undo, Repair, Migrate, Answer, read from the question |
| Floor | The lowest class the boundary map allows for a piece of ground |
| Map gap | Ground the boundary map does not cover, logged when met |
| Escalation | Raising a class; needs no justification, never invisible |
| De-escalation | Lowering a class; always recorded |
| Choice story | The Repair handoff: Chose / Over / Because / Commits us to |
| Answerer | The person or role who answers for a Migrate or Answer decision |
| Ceiling | The highest class an unattended run may close alone |
| Break-glass | Acting first in a live incident, classifying and recording within a set window |
