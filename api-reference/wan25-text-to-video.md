# Wan2.5 Text to Video

Generate high-quality videos from text descriptions using the `wan2.5-t2v-preview` model.

## API Endpoint

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## Usage Examples

### Basic Text-to-Video

```json
{
  "model": "wan2.5-t2v-preview",
  "task_type": "video",
  "input": {
    "prompt": "A futuristic city with flying cars and neon lights",
    "size": "1280*720",
    "duration": 5
  }
}
```

### With Prompt Enhancement

```json
{
  "model": "wan2.5-t2v-preview",
  "task_type": "video",
  "input": {
    "prompt": "A peaceful garden in spring",
    "size": "1920*1080",
    "duration": 10,
    "prompt_extend": true
  }
}
```

## Important Notes

> **Prompt Enhancement**: Enable `prompt_extend: true` to automatically optimize your prompt for better results
> **Duration Options**: Choose 5 or 10 seconds, defaults to 5 seconds
> **Audio Support**: Generates videos with audio by default (auto-dubbing), customize via `audio_url`
> **Prompt Length**: Maximum 1500 characters
> **Processing Time**: Typically 1-5 minutes
> **Video Expiration**: 24 hours, download promptly
