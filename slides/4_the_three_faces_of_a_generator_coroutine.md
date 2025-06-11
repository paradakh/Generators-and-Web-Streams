# Concept 3: The Generator as a Coroutine

**The Core Idea:** By combining the producer and consumer roles, a generator becomes a two-way communication channel—a coroutine. It produces a value (a question) and pauses to consume a new value (an answer).

How it works:

```typescript
const answer = yield "What is your name?";
```

Example: This is the foundational model for advanced libraries that manage side-effects, like Redux Saga (put/take) and Effect-TS.
