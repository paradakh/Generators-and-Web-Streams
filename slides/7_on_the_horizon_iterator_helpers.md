# The Future is Simpler: TC39 Iterator Helpers

Let's revisit our findComponents example. We want to get the name of every "primary" button.

**Before:** The Manual Loop

```typescript
const primaryButtonNames = [];
for (const button of findComponents(layers, "Button")) {
  if (button.variant === "primary") {
    primaryButtonNames.push(button.name);
  }
}
// Result: ['SubmitForm', 'ConfirmModal']
```

**After:** Chaining Methods

```typescript
// (This syntax is a proposal)
const primaryButtonNames = findComponents(layers, "Button")
  .filter((button) => button.variant === "primary")
  .map((button) => button.name)
  .take(5)
  .toArray(); // or just loop over the result

// Result: ['SubmitForm', 'ConfirmModal']
```

The language is evolving to make these lazy patterns even more ergonomic and familiar, just like with Arrays.

**links:**

- https://github.com/tc39/proposal-iterator-helpers
- https://github.com/tc39/proposal-async-iterator-helpers
