# Wan2.2 Text to Video

Generate videos from text descriptions using the `wan2.2-t2v-plus` model.

## API Endpoint

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## Usage Examples

### Basic Text-to-Video

```json
{
  "model": "wan2.2-t2v-plus",
  "task_type": "video",
  "input": {
    "prompt": "A serene mountain landscape at sunset with flowing clouds",
    "size": "1280*720",
    "duration": 5
  }
}
```

### With Negative Prompt

```json
{
  "model": "wan2.2-t2v-plus",
  "task_type": "video",
  "input": {
    "prompt": "A futuristic city with flying cars",
    "negative_prompt": "blurry, low quality",
    "size": "1920*1080",
    "duration": 5
  }
}
```

## Important Notes

> **Duration Limit**: wan2.2-t2v-plus generates fixed 5-second videos, cannot be modified
> **Prompt Length**: Maximum 800 characters
> **Audio Support**: wan2.2 models do not support audio
> **Processing Time**: Typically 1-5 minutes
> **Video Expiration**: 24 hours, download promptly
