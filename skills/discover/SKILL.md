---
description: "Discover APIs from the Postman API Network using Orbit's agent-friendly search. Returns endpoints with evaluateGuide fields showing what each API can and can't do."
allowed-tools: ["Bash", "Write", "Read"]
---

# orbit:discover

Search the Postman API Network for APIs matching a capability query.

## Input

A capability description — what you need the API to do.
Multiple capabilities: comma-separated or as separate arguments.

## Steps

1. Read `references/orbit-api.md` for the API contract.
2. For each capability query, POST to the Orbit search endpoint using curl.
3. Parse the JSON response. For each result, extract:
   - `name`, `method`, `url`
   - `evaluateGuide` — the agent-oriented breakdown of what the endpoint does, what it's good for, and what it doesn't support
4. Format results as a readable markdown table or list grouped by capability.
5. Save output to `orbit-output/<slugified-query>.md`.
6. Present a summary to the user highlighting the top matches and their evaluateGuide insights.

## Output format

For each API result:

```
### <name>
- **Method:** <method>
- **URL:** <url>
- **Evaluate Guide:** <evaluateGuide summary>
```

Group results under `## <capability query>` headings when multiple queries are run.

## Notes

- If a query returns zero results, say so — don't fabricate endpoints.
- The `evaluateGuide` field is the key value: it tells you what an API is good for and what it can't do, saving trial-and-error.
- Orbit is designed for agent consumption (compact payloads, structured guidance) vs human browsing on the Postman API Network website.
