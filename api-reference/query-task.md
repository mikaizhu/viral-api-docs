# Query Task Status

Query async task execution status and results by `task_id`.

{% openapi src="../openapi-nanobanana-pro.yaml" path="/v1/task/query" method="get" %}
{% endopenapi %}

---

## Try It

### curl

```bash
curl -X GET "https://viralapi.ai/v1/task/query?task_id=task_nano-banana-pro_1765178625768" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### Python

```python
import requests

resp = requests.get(
    "https://viralapi.ai/v1/task/query",
    headers={"Authorization": "Bearer YOUR_API_KEY"},
    params={"task_id": "task_nano-banana-pro_1765178625768"}
)
result = resp.json()
print(result["status"])   # pending / processing / completed / failed
print(result["results"])  # ["https://cdn.viralapi.ai/outputs/image.png"] when completed
```

### Node.js

```javascript
const taskId = "task_nano-banana-pro_1765178625768";
const resp = await fetch(
  `https://viralapi.ai/v1/task/query?task_id=${taskId}`,
  { headers: { "Authorization": "Bearer YOUR_API_KEY" } }
);
const result = await resp.json();
console.log(result.status);   // pending / processing / completed / failed
console.log(result.results);  // ["https://cdn.viralapi.ai/outputs/image.png"] when completed
```
