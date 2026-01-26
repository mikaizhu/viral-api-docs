# Wan2.5 Image to Video

使用 `wan2.5-i2v-preview` 模型将图像转换为高质量动态视频。

## 模型特性

- 支持 480P/720P/1080P（默认 1080P），时长 5/10 秒（默认 5 秒）
- 默认生成有声视频（自动配音），支持自定义音频
- 支持单镜头和多镜头叙事

## 版本优势

相比 Wan2.2：更自然流畅的运动、更准确的控制、更高的整体质量

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础图生视频

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

### 复杂运动控制

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

## 图像要求

- **分辨率**: 360-2000 像素
- **文件大小**: ≤10MB
- **格式**: JPG, PNG, WebP
- **建议**: 使用清晰、构图良好的图像以获得最佳效果

## 重要说明

> **时长选项**: 可选 5 秒或 10 秒，默认 5 秒
> **有声视频**: 默认生成有声视频（自动配音），可通过 `audio_url` 自定义音频
> **提示词建议**: 具体描述运动方式和节奏，如"镜头缓慢向右平移，人物逐渐转身"
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
