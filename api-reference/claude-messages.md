# Claude Native API

Claude Native API supports text generation, multi-turn conversations, image understanding, and multimodal capabilities. Supports both streaming and non-streaming output modes.

## Create Message

Create conversation messages with text, images, and multimodal inputs. Control streaming output via the `stream` parameter.

> **Note**: Requests must include the `anthropic-version: 2023-06-01` header.

{% openapi src="../.gitbook/assets/openapi-claude.yaml" path="/v1/messages" method="post" %}
{% endopenapi %}
