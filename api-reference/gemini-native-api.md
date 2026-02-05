# Gemini Native API

Gemini Native API supports text generation, multi-turn conversations, image understanding, PDF analysis, and multimodal capabilities.

## Generate Content

Non-streaming content generation that returns the complete response at once.

{% openapi src="../.gitbook/assets/openapi-gemini.yaml" path="/v1beta/models/{model}:generateContent" method="post" %}
{% endopenapi %}

## Stream Generate Content

Streaming content generation using SSE (Server-Sent Events). Returns partial responses progressively.

> **Note**: Remember to add `?alt=sse` query parameter to enable streaming output.

{% openapi src="../.gitbook/assets/openapi-gemini.yaml" path="/v1beta/models/{model}:streamGenerateContent" method="post" %}
{% endopenapi %}
