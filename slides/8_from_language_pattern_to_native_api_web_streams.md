# From Language Pattern to Native API: Web Streams

Generators gave us the pattern. Web Streams are the browser's native, high-performance implementation of that pattern for I/O (network requests, file system).

## Producer becomes ReadableStream

A source you read from

```typescript
const res = await fetch("/streaming-endpoint");
res.body; // ReadableStream
```

## Consumer becomes WritableStream

A destination you write to (e.g. writing to a file).

```typescript
const fileHandle = await window.showSaveFilePicker();

// Create a writable stream from the file handle
const writableStream = await fileHandle.createWritable();

// Get a writer and write data to the stream
const writer = writableStream.getWriter();
await writer.write(data);

// Close the stream to finalize writing
await writer.close();
```

This approach leverages browser-specific APIs that return WritableStream objects for efficient data output.

## Coroutine becomes TransformStream

Combination of ReadableStream and WritableStream.
Modifies data as it passes through.

```typescript
new TextEncoderStream();
new DecompressionStream("gzip");
```

**links:**

- https://web.dev/articles/streams
