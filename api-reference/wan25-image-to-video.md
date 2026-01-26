# Wan2.5 Image to Video

使用 `wan2.5-i2v` 模型将图像转换为高质量动态视频。

## 模型特性

- **增强的运动理解**: 更准确地理解和执行运动指令
- **自然的动作**: 更流畅、更符合物理规律的画面运动
- **高质量输出**: 支持最高 1080P 分辨率
- **灵活时长**: 支持 2-15 秒的视频生成
- **镜头控制**: 支持单镜头和多镜头叙事

## 版本优势

相比 Wan2.2，Wan2.5 提供：
- ✅ 更自然流畅的运动效果
- ✅ 更准确的运动控制
- ✅ 更好的画面连贯性
- ✅ 更高的整体视频质量

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础图生视频

```json
{
  "model": "wan2.5-i2v",
  "task_type": "video",
  "input": {
    "prompt": "The city comes alive with movement and energy",
    "img_url": "https://example.com/city-scene.jpg",
    "resolution": "720P",
    "duration": 5
  }
}
```

### 复杂运动控制

```json
{
  "model": "wan2.5-i2v",
  "task_type": "video",
  "input": {
    "prompt": "Camera slowly pans right while the character turns and smiles",
    "img_url": "https://example.com/portrait.jpg",
    "resolution": "1080P",
    "duration": 8,
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

> **提示词建议**: 具体描述运动方式和节奏，如"镜头缓慢向右平移，人物逐渐转身"
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
