# Stream Generate Content

Streaming content generation using SSE (Server-Sent Events). Returns partial responses progressively, ideal for real-time user experience with long-form content generation.

> **Note**: Remember to add `?alt=sse` query parameter to enable streaming output.

{% openapi src="../openapi-gemini.yaml" path="/v1beta/models/{model}:streamGenerateContent" method="post" %}
{% endopenapi %}
