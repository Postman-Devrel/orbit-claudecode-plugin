# Orbit Claude Code Plugin

Discover APIs from the [Postman API Network](https://www.postman.com/explore) using Postman Orbit -- an agent-friendly search API designed for AI-powered app design.

## What is Orbit?

Orbit is Postman's API discovery service built specifically for AI agent consumption. Unlike browsing the Postman API Network in a browser, Orbit returns compact, structured payloads with `evaluateGuide` fields that tell agents exactly what each API endpoint can and can't do. This lets agents make integration decisions without trial-and-error.

## Install

```bash
claude plugin add Postman-Devrel/orbit-claudecode-plugin
```

## Usage

```
/orbit:discover payment processing for subscriptions
```

Search for multiple capabilities at once:

```
/orbit:discover send transactional email, geocode addresses, payment processing
```

## What you get

For each matching API, Orbit returns:

- **Name** and **description** of the endpoint
- **Method** and **URL** for the API call
- **evaluateGuide** -- structured guidance covering:
  - What the endpoint does
  - What it's best used for
  - What it does not support

Results are saved to `orbit-output/` as markdown files for reference.

## Design process

Orbit works best when you use it at the start of a project to build an API blueprint before writing code. Here's the workflow:

1. **Describe what you're building.** Tell your agent the app you want to create, including the key capabilities it needs (payments, auth, email, etc.). You don't need to know which APIs exist yet.

2. **Let the agent query Orbit.** The agent breaks your description into capability queries, hits the Orbit API for each one, and returns candidate endpoints with their evaluateGuide breakdowns.

3. **Read the gaps.** The evaluateGuide's "Not supported" lines are the most valuable part. They tell you what each API can't do, so you can identify missing capabilities before you've written any integration code.

4. **Iterate.** Use those gaps as your next round of queries. "Find me APIs that handle payment refunds" or "I need an auth provider that supports token refresh." Each round narrows the design.

5. **Save the blueprint.** The agent saves results to `orbit-output/` as a structured file you can reference throughout the project. This becomes your API design document, readable by both humans and agents.

The goal is to make API selection decisions intentionally at design time, not discover limitations mid-sprint after you've already integrated half the stack.

## Orbit vs postman:search

| | Orbit (`orbit:discover`) | Postman Search (`postman:search`) |
|---|---|---|
| **Designed for** | AI agents | Human browsing |
| **Payloads** | Compact, structured | Rich, detailed |
| **evaluateGuide** | Yes -- agent decision support | No |
| **Best when** | Starting a project, need to find APIs for capabilities | Exploring collections, workspaces, documentation |

## Links

- [Postman API Network](https://www.postman.com/explore)
- [Claude Code Plugins](https://docs.anthropic.com/en/docs/claude-code/plugins)
