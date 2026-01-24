# Gemini Native API

Gemini 原生 API 接口，支持文本生成、多轮对话、图片理解、PDF 分析等多模态能力。

## Generate Content

Non-streaming content generation that returns the complete response at once.

{% openapi src="../.gitbook/assets/openapi-gemini.yaml" path="/v1beta/models/{model}:generateContent" method="post" %}
{% endopenapi %}

## Stream Generate Content

Streaming content generation using SSE (Server-Sent Events). Returns partial responses progressively.

> **Note**: Remember to add `?alt=sse` query parameter to enable streaming output.

{% openapi src="../.gitbook/assets/openapi-gemini.yaml" path="/v1beta/models/{model}:streamGenerateContent" method="post" %}
{% endopenapi %}
