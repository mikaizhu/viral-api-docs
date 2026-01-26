# Wan2.2 Image to Video

使用 `wan2.2-i2v` 模型将图像转换为动态视频。

## 模型特性

- **图像驱动**: 以图像作为首帧，生成连贯的视频内容
- **运动控制**: 通过文本提示词控制画面运动方式
- **高质量输出**: 支持最高 1080P 分辨率
- **灵活时长**: 支持 2-15 秒的视频生成

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础图生视频

```json
{
  "model": "wan2.2-i2v",
  "task_type": "video",
  "input": {
    "prompt": "Camera slowly zooms in on the mountain peak",
    "img_url": "https://example.com/first-frame.jpg",
    "resolution": "720P",
    "duration": 5
  }
}
```

### 带自定义音频

```json
{
  "model": "wan2.2-i2v",
  "task_type": "video",
  "input": {
    "prompt": "The scene comes alive with gentle movement",
    "img_url": "https://example.com/scene.jpg",
    "audio_url": "https://example.com/background-music.mp3",
    "resolution": "1080P",
    "duration": 8
  }
}
```

## 图像要求

- **分辨率**: 360-2000 像素
- **文件大小**: ≤10MB
- **格式**: JPG, PNG, WebP
- **建议**: 使用清晰、构图良好的图像以获得最佳效果

## 重要说明

> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
> **提示词建议**: 描述画面的运动方式，而非重复描述图像内容
