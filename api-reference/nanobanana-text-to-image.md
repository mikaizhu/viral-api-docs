# NanoBanana Text to Image

Generate images from text prompts using the `gemini-2.5-flash-image` model.

{% openapi src="../openapi-nanobanana.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

---

## Try It

### curl

```bash
curl -X POST https://viralapi.ai/v1/task/create \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-2.5-flash-image",
    "task_type": "image",
    "input": {
      "prompt": "A serene mountain landscape at sunset with vibrant colors",
      "aspect_ratio": "16:9"
    }
  }'
```

### Python

```python
import requests

resp = requests.post(
    "https://viralapi.ai/v1/task/create",
    headers={"Authorization": "Bearer YOUR_API_KEY"},
    json={
        "model": "gemini-2.5-flash-image",
        "task_type": "image",
        "input": {
            "prompt": "A serene mountain landscape at sunset with vibrant colors",
            "aspect_ratio": "16:9"
        }
    }
)
print(resp.json())
# {"code": 200, "msg": "success", "data": {"task_id": "task_nanobanana_..."}}
```

### Node.js

```javascript
const resp = await fetch("https://viralapi.ai/v1/task/create", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_API_KEY"
  },
  body: JSON.stringify({
    model: "gemini-2.5-flash-image",
    task_type: "image",
    input: {
      prompt: "A serene mountain landscape at sunset with vibrant colors",
      aspect_ratio: "16:9"
    }
  })
});
const data = await resp.json();
console.log(data);
// {code: 200, msg: "success", data: {task_id: "task_nanobanana_..."}}
```
