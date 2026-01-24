# Veo Video Generation API

Gemini Veo 视频生成 API，支持文生视频、图生视频、帧插值和参考图片等功能。

## 支持的模型

| 模型 | 版本 | 速度 | 音频 | 图生视频 | 帧插值 | 参考图片 |
|------|------|------|------|----------|--------|----------|
| `veo-2.0-generate-001` | 2.0 | 标准 | ❌ | ✅ 单图 | ❌ | ❌ |
| `veo-3.0-generate-001` | 3.0 | 标准 | ✅ | ✅ 单图 | ❌ | ❌ |
| `veo-3.0-fast-generate-001` | 3.0 | 快速 | ✅ | ✅ 单图 | ❌ | ❌ |
| `veo-3.1-generate-preview` | 3.1 | 标准 | ✅ | ✅ 单图 | ✅ 双图 | ✅ 最多3张 |
| `veo-3.1-fast-generate-preview` | 3.1 | 快速 | ✅ | ✅ 单图 | ✅ 双图 | ✅ 最多3张 |

## 使用模式

| 模式 | images 数量 | referenceImages | 时长要求 | 模型要求 |
|------|------------|-----------------|----------|----------|
| 文生视频 | 0 | 可选 0-3 张* | 4/6/8秒 | 所有版本 |
| 图生视频 | 1 | 可选 0-3 张* | 4/6/8秒 | 所有版本 |
| 帧插值 | 2 | **不支持** | **仅8秒** | **仅 Veo 3.1** |

> **重要限制**：帧插值（2张images）和参考图片（referenceImages）功能互斥，不能同时使用。参考图片功能仅 Veo 3.1 支持。

## Create Video Generation Task

创建视频生成任务，返回 task_id 用于后续查询。

{% openapi src="../.gitbook/assets/openapi-veo.yaml" path="/v1/videos" method="post" %}
{% endopenapi %}

## Query Video Task Status

查询视频生成任务的状态和结果。建议轮询间隔 5 秒。

{% openapi src="../.gitbook/assets/openapi-veo.yaml" path="/v1/videos/{task_id}" method="get" %}
{% endopenapi %}
