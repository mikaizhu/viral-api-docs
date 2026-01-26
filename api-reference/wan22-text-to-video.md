# Wan2.2 Text to Video

使用 `wan2.2-t2v-plus` 模型将文本描述转换为视频。

## API 端点

{% openapi src="../.gitbook/assets/openapi-tongyi-wanxiang.yaml" path="/v1/task/create" method="post" %}
{% endopenapi %}

## 使用示例

### 基础文生视频

```json
{
  "model": "wan2.2-t2v-plus",
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
  "model": "wan2.2-t2v-plus",
  "task_type": "video",
  "input": {
    "prompt": "A futuristic city with flying cars",
    "negative_prompt": "blurry, low quality",
    "size": "1920*1080",
    "duration": 5
  }
}
```

## 重要说明

> **时长限制**: wan2.2-t2v-plus 固定生成 5 秒视频，不可修改
> **提示词长度**: 最长 800 字符
> **音频支持**: wan2.2 模型不支持添加音频
> **处理时间**: 通常 1-5 分钟
> **视频有效期**: 24 小时，请及时下载
