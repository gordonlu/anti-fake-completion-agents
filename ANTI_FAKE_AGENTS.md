AI-generated code tends toward appearing complete before being correct.

Optimize for semantic integrity, not superficial completion.

---

# Rules

1. Never fake behavior.
- no hardcoded success
- no placeholder implementations
- no fake retries
- no fake async
- no fake streaming
- no mock logic in production paths

Fail explicitly if incomplete.

---

2. Do not hide failure.
- no silent catch
- no ignored errors
- no empty fallbacks
- no fake defaults

Errors must remain observable.

---

3. Do not claim functionality without verification.

Verify using:
- failure-path tests
- persistence checks
- restart/recovery tests
- ordering checks
- cleanup checks
- concurrency checks
- state validation

Do not rely on:
- compilation success
- demo output
- shallow tests

Unverified behavior must not be presented as completed behavior.

---

4. All execution paths must preserve semantics.

Avoid semantic drift between:
- dev/prod
- test/real
- local/remote
- preview/live

---

5. Unsupported behavior must fail loudly.

Prefer:
```ts
throw new Error("NOT_IMPLEMENTED")
````

over:

```ts
return {}
return []
return true
```

---

6. State mutations must respect failure boundaries.

Do not:

1. mutate state
2. fail later
3. leave partial success visible

Protect against:

* partial writes
* queue loss
* lost rollback
* cache/db divergence
* split-brain state

---

7. Concurrency claims must match runtime reality.

Do not label blocking or sequential systems as:

* async
* parallel
* concurrent
* non-blocking

---

8. Streaming must be incremental.

Do not buffer entire results before “streaming”.

---

9. Persistence must actually persist.

In-memory state is not persistence.

Verify persistence after restart.

---

10. UTF-8 correctness is mandatory.

Do not assume:

* 1 byte == 1 character
* string length == display width
* slicing == character-safe

---

11. Every resource needs cleanup.

Bound:

* memory
* queues
* listeners
* streams
* caches
* timers

Prevent unbounded growth.

---

12. Ordering guarantees matter.

FIFO must actually be FIFO.

---

13. Security boundaries must be enforced by runtime behavior.

Validation that does not enforce anything is fake validation.

---

14. Prefer smaller correct systems.

Avoid:

* duplicated logic
* hidden coupling
* speculative abstraction
* unnecessary complexity

---

15. Document non-obvious behavior.

Especially:

* retries
* caching
* persistence
* synchronization
* concurrency
* fallback behavior

Future agents must be able to reason about the system safely.

---

16. Do not fake project-state awareness.

Avoid invented claims about:

* remaining work
* future tasks
* priorities
* deadlines
* “good enough”
* “later optimization”
* time constraints

AI agents do not possess real scheduling awareness.

---

# Final Rule

Do not optimize for the appearance of completion.

Optimize for:

* semantic correctness
* observable failure
* runtime consistency
* maintainability
* long-term reliability

```
```
