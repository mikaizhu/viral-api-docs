# NanoBanana Pro Text to Image

Generate high-quality images from text prompts using the `gemini-3-pro-image-preview` model. Supports 1K/2K/4K resolution.

{% openapi src="../openapi-nanobanana-pro.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

---

## Try It

### curl

```bash
curl -X POST https://viralapi.ai/v1/task/create \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-3-pro-image-preview",
    "task_type": "image",
    "input": {
      "prompt": "A futuristic banana with neon lights in a cyberpunk city",
      "image_size": "2K",
      "aspect_ratio": "9:16"
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
        "model": "gemini-3-pro-image-preview",
        "task_type": "image",
        "input": {
            "prompt": "A futuristic banana with neon lights in a cyberpunk city",
            "image_size": "2K",
            "aspect_ratio": "9:16"
        }
    }
)
print(resp.json())
# {"code": 200, "msg": "success", "data": {"task_id": "task_nano-banana-pro_..."}}
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
    model: "gemini-3-pro-image-preview",
    task_type: "image",
    input: {
      prompt: "A futuristic banana with neon lights in a cyberpunk city",
      image_size: "2K",
      aspect_ratio: "9:16"
    }
  })
});
const data = await resp.json();
console.log(data);
// {code: 200, msg: "success", data: {task_id: "task_nano-banana-pro_..."}}
```
