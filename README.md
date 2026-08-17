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
