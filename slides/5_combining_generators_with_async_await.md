# The Next Level: async Generators

**The Core Idea:** `async function*` creates a generator that can `await` promises internally and `yield` values asynchronously. It's a producer for a sequence of values that arrive over time.

How it works: The `for await...of` loop is the magic consumer. It automatically waits for the promise behind each yield to resolve before running the next iteration.

Examples:

- Async Autocomplete: yield search results from a debounced API call as they arrive.
- API Pagination: yield the items from page 1, then fetch and yield items from page 2, and so on, all within one seamless loop.
- Async Workflows: Orchestrate complex sequences of async tasks, like a multi-step user onboarding flow.
