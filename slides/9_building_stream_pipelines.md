# Building Stream Pipelines with .pipeThrough() and .pipeTo()

We chain streams to create memory-efficient pipelines that show content to the user as it's being produced, without waiting for the full download.

`.pipeTo()`: Connects a ReadableStream to a WritableStream, handling backpressure automatically.

`.pipeThrough()`: Connects a ReadableStream to a TransformStream.

Example: Stream Markdown from a server, convert it to HTML, and render it.

```typescript
// 1. A TransformStream to convert Markdown chunks to HTML
const markdownToHtml = new TransformStream({
  transform(chunk, controller) {
    // A real app would use a streaming markdown parser
    const html = `<p>${new TextDecoder().decode(chunk)}</p>`;
    controller.enqueue(html);
  },
});

// 2. A WritableStream to append HTML to the DOM
const domWriter = new WritableStream({
  write(chunk) {
    document.body.insertAdjacentHTML("beforeend", chunk);
  },
});

// 3. Fetch data and build the pipeline
fetch("/get-markdown-stream")
  .then((response) => {
    // response.body is our ReadableStream
    return response.body
      .pipeThrough(markdownToHtml) // Readable -> Transform
      .pipeTo(domWriter); // Readable -> Writable
  })
  .then(() => console.log("Stream complete!"));
```

**links:**
https://developer.chrome.com/docs/ai/render-llm-responses
