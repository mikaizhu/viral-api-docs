# NanoBanana Pro Image Edit

Edit existing images with high quality using the `gemini-3-pro-image-preview` model. Supports 1K/2K/4K resolution.

> **Note**: The actual API endpoint is `POST /v1/task/create`. Providing `image_urls` in the input switches to image editing mode.

{% openapi src="../.gitbook/assets/openapi-nanobanana-pro.yaml" path="/v1/task/create-image-edit" method="post" %}
[openapi-nanobanana-pro.yaml](../.gitbook/assets/openapi-nanobanana-pro.yaml)
{% endopenapi %}
