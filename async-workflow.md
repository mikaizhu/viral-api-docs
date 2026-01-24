# Async Workflow

ViralAPI uses an asynchronous task processing model. All image generation requests are non-blocking — you submit a task and poll for results.

## Task Lifecycle

```
┌─────────┐     ┌────────────┐     ┌───────────┐
│ pending  │ ──> │ processing │ ──> │ completed │
└─────────┘     └────────────┘     └───────────┘
                       │
                       ▼
                 ┌──────────┐
                 │  failed  │
                 └──────────┘
```

| Status | Description | `progress` | `results` |
|--------|-------------|-----------|-----------|
| `pending` | Task queued, waiting to be processed | `0` | `[]` |
| `processing` | Image generation in progress | `1-99` | `[]` |
| `completed` | Generation finished successfully | `100` | `[url, ...]` |
| `failed` | Generation failed | `0` | `[]` |

## Polling Strategy

### Recommended Approach

```python
import time
import requests

API_KEY = "YOUR_API_KEY"
BASE_URL = "https://viralapi.ai"

def create_task(prompt, model="gemini-2.5-flash-image"):
    resp = requests.post(
        f"{BASE_URL}/v1/task/create",
        headers={"Authorization": f"Bearer {API_KEY}"},
        json={
            "model": model,
            "task_type": "image",
            "input": {"prompt": prompt}
        }
    )
    return resp.json()["data"]["task_id"]

def poll_task(task_id, interval=3, max_attempts=60):
    for _ in range(max_attempts):
        resp = requests.get(
            f"{BASE_URL}/v1/task/query",
            headers={"Authorization": f"Bearer {API_KEY}"},
            params={"task_id": task_id}
        )
        result = resp.json()

        if result["status"] == "completed":
            return result["results"]
        elif result["status"] == "failed":
            raise Exception("Task failed")

        time.sleep(interval)

    raise TimeoutError("Task did not complete in time")

# Usage
task_id = create_task("A cat wearing a space helmet")
image_urls = poll_task(task_id)
print(image_urls)
```

### Polling Intervals

| Phase | Recommended Interval |
|-------|---------------------|
| First 10 seconds | 2 seconds |
| 10-60 seconds | 3-5 seconds |
| After 60 seconds | 10 seconds |

### Node.js Example

```javascript
const API_KEY = "YOUR_API_KEY";
const BASE_URL = "https://viralapi.ai";

async function createTask(prompt, model = "gemini-2.5-flash-image") {
  const resp = await fetch(`${BASE_URL}/v1/task/create`, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": `Bearer ${API_KEY}`
    },
    body: JSON.stringify({
      model,
      task_type: "image",
      input: { prompt }
    })
  });
  const data = await resp.json();
  return data.data.task_id;
}

async function pollTask(taskId, interval = 3000, maxAttempts = 60) {
  for (let i = 0; i < maxAttempts; i++) {
    const resp = await fetch(
      `${BASE_URL}/v1/task/query?task_id=${taskId}`,
      { headers: { "Authorization": `Bearer ${API_KEY}` } }
    );
    const result = await resp.json();

    if (result.status === "completed") return result.results;
    if (result.status === "failed") throw new Error("Task failed");

    await new Promise(r => setTimeout(r, interval));
  }
  throw new Error("Timeout");
}

// Usage
const taskId = await createTask("A cat wearing a space helmet");
const urls = await pollTask(taskId);
console.log(urls);
```

## Error Handling

When a task fails or the API returns an error, the response follows a consistent structure:

```json
{
  "error": {
    "code": 500,
    "message": "Internal server error, please try again later",
    "type": "server_error",
    "fallback_suggestion": "retry after 30 seconds"
  }
}
```

### Retry Strategy

| Error Code | Retry? | Strategy |
|-----------|--------|----------|
| 400 | No | Fix request parameters |
| 401 | No | Check/refresh API key |
| 402 | No | Top up account balance |
| 403 | No | Check model access permissions |
| 404 (task) | No | Task expired, create a new one |
| 500 | Yes | Retry with exponential backoff |
| 502 | Yes | Retry after 30 seconds |
| 503 | Yes | Retry after 60 seconds |

## Image URL Expiration

Generated image URLs in the `results` array are valid for **24 hours**. Download and store them in your own storage before they expire.
