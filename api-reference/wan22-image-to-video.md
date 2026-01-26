# Wan2.2 Image to Video

使用 Wan2.2 图生视频模型将图像转换为动态视频。提供两个版本：

- **wan2.2-i2v-flash**: 快速版本，支持 480P/720P 分辨率
- **wan2.2-i2v-plus**: 增强版本，支持 480P/1080P 分辨率

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### Flash 版本示例（720P）

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

### Plus 版本示例（1080P）

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

## 图像要求

- **分辨率**: 360-2000 像素
- **文件大小**: ≤10MB
- **格式**: JPG, PNG, WebP
- **建议**: 使用清晰、构图良好的图像以获得最佳效果

## 重要说明

> **时长限制**: wan2.2 模型固定生成 5 秒视频，不可修改
> **提示词长度**: 最长 800 字符
> **音频支持**: wan2.2 模型不支持添加音频
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
> **提示词建议**: 描述画面的运动方式，而非重复描述图像内容
