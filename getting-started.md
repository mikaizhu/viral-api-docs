# Getting Started

This guide walks you through making your first image generation request with ViralAPI.

## Prerequisites

- A ViralAPI account with an active API Key ([get one here](https://viralapi.ai/api-key))

## Step 1: Create a Task

Send a POST request to create an image generation task:

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

Response:

```json
{
  "code": 200,
  "msg": "success",
  "data": {
    "task_id": "task_nanobanana_1765178625768"
  }
}
```

## Step 2: Poll for Results

Use the `task_id` to check the task status:

```bash
curl -X GET "https://viralapi.ai/v1/task/query?task_id=task_nanobanana_1765178625768" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

Response (completed):

```json
{
  "create_time": 1756817821,
  "complete_time": 1763088308,
  "task_type": "image",
  "task_id": "task_nanobanana_1765178625768",
  "progress": 100,
  "model": "gemini-2.5-flash-image",
  "status": "completed",
  "results": [
    "https://cdn.viralapi.ai/outputs/generated-image-1.png"
  ]
}
```

## Step 3: Download the Image

When `status` is `completed`, the `results` array contains the generated image URLs. Download them before they expire (24-hour validity).

## Using NanoBanana Pro

For higher quality output, switch to the Pro model:

```bash
curl -X POST https://viralapi.ai/v1/task/create \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-3-pro-image-preview",
    "task_type": "image",
    "input": {
      "prompt": "A futuristic city with neon lights",
      "image_size": "2K",
      "aspect_ratio": "9:16"
    }
  }'
```

The Pro model additionally supports `image_size` parameter (`1K`, `2K`, `4K`).

## Image Editing

To edit an existing image, add `image_urls` to the input:

```bash
curl -X POST https://viralapi.ai/v1/task/create \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "model": "gemini-2.5-flash-image",
    "task_type": "image",
    "input": {
      "prompt": "Transform this into a watercolor painting style",
      "image_urls": ["https://example.com/your-image.jpg"],
      "aspect_ratio": "1:1"
    }
  }'
```

The presence of `image_urls` switches the operation from text-to-image to image editing. Up to 10 images are supported.

## Next Steps

- [Authentication](authentication.md) — Token management and security
- [Async Workflow](async-workflow.md) — Polling strategies and best practices
