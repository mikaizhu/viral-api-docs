# NanoBanana Image Edit

Edit existing images based on text instructions using the `gemini-2.5-flash-image` model.

> **Note**: The actual API endpoint is `POST /v1/task/create`. Providing `image_urls` in the input switches to image editing mode.

{% openapi src="../openapi-nanobanana.yaml" path="/v1/task/create-image-edit" method="post" %}
{% endopenapi %}
