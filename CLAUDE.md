# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file HTML dashboard for monitoring N8N workflow executions in real-time. Designed to run as a **Missive iframe integration**. Displays execution status (success/error/running), allows filtering and searching, and links to detailed execution views in N8N.

## Development

This is a static HTML file with embedded CSS and JavaScript. No build tools, no dependencies.

**To run locally:** Must be served over HTTPS for Missive integration. Use ngrok or Caddy for local dev.

**To test in Missive:**
1. Serve via HTTPS (e.g., `ngrok http 8080`)
2. In Missive: Settings → Integrations → Add Custom Integration
3. Enter your HTTPS URL

## Architecture

- **index.html** - Complete application: HTML structure, CSS styling, and vanilla JavaScript
- **Missive Integration** - Uses `missive.js` library for iframe-compatible forms and storage
- **N8N API Integration** - Uses `/api/v1/executions` endpoint with `X-N8N-API-KEY` header authentication
- **State Management** - API key stored via `Missive.storeGet/storeSet` (persists per-user, clears on logout)
- **Auto-refresh** - Polls every 30 seconds for updated execution data

## Missive API Usage

| Function | Purpose |
|----------|---------|
| `Missive.storeGet('n8n_api_key')` | Retrieve stored API key |
| `Missive.storeSet('n8n_api_key', value)` | Save API key (use `null` to clear) |
| `Missive.openForm({...})` | Show popup forms (replaces `prompt()`/`confirm()`) |

**Why not localStorage/prompt()?** - These are blocked in iframe contexts for security.

## Configuration

The N8N base URL is hardcoded at line 408:
```javascript
const N8N_URL = 'https://n8n-hcd.ngrok.dev';
```

Change this to point to a different N8N instance.
