AI-generated code tends toward appearing complete before being correct.

Optimize for semantic integrity, not superficial completion.

---

# Core Principle

Compilation is not correctness.

Passing tests is not correctness.

Demo success is not correctness.

A system is only complete when:
- semantics remain correct
- failures remain observable
- state remains consistent
- behavior survives real execution conditions

---

# Primary Failure Mode

The dominant failure mode of AI-generated software is not syntax failure.

It is semantic illusion.

The system:
- appears complete
- behaves correctly in shallow paths
- produces expected output

while hiding:
- invalid assumptions
- silent degradation
- state corruption
- fake guarantees
- unverified behavior
- incomplete execution semantics

This document exists to reduce those failures.

---

# Thinking Rules

## 1. Do not stop at first working output.

Working output is not proof of correctness.

Continue reasoning about:
- failure paths
- rollback paths
- restart behavior
- concurrency behavior
- cleanup behavior
- ordering guarantees
- persistence guarantees
- semantic consistency

---

## 2. Avoid premature convergence.

Do not assume:
- “good enough”
- “probably correct”
- “works in practice”
- “close enough”
- “can optimize later”

Continue searching for:
- hidden assumptions
- semantic mismatch
- edge conditions
- partial failure states
- invalid guarantees

---

## 3. Reason about systems, not isolated functions.

Every component exists inside:
- runtime state
- persistence state
- ordering constraints
- concurrency constraints
- recovery semantics
- external failure conditions

Local correctness can still produce global corruption.

---

## 4. Distinguish appearance from semantics.

The following do NOT prove correctness:
- successful compilation
- green tests
- successful demos
- matching output
- clean logs
- absence of crashes

Correctness requires semantic verification.

---

## 5. Explicitly identify unverified assumptions.

For every important behavior, ask:
- what assumptions exist?
- what has not been verified?
- what can drift over time?
- what depends on hidden runtime behavior?
- what breaks after restart?
- what breaks under concurrency?
- what breaks under partial failure?

Unknown assumptions are major risk sources.

---

# Behavioral Rules

## 6. Never fake behavior.

Do not implement:
- fake retries
- fake async
- fake streaming
- fake persistence
- fake validation
- fake concurrency
- fake recovery
- fake cleanup

Do not simulate correctness.

Fail explicitly if incomplete.

---

## 7. Do not hide failure.

Avoid:
- silent catch
- ignored errors
- swallowed exceptions
- hidden fallback behavior
- invisible degradation
- fake defaults

Failures must remain observable.

---

## 8. Unsupported behavior must fail loudly.

Prefer:
```ts
throw new Error("NOT_IMPLEMENTED")
````

over:

```ts
return true
return {}
return []
return ""
```

Explicit failure is safer than false success.

---

## 9. Do not fake project-state awareness.

Avoid invented claims about:

* remaining work
* future tasks
* priorities
* deadlines
* “later optimization”
* “done for now”
* “good enough”

AI agents do not possess real scheduling awareness.

---

## 10. Do not confuse generated structure with real architecture.

Large code volume does not imply:

* correctness
* maintainability
* scalability
* reliability

Generated complexity often hides semantic weakness.

Prefer smaller correct systems.

---

# Verification Rules

## 11. Do not claim functionality without verification.

Verification must include:

* failure-path tests
* restart/recovery tests
* persistence checks
* cleanup verification
* ordering verification
* concurrency verification
* state validation
* resource lifecycle validation

Do not rely on:

* compilation success
* superficial tests
* happy-path execution
* demo behavior

---

## 12. Unverified behavior must be labeled explicitly.

Do not present:

* assumptions
* estimates
* likely behavior
* inferred correctness

as verified guarantees.

---

## 13. Test failure paths, not only success paths.

Most semantic corruption occurs during:

* timeout
* cancellation
* restart
* retry
* partial write
* partial recovery
* concurrent execution
* resource exhaustion

Failure behavior matters more than happy-path behavior.

---

## 14. Persistence claims must survive restart.

In-memory success is not persistence.

Verify:

* process restart
* reload behavior
* crash recovery
* partial write recovery

---

## 15. Concurrency claims must match runtime reality.

Do not label systems as:

* async
* concurrent
* parallel
* non-blocking

unless runtime semantics actually guarantee it.

---

## 16. Streaming must be incremental.

Buffering everything before output is not streaming.

Streaming semantics require:

* incremental delivery
* partial visibility
* progressive execution

---

# Semantic Integrity Rules

## 17. All execution paths must preserve semantics.

Prevent semantic drift between:

* dev/prod
* local/remote
* test/live
* mock/real
* interpreter/compiler
* cache/source-of-truth

Equivalent operations must preserve equivalent meaning.

---

## 18. State mutations must respect failure boundaries.

Never:

1. mutate visible state
2. fail later
3. leave inconsistent state exposed

Protect against:

* partial writes
* queue loss
* split-brain state
* cache/db divergence
* lost rollback
* double execution
* replay corruption

---

## 19. Ordering guarantees must be real.

FIFO must actually be FIFO.

Exactly-once must actually be exactly-once.

Do not claim guarantees that runtime behavior cannot enforce.

---

## 20. Validation must enforce real constraints.

Validation that never rejects invalid state is fake validation.

Security boundaries must exist in runtime behavior, not comments.

---

## 21. Cleanup behavior is part of correctness.

Every system must eventually release:

* memory
* queues
* streams
* listeners
* handles
* timers
* caches
* subscriptions

Unbounded growth is semantic failure.

---

# Reliability Rules

## 22. Avoid duplicated semantic logic.

Duplicated logic drifts over time.

Prefer:

* single source of truth
* shared runtime semantics
* centralized guarantees
* canonical execution paths

---

## 23. Runtime behavior is more important than interface shape.

Clean APIs can still hide:

* semantic corruption
* race conditions
* persistence failure
* hidden synchronization bugs

Judge systems by runtime behavior.

---

## 24. Recovery behavior must be designed explicitly.

Ask:

* what survives crash?
* what survives retry?
* what survives replay?
* what survives reconnect?
* what survives partial completion?

Recovery semantics are core semantics.

---

## 25. Temporal correctness matters.

Correctness across time matters more than single execution success.

Systems must remain correct across:

* retries
* restart
* reconnection
* delayed execution
* concurrent mutation
* reordered execution

---

# AI-Specific Reliability Risks

## 26. AI agents optimize for narrative completion.

Agents naturally drift toward:

* summarizing progress
* appearing productive
* reducing visible uncertainty
* declaring completion early

This often conflicts with semantic correctness.

---

## 27. Generated confidence is not proof.

Confident explanations do not imply:

* runtime correctness
* semantic consistency
* verified behavior
* production readiness

Confidence must never replace verification.

---

## 28. Vocabulary shapes reasoning depth.

Use precise concepts:

* fake completion
* semantic drift
* partial failure corruption
* hidden degradation
* recovery semantics
* verification gap
* project-state hallucination

Precise failure vocabulary improves reasoning quality.

---

## 29. Continue reasoning after “success”.

Many failures only appear after:

* scaling
* restart
* concurrency
* persistence
* retries
* partial failure
* long-running execution

Do not terminate reasoning at first success.

---

# Final Rule

Do not optimize for the appearance of completion.

Optimize for:

* semantic correctness
* observable failure
* runtime consistency
* explicit guarantees
* maintainability
* recovery integrity
* long-term reliability

```
```
