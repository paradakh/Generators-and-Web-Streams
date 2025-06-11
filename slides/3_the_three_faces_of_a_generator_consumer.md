# Concept 2: The Generator as a Data Consumer

**The Core Idea:** A generator can also pause its execution to wait for input. It becomes an "observer" that you can push data into using .next(value).

Example: (A simple logger)

```typescript
function* logger() {
  while (true) {
    const message = yield; // Pause and wait for a message
    console.log(new Date().toISOString(), message);
  }
}
const myLogger = logger();
myLogger.next(); // Start the logger, now it's waiting...
myLogger.next("User clicked button");
```

**Other Use Cases:** Builder pattern, event collectors, simple state machines.
