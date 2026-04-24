# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is an API documentation repository for Unmade's public partner integration API. Documentation is written in [API Blueprint](https://apiblueprint.org/) format (`.apib` files) and rendered to HTML using the [Blueprinter](https://github.com/funbox/blueprinter) Docker image.

## Local Development

Requires Docker. Serves with live-reload at http://localhost:3000/

```bash
# V1 API docs
docker-compose up dev

# V2 API docs
docker-compose up dev-v2
```

## Building

```bash
# Generate index.html from V1 spec
docker-compose up render

# Generate v2.html from V2 spec
docker-compose up render-v2
```

## Deployment

Pushing to `main` triggers a GitHub Actions workflow (`.github/workflows/deploy.yml`) that builds both V1 and V2 docs and deploys to GitHub Pages. Published assets at https://engineering.unmade.com/api-docs/:

- `index.html` — rendered V1 docs
- `v2.html` — rendered V2 docs
- `apiary.apib` — raw V1 spec
- `apiary_v2.apib` — raw V2 spec
- `llms.txt` — LLM-friendly entry point

## Architecture

### Files

- `apiary.apib` — V1 API specification
- `apiary_v2.apib` — V2 API specification (superset of V1, all endpoints at `/v2/`)
- `llms.txt` — LLM-friendly summary of both API versions; deployed to GitHub Pages alongside the rendered docs

### API Blueprint Format

```
FORMAT: 1A
HOST: https://partner-subdomain.embed.unmade.com/

# Group Name

## Endpoint Name [/v2/path/{id}]

### Action Description [GET]

+ Request (application/json)
    + Headers
            Authorization: Token ABCDEF
    + Body

            { "field": "value" }

+ Response 200 (application/json)
    + Body

            { "response": "data" }
```

Indentation in `.apib` files uses 4 spaces (enforced by `.editorconfig`).

### API Versions

**Prefer V2 for all new work.** V1 is for historical context is deprecated.

**V1** covers: Editor iframe integration, Design API, Transfer Preview API, Roster API, Orders API, Factory API.

**V2** adds/changes: 3D design view (`/v2/designs/{id}/3d/`), partner data endpoints on orders, shipping address retrieval, order items pagination, enhanced job states, materials data, and an Ecommerce Orders API (replaces V1 Orders API).

### Internal Links

Use relative URLs for internal links between sections (not absolute `#anchor` links), as established in recent commits.
