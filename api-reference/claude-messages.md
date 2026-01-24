# Claude Native API

Claude 原生 API 接口，支持文本生成、多轮对话、图片理解等多模态能力。支持流式和非流式两种输出模式。

## Create Message

创建对话消息，支持文本、图片等多模态输入。通过 `stream` 参数控制是否流式输出。

> **Note**: 请求时必须包含 `anthropic-version: 2023-06-01` 请求头。

{% openapi src="../.gitbook/assets/openapi-claude.yaml" path="/v1/messages" method="post" %}
{% endopenapi %}
