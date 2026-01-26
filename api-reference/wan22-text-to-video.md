# Wan2.2 Text to Video

使用 `wan2.2-t2v` 模型将文本描述转换为视频。

## 模型特性

- **文本驱动**: 仅需文本描述即可生成视频
- **灵活分辨率**: 支持 720P/1080P，横屏/竖屏
- **时长可控**: 支持 2-15 秒的视频生成
- **镜头控制**: 支持单镜头和多镜头叙事

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础文生视频

```json
{
  "model": "wan2.2-t2v",
  "task_type": "video",
  "input": {
    "prompt": "A serene mountain landscape at sunset with flowing clouds",
    "size": "1280*720",
    "duration": 5
  }
}
```

### 带反向提示词

```json
{
  "model": "wan2.2-t2v",
  "task_type": "video",
  "input": {
    "prompt": "A futuristic city with flying cars",
    "negative_prompt": "blurry, low quality",
    "size": "1920*1080",
    "duration": 8
  }
}
```

## 重要说明

> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
> **计费方式**: 按成功生成的视频秒数计费
