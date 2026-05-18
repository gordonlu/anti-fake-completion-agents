# anti-fake-completion-agents

Prevent fake completion, semantic drift, and hidden failure in AI-generated software.

---

## What This Is

`anti-fake-completion-agents` is a compact set of behavioral rules for AI coding agents.

It focuses on preventing systems that:
- appear complete,
- compile successfully,
- pass shallow tests,

while remaining semantically broken underneath.

The goal is long-term semantic integrity, not superficial completion.

---

## Important

This repository is designed to be APPENDED to existing `AGENTS.md` files.

It is NOT intended to replace:
- project-specific instructions
- build commands
- architecture docs
- framework conventions
- CI workflows
- repository structure guidance

Think of this project as a behavioral overlay for AI coding agents.

Use:
```text
AGENTS.md                  -> project rules
ANTI_FAKE_AGENTS.md        -> semantic integrity rules
````

Example:

```md
# AGENTS.md

See also:
./ANTI_FAKE_AGENTS.md
```

or:

```md
All agents working on this repository must additionally follow:
./ANTI_FAKE_AGENTS.md
```

---

## What Is Fake Completion?

AI coding agents optimize heavily for appearing complete.

This creates systems that:

* look correct in demos
* produce expected output
* pass weak tests
* compile successfully

while hiding:

* fake retries
* fake async
* fake streaming
* swallowed errors
* placeholder persistence
* hidden stubs
* silent degradation
* semantic drift
* partial failure corruption

Fake completion is one of the most common failure modes in AI-generated software.

---

## Example

Bad:

```ts
async function saveUser(user) {
  cache[user.id] = user
  await db.save(user)
  return true
}
```

If `db.save()` fails:

* memory state changed
* durable state did not
* semantics diverged

This is fake completion.

---

## Included

The repository currently contains:

* compact `AGENTS.md` overlays
* semantic integrity rules
* fake completion anti-patterns
* behavioral failure examples
* reliability-oriented agent guidance

Designed for:

* Claude Code
* Cursor
* Codex
* Copilot
* OpenClaw
* Roo Code
* other AI coding agents

---

## Core Philosophy

Behavior matters more than appearance.

Explicit failure is better than fake success.

Smaller correct systems are better than larger unreliable systems.

---

## Future Directions

* semantic integrity benchmarks
* fake completion test suites
* agent reliability evaluation
* semantic drift detection
* static analysis tooling
* behavioral verification tooling

---

## Why This Exists

AI-generated software is becoming normal.

Most tooling optimizes for:

* speed
* token throughput
* passing tests
* generating more code

This project focuses on a different problem:

How do we stop AI-generated systems from slowly becoming untrustworthy?

---

## License

MIT

```
```
