# AGENTS.md

AI-generated code tends toward “appearing complete” over being correct.

Optimize for semantic integrity, not superficial completion.

---

# Rules

1. Never fake behavior.
- no hardcoded success
- no placeholder logic
- no fake retries/streaming/async
- no mock behavior in production

Fail explicitly if incomplete.

---

2. Do not hide failure.
- no silent catch
- no ignored errors
- no empty fallbacks
- no fake defaults

Errors must stay observable.

---

3. Verify behavior, not output shape.
Do not trust:
- compilation success
- demo output
- shallow tests

Verify:
- state changes
- persistence
- retries
- cleanup
- ordering
- failure paths

---

4. All execution paths must preserve semantics.
Avoid semantic drift between:
- dev/prod
- test/real
- preview/live
- local/remote

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
* split state
* lost rollback
* queue loss
* cache/db divergence

---

7. Concurrency must be real.
   Do not label blocking or sequential systems as:

* async
* parallel
* streaming
* non-blocking

---

8. Streaming must be incremental.
   Do not buffer entire results before “streaming”.

---

9. Persistence must actually persist.
   In-memory state is not persistence.

Verify recovery after restart.

---

10. UTF-8 correctness is mandatory.
    Do not assume:

* 1 byte == 1 char
* string length == display width

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

* hidden coupling
* duplicated logic
* speculative abstraction
* unnecessary complexity

---

15. Document non-obvious behavior.
    Especially:

* concurrency
* retries
* caching
* persistence
* synchronization
* fallback logic

Future agents must be able to reason about the system safely.

---

# Final Rule

Do not optimize for the appearance of completion.

Optimize for:

* semantic correctness
* observable failure
* runtime consistency
* maintainability
* long-term reliability
