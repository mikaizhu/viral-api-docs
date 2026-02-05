# Veo Video Generation API

Gemini Veo video generation API supports text-to-video, image-to-video, frame interpolation, and reference images.

## Supported Models

| Model | Version | Speed | Audio | Image-to-Video | Frame Interpolation | Reference Images |
|------|------|------|------|----------|--------|----------|
| `veo-2.0-generate-001` | 2.0 | Standard | ❌ | ✅ Single | ❌ | ❌ |
| `veo-3.0-generate-001` | 3.0 | Standard | ✅ | ✅ Single | ❌ | ❌ |
| `veo-3.0-fast-generate-001` | 3.0 | Fast | ✅ | ✅ Single | ❌ | ❌ |
| `veo-3.1-generate-preview` | 3.1 | Standard | ✅ | ✅ Single | ✅ Dual | ✅ Up to 3 |
| `veo-3.1-fast-generate-preview` | 3.1 | Fast | ✅ | ✅ Single | ✅ Dual | ✅ Up to 3 |

## Usage Modes

| Mode | images Count | referenceImages | Duration | Model Requirement |
|------|------------|-----------------|----------|----------|
| Text-to-Video | 0 | Optional 0-3* | 4/6/8s | All versions |
| Image-to-Video | 1 | Optional 0-3* | 4/6/8s | All versions |
| Frame Interpolation | 2 | **Not supported** | **8s only** | **Veo 3.1 only** |

> **Important Limitation**: Frame interpolation (2 images) and reference images (referenceImages) are mutually exclusive and cannot be used together. Reference images feature is only supported by Veo 3.1.

## Create Video Generation Task

Create a video generation task, returns task_id for subsequent queries.

{% openapi src="../.gitbook/assets/openapi-veo.yaml" path="/v1/videos" method="post" %}
{% endopenapi %}

## Query Video Task Status

Query the status and results of a video generation task. Recommended polling interval: 5 seconds.

{% openapi src="../.gitbook/assets/openapi-veo.yaml" path="/v1/videos/{task_id}" method="get" %}
{% endopenapi %}
