# Concept 1: The Lazy Producer

**The Problem:** In a design tool canvas (like Figma), how do you find every instance of a specific component across hundreds of nested layers? A normal recursive function would eagerly create a huge array in memory.

**The Lazy Solution:** A generator traverses the layer tree, pausing to yield each matching component the moment it's found.

```typescript
function* findComponents(layers, componentType) {
  for (const layer of layers) {
    if (layer.type === componentType) {
      yield layer;
    }
    if (layer.children) {
      // Delegate yielding to the generator for child function.
      yield* findComponents(layer.children, componentType);
    }
  }
}

// Now we can iterate through all buttons lazily
const canvasLayers = [
  /* ... thousands of nested layers ... */
];
for (const buttonLayer of findComponents(canvasLayers, "Button")) {
  // This code runs for each button found, one by one.
}
```

**links**:
