# anti-fake-completion-agents

AI-generated code often appears complete before it is correct.

This repository provides semantic integrity rules for AI coding agents, helping prevent:

* fake completion
* hidden failure
* semantic drift
* state corruption
* unverifiable guarantees
* premature completion claims

![anti-fake-completion-agents header](./assets/header.png)

---

## The Problem

AI coding agents are strongly incentivized to produce visible progress:

* code compiles
* tests pass
* demos work
* output looks plausible
* explanations sound confident

These signals are useful, but they do not prove correctness.

A system may look finished while still containing:

* retries without safe retry semantics
* buffered output presented as streaming
* in-memory state presented as persistence
* errors hidden by fallbacks or empty defaults
* inconsistent state after partial failure
* validation that enforces nothing
* behavior that breaks after restart
* guarantees that do not match runtime reality

This is **fake completion**: the appearance of completion without verified semantic integrity.

---

## Core Principle

> Compilation, passing tests, and successful demos are evidence—not proof.

A change is complete only when its intended behavior remains correct under relevant real-world conditions, including:

* failure
* cancellation
* retry
* restart
* recovery
* concurrency
* partial completion
* long-running execution

Behavior matters more than appearance.

---

## What the Rules Enforce

`ANTI_FAKE_AGENTS.md` instructs coding agents to:

* verify semantics rather than surface output
* continue reasoning after the happy path succeeds
* fail explicitly instead of simulating unsupported behavior
* keep errors and degradation observable
* protect state across partial failures
* distinguish real runtime guarantees from interface labels
* preserve semantics across production, test, mock, and recovery paths
* identify assumptions and unverified behavior
* verify lifecycle, recovery, and cleanup behavior
* report evidence before declaring completion

The rules favor smaller, correct systems over larger systems with unclear guarantees.

---

## Usage

Use `ANTI_FAKE_AGENTS.md` alongside your project's existing agent instructions.

It is not a replacement for:

* project-specific conventions
* architecture documentation
* build and test commands
* repository structure guidance
* framework rules
* CI workflows
* security policies

Recommended structure:

```text
your-project/
├── AGENTS.md
├── ANTI_FAKE_AGENTS.md
└── ...
```

Reference it from your main `AGENTS.md`:

```md
# AGENTS.md

All coding agents working in this repository must also follow:

./ANTI_FAKE_AGENTS.md
```

You can copy the file directly:

```bash
curl -O https://raw.githubusercontent.com/gordonlu/anti-fake-completion-agents/main/ANTI_FAKE_AGENTS.md
```

Then commit it with the rest of your project instructions.

---

## Example: Partial Failure Corruption

```ts
async function saveUser(user: User): Promise<boolean> {
  cache[user.id] = user;
  await db.save(user);
  return true;
}
```

This appears reasonable on the successful path.

But if `db.save()` fails:

* the cache contains the new value
* the database contains the old value
* callers may observe inconsistent state
* the function has no rollback or recovery semantics

The function is syntactically valid and may pass shallow tests, but its failure behavior is incomplete.

A correct implementation must explicitly define how cache and durable state remain consistent when either operation fails.

---

## Common Failure Patterns

| Pattern                         | Description                                                                      |
| ------------------------------- | -------------------------------------------------------------------------------- |
| **Fake Completion**             | The implementation looks finished, but required semantics are missing            |
| **Fake Retry**                  | An operation is repeated without idempotency, backoff, or failure classification |
| **Fake Async**                  | Blocking work is exposed through an asynchronous interface                       |
| **Fake Streaming**              | The full result is buffered before any output is delivered                       |
| **Placeholder Persistence**     | In-memory state is presented as durable storage                                  |
| **Hidden Degradation**          | The system silently falls back to weaker behavior                                |
| **Semantic Drift**              | Equivalent paths behave differently over time or across environments             |
| **Partial Failure Corruption**  | One state mutation succeeds while another fails                                  |
| **Fake Validation**             | Validation exists structurally but does not enforce real constraints             |
| **Queue Loss**                  | Work is acknowledged or removed before processing is safely completed            |
| **Verification Gap**            | A behavior is claimed without evidence covering the relevant conditions          |
| **Project-State Hallucination** | An agent invents completion status, priorities, or remaining work                |

---

## Verification Expectations

Verification should match the claims being made.

Depending on the change, this may include:

* primary behavior tests
* invalid-input tests
* timeout and cancellation tests
* partial-failure tests
* restart and recovery tests
* persistence checks
* concurrency and ordering checks
* cleanup verification
* real integration checks

Not every change requires every category.

However, omitted categories should be intentionally judged irrelevant—not silently ignored.

---

## Completion Reporting

Before declaring a task complete, an agent should report:

* what changed
* what was verified
* how it was verified
* what remains unverified
* known limitations or risks

Compilation success, test counts, generated code volume, and confident explanations are not substitutes for this evidence.

---

## Supported Agents

The rules are tool-independent and can be used with:

* Codex
* Claude Code
* Cursor
* GitHub Copilot
* OpenHands
* Roo Code
* other repository-aware coding agents

Actual instruction-loading behavior differs between tools. Reference the file through the mechanism supported by your agent.

---

## Repository Contents

```text
.
├── AGENTS.md
├── ANTI_FAKE_AGENTS.md
├── README.md
├── LICENSE
└── assets/
    └── header.png
```

`ANTI_FAKE_AGENTS.md` contains the reusable semantic integrity rules.

---

## Why This Exists

Most AI coding workflows optimize for:

* faster generation
* more code
* fewer visible errors
* passing tests
* rapid task completion

Those goals are useful, but they can reward systems that appear finished before their behavior is trustworthy.

This project focuses on a different question:

> How can coding agents produce software whose guarantees remain true after the first successful demo?

---

## Future Directions

* semantic integrity benchmarks
* fake-completion test scenarios
* failure-path evaluation suites
* semantic drift detection
* completion-claim verification
* runtime guarantee analysis

---

## License

MIT
