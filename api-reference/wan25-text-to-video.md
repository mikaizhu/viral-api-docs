# Wan2.5 Text to Video

使用 `wan2.5-t2v` 模型将文本描述转换为高质量视频。

## 模型特性

- **增强的文本理解**: 更准确地理解复杂的文本描述
- **智能改写**: 支持 `prompt_extend` 功能，自动优化提示词
- **高质量输出**: 更流畅的动作和更自然的画面过渡
- **灵活分辨率**: 支持 720P/1080P，横屏/竖屏
- **时长可控**: 支持 2-15 秒的视频生成

## 版本优势

相比 Wan2.2，Wan2.5 提供：
- ✅ 更高的视频质量和流畅度
- ✅ 更准确的文本理解
- ✅ 支持智能提示词改写
- ✅ 更自然的动作和过渡效果

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础文生视频

```json
{
  "model": "wan2.5-t2v",
  "task_type": "video",
  "input": {
    "prompt": "A futuristic city with flying cars and neon lights",
    "size": "1280*720",
    "duration": 5
  }
}
```

### 启用智能改写

```json
{
  "model": "wan2.5-t2v",
  "task_type": "video",
  "input": {
    "prompt": "A peaceful garden in spring",
    "size": "1920*1080",
    "duration": 8,
    "prompt_extend": true
  }
}
```

## 重要说明

> **智能改写**: 启用 `prompt_extend: true` 可以让模型自动优化你的提示词，提升生成效果
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
