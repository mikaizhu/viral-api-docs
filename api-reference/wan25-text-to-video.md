# Wan2.5 Text to Video

使用 `wan2.5-t2v-preview` 模型将文本描述转换为高质量视频。

## 模型特性

- 支持 5/10 秒时长（默认 5 秒），默认分辨率 1920*1080（1080P）
- 提示词最长 1500 字符，支持智能改写（`prompt_extend`）
- 默认生成有声视频（自动配音），支持自定义音频

## 版本优势

相比 Wan2.2：更高质量、支持智能改写、可选时长、有声视频

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础文生视频

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

### 启用智能改写

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

## 重要说明

> **智能改写**: 启用 `prompt_extend: true` 可以让模型自动优化你的提示词，提升生成效果
> **时长选项**: 可选 5 秒或 10 秒，默认 5 秒
> **有声视频**: 默认生成有声视频（自动配音），可通过 `audio_url` 自定义音频
> **提示词长度**: 最长 1500 字符
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
