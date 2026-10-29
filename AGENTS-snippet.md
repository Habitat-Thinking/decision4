# Decision4 handoff contract (v1)

Paste the block below into your project's `AGENTS.md`. It states sections 3 to 7 of [`DECISION4.md`](DECISION4.md) for an agent.

```markdown
## Decision4 handoff contract (v1)

For every decision you make, ask: "If this turns out to be wrong,
what does it take to put right?" Take the class from the boundary map.
Classes run from lowest to highest: Undo, Repair, Migrate, Answer.

- Undo (a revert): hand back the result.
- Repair (real work, contained to this team): hand back the result and a
  choice story: Chose / Over / Because / Commits us to.
- Migrate (coordinated change involving other people): hand back at least
  two real options, or one stated as forced with the constraint that forces it.
- Answer (an explanation to someone outside the team with standing to ask,
  because the wrong outcome has reached them and nothing unmakes it): hand back
  evidence labelled observed, inferred, asked or unknown, and your challenges.
  Do not recommend.

Rules:
- Propose a class at or above the map's floor, never below it.
- Unmapped or unsure: take the higher class and log a map gap.
- A change takes the class of its highest decision.
- Escalate freely and say who it pulls in. Never lower a class silently.
- Unattended runs close only Undo. Above Undo, hand back and stop.
```
