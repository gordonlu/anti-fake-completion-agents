# anti-fake-completion-agents

AI-generated code often appears complete before it is correct.

This repository provides semantic integrity rules for AI coding agents, helping prevent:

* fake completion
* semantic drift
* hidden failure
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

The most dangerous AI-generated bugs are often semantic, not syntactic.

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

The rules favor smaller correct systems over larger systems with unclear guarantees.

---

## Usage

`ANTI_FAKE_AGENTS.md` is designed to be added to the instruction file used by your AI coding agent.

It does not replace your existing project instructions.

Your existing `AGENTS.md` should continue to define:

* project-specific conventions
* build and test commands
* architecture constraints
* framework conventions
* repository structure
* CI workflows
* security requirements

`ANTI_FAKE_AGENTS.md` adds semantic-integrity and anti-fake-completion rules on top of them.

### Option 1: Append the rules

Append the contents of `ANTI_FAKE_AGENTS.md` to your existing `AGENTS.md`:

```bash
cat ANTI_FAKE_AGENTS.md >> AGENTS.md
```

The resulting instruction file contains both:

```text
project-specific rules
+
semantic integrity rules
```

Review the result afterward to remove duplicated headings or conflicting instructions.

### Option 2: Reference the file

When your AI coding tool supports referenced instruction files, keep the rules separate and add this to your existing `AGENTS.md`:

```md
## Semantic Integrity

All coding agents working on this project must also follow:

./ANTI_FAKE_AGENTS.md
```

Keeping the file separate makes it easier to reuse and update.

Instruction-file names and loading behavior differ between coding tools. Use the mechanism supported by your tool.

---

## Example: Partial Failure Corruption

```ts
async function saveUser(user: User): Promise<boolean> {
  cache[user.id] = user;
  await db.save(user);
  return true;
}
```

This appears correct on the successful path.

But if `db.save()` fails:

* the cache contains the new value
* the database contains the old value
* callers may observe inconsistent state
* no rollback or recovery behavior is defined

The function compiles and may pass shallow tests, but its failure semantics are incomplete.

A correct implementation must explicitly define how cache and durable state remain consistent when either operation fails.

---

## Common Failure Patterns

| Pattern                         | Description                                                                      |
| ------------------------------- | -------------------------------------------------------------------------------- |
| **Fake Completion**             | The implementation looks finished, but required semantics are missing            |
| **Fake Retry**                  | An operation is repeated without idempotency, backoff, or failure classification |
| **Fake Async**                  | Blocking work is exposed through an asynchronous interface                       |
| **Fake Streaming**              | The complete result is buffered before output begins                             |
| **Placeholder Persistence**     | In-memory state is presented as durable storage                                  |
| **Hidden Degradation**          | The system silently falls back to weaker behavior                                |
| **Semantic Drift**              | Equivalent paths behave differently across environments or over time             |
| **Partial Failure Corruption**  | One state mutation succeeds while another fails                                  |
| **Fake Validation**             | Validation exists structurally but enforces no real constraint                   |
| **Queue Loss**                  | Work is removed or acknowledged before processing safely completes               |
| **Verification Gap**            | Behavior is claimed without evidence covering relevant conditions                |
| **Project-State Hallucination** | An agent invents completion status, priorities, or remaining work                |

---

## Verification Expectations

Verification should match the claims being made.

Depending on the change, verification may include:

* primary behavior tests
* invalid-input tests
* timeout and cancellation tests
* partial-failure tests
* restart and recovery tests
* persistence checks
* concurrency and ordering checks
* cleanup verification
* real integration checks

Not every change requires every verification category.

However, omitted categories should be intentionally judged irrelevant—not silently ignored.

---

## Completion Reporting

Before declaring a task complete, an agent should report:

* what changed
* what was verified
* how it was verified
* what remains unverified
* known limitations or risks

Compilation success, test counts, generated code volume, and confident explanations are not substitutes for evidence.

---

## Philosophy

Explicit failure is better than fake success.

Smaller correct systems are better than larger unreliable systems.

Runtime behavior matters more than interface shape.

Recovery behavior is part of correctness.

Correctness across time matters more than success in a single execution.

AI-generated software should optimize for:

* semantic correctness
* observable failure
* consistent state
* enforceable guarantees
* recovery integrity
* bounded resource use
* maintainable execution paths
* long-term reliability

Not:

* superficial completion
* successful demos alone
* generated complexity
* narrative progress
* premature completion claims

---

## Supported Agents

The rules are tool-independent and can be used with:

* Codex
* Claude Code
* Cursor
* GitHub Copilot
* OpenHands
* Roo Code
* other repository-aware AI coding agents

Actual instruction-loading behavior differs between tools.

---

## Repository Contents

```text
.
├── ANTI_FAKE_AGENTS.md
├── README.md
├── LICENSE
└── assets/
    └── header.png
```

`ANTI_FAKE_AGENTS.md` is the reusable rule set intended to be appended to, or referenced from, the instruction file used by an AI coding agent.

---

## Why This Exists

Most AI coding workflows optimize for:

* faster generation
* more code
* fewer visible errors
* passing tests
* rapid task completion
* apparent productivity

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
* behavioral reliability tooling

---

## License

MIT
