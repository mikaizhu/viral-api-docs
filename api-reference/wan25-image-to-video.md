# Wan2.5 Image to Video

Convert images to high-quality dynamic videos using the `wan2.5-i2v-preview` model.

## API Endpoint

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## Usage Examples

### Basic Image-to-Video

```json
{
  "model": "wan2.5-i2v-preview",
  "task_type": "video",
  "input": {
    "prompt": "The city comes alive with movement and energy",
    "img_url": "https://example.com/city-scene.jpg",
    "resolution": "1080P",
    "duration": 5
  }
}
```

### Advanced Motion Control

```json
{
  "model": "wan2.5-i2v-preview",
  "task_type": "video",
  "input": {
    "prompt": "Camera slowly pans right while the character turns and smiles",
    "img_url": "https://example.com/portrait.jpg",
    "resolution": "1080P",
    "duration": 10,
    "shot_type": "multi"
  }
}
```

## Image Requirements

- **Resolution**: 360-2000 pixels
- **File Size**: ≤10MB
- **Format**: JPG, PNG, WebP
- **Recommendation**: Use clear, well-composed images for best results

## Important Notes

> **Duration Options**: Choose 5 or 10 seconds, defaults to 5 seconds
> **Audio Support**: Generates videos with audio by default (auto-dubbing), customize via `audio_url`
> **Prompt Tip**: Describe motion style and rhythm specifically, e.g., "camera slowly pans right while character gradually turns"
> **Processing Time**: Typically 1-5 minutes
> **Video Expiration**: 24 hours, download promptly
