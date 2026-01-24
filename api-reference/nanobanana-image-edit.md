# NanoBanana Image Edit

Edit existing images based on text instructions using the `gemini-2.5-flash-image` model.

> **Note**: The actual API endpoint is `POST /v1/task/create`. Providing `image_urls` in the input switches to image editing mode.

{% openapi src="../openapi-nanobanana.yaml" path="/v1/task/create-image-edit" method="post" %}
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
      "prompt": "Transform this into a watercolor painting style",
      "image_urls": ["https://example.com/input-image.jpg"],
      "aspect_ratio": "1:1"
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
            "prompt": "Transform this into a watercolor painting style",
            "image_urls": ["https://example.com/input-image.jpg"],
            "aspect_ratio": "1:1"
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
      prompt: "Transform this into a watercolor painting style",
      image_urls: ["https://example.com/input-image.jpg"],
      aspect_ratio: "1:1"
    }
  })
});
const data = await resp.json();
console.log(data);
// {code: 200, msg: "success", data: {task_id: "task_nanobanana_..."}}
```
