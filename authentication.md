# Authentication

All ViralAPI endpoints require Bearer Token authentication.

## Getting Your API Key

1. Visit [https://viralapi.ai/api-key](https://viralapi.ai/api-key)
2. Sign in to your account
3. Create or copy your API Key

## Using the Token

Include the token in the `Authorization` header of every request:

```
Authorization: Bearer YOUR_API_KEY
```

Example:

```bash
curl -X POST https://viralapi.ai/v1/task/create \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer sk-xxxxxxxxxxxxxxxxxxxx" \
  -d '{"model": "gemini-2.5-flash-image", "task_type": "image", "input": {"prompt": "hello"}}'
```

## Error Responses

### 401 Unauthorized

Returned when the token is missing, malformed, or expired:

```json
{
  "error": {
    "code": 401,
    "message": "Invalid or expired token",
    "type": "authentication_error"
  }
}
```

### 402 Payment Required

Returned when your account balance is insufficient:

```json
{
  "error": {
    "code": 402,
    "message": "Insufficient account balance. Please top up at https://viralapi.ai/api-key",
    "type": "payment_required"
  }
}
```

### 403 Forbidden

Returned when your account lacks permission for the requested model:

```json
{
  "error": {
    "code": 403,
    "message": "Access denied for this model",
    "type": "permission_error",
    "param": "model"
  }
}
```

## Security Best Practices

- Never expose your API Key in client-side code or public repositories
- Use environment variables to store the key
- Rotate your key immediately if it is compromised
- Use separate keys for development and production environments
