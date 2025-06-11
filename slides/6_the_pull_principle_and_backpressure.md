# The Consumer is in Control

**The Core Idea:** The consumer `for await...of` loop pulls data, setting the pace. This creates natural backpressure, preventing a fast producer (like progress events) from overwhelming a consumer.

Example: Tracking Upload Progress

```typescript
async function* upload(file) {
  const xhr = new XMLHttpRequest();
  xhr.open("POST", "/upload-endpoint", true);
  xhr.send(file);

  while (xhr.readyState !== xhr.DONE) {
    yield new Promise((resolve) => {
      const onProgress = (e) => resolve({ progress: e.loaded / e.total });
      xhr.upload.addEventListener("progress", onProgress, { once: true });
    });
  }

  yield { url: xhr.responseText };
}

// use it in redux-thunk
for await (const value of upload(myFile)) {
  if (value.progress) {
    dispatch(updateProgress(value.progress));
    continue;
  }

  if (value.url) {
    dispatch(setUploadedUrl(value.url));
  }
}
```
