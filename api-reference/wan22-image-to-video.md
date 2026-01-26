# Wan2.2 Image to Video

Convert images to dynamic videos using Wan2.2 image-to-video models. Two versions available:

- **wan2.2-i2v-flash**: Fast version, supports 480P/720P resolution
- **wan2.2-i2v-plus**: Enhanced version, supports 480P/1080P resolution

## API Endpoint

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## Usage Examples

### Flash Version Example (720P)

```json
{
  "model": "wan2.2-i2v-flash",
  "task_type": "video",
  "input": {
    "prompt": "Camera slowly zooms in on the mountain peak",
    "img_url": "https://example.com/first-frame.jpg",
    "resolution": "720P",
    "duration": 5
  }
}
```

### Plus Version Example (1080P)

```json
{
  "model": "wan2.2-i2v-plus",
  "task_type": "video",
  "input": {
    "prompt": "The scene comes alive with gentle movement",
    "img_url": "https://example.com/scene.jpg",
    "resolution": "1080P",
    "duration": 5
  }
}
```

## Image Requirements

- **Resolution**: 360-2000 pixels
- **File Size**: ≤10MB
- **Format**: JPG, PNG, WebP
- **Recommendation**: Use clear, well-composed images for best results

## Important Notes

> **Duration Limit**: wan2.2 models generate fixed 5-second videos, cannot be modified
> **Prompt Length**: Maximum 800 characters
> **Audio Support**: wan2.2 models do not support audio
> **Processing Time**: Typically 1-5 minutes
> **Video Expiration**: 24 hours, download promptly
> **Prompt Tip**: Describe the motion in the scene, not the image content itself
