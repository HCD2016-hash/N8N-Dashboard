# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-file HTML dashboard for monitoring N8N workflow executions in real-time. Displays execution status (success/error/running), allows filtering and searching, and links to detailed execution views in N8N.

## Development

This is a static HTML file with embedded CSS and JavaScript. No build tools, no dependencies.

**To run locally:** Open `index.html` in a browser, or serve with any static file server.

**To test:** Requires a running N8N instance accessible at the configured URL (`https://n8n-hcd.ngrok.dev`) and a valid N8N API key.

## Architecture

- **index.html** - Complete application: HTML structure, CSS styling, and vanilla JavaScript
- **N8N API Integration** - Uses `/api/v1/executions` endpoint with `X-N8N-API-KEY` header authentication
- **State Management** - API key stored in `localStorage` under `n8n_api_key`
- **Auto-refresh** - Polls every 30 seconds for updated execution data

## Configuration

The N8N base URL is hardcoded at line 405:
```javascript
const N8N_URL = 'https://n8n-hcd.ngrok.dev';
```

Change this to point to a different N8N instance.
