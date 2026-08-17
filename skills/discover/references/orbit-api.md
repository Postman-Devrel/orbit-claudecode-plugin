# Orbit API Reference

## Endpoint

```
POST https://fabric-gateway.postmanlabs.com/api/search
Content-Type: application/json
```

## Request

```json
{
  "q": "your search query"
}
```

The query should describe the capability you need — e.g., "payment processing for subscriptions", "send transactional email", "geocoding addresses".

## Example curl

```bash
curl -s -X POST https://fabric-gateway.postmanlabs.com/api/search \
  -H "Content-Type: application/json" \
  -d '{"q": "payment processing"}' | jq .
```

## Response schema

```json
{
  "data": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "method": "GET | POST | PUT | PATCH | DELETE",
      "url": "string (the API endpoint URL)",
      "evaluateGuide": "string (agent-oriented usage guidance)"
    }
  ],
  "meta": {
    "q": "string (echo of search query)",
    "total": "number (total matching results)",
    "nextCursor": "string | null (pagination cursor)"
  }
}
```

## Field descriptions

| Field | Description |
|-------|-------------|
| `id` | Unique identifier for the API endpoint |
| `name` | Human-readable name of the endpoint |
| `description` | Brief description of what the endpoint does |
| `method` | HTTP method (GET, POST, PUT, PATCH, DELETE) |
| `url` | The API endpoint URL |
| `evaluateGuide` | Agent-oriented guidance — what the endpoint does, what it's good for ("Use for"), and what it can't do ("Not supported"). This is the key differentiator for AI agent consumption |

## The evaluateGuide field

The `evaluateGuide` is what makes Orbit results agent-friendly. It provides structured guidance so an AI agent can quickly decide whether an API fits its needs without trial-and-error:

- **What it does** — a concise description of the endpoint's purpose
- **Use for** — specific scenarios where this endpoint is the right choice
- **Not supported** — capabilities this endpoint does not cover, preventing wasted integration effort

## Pagination

When `meta.nextCursor` is non-null, pass it as `"cursor"` in the next request body to fetch more results:

```json
{
  "q": "payment processing",
  "cursor": "value-from-nextCursor"
}
```
