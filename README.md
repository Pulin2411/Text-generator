# Story Generator API (FastAPI + Gemini)

Lightweight FastAPI service that forwards a user prompt to Gogle Gemini (Generative Language API) and returns a creative story.  
This repository contains a minimal example implementation and instructions to run locally or in a container.

## Contents

- `app.py` — FastAPI application with a `/generate-story` POST endpoint. :contentReference[oaicite:2]{index=2}
- `requirements.txt` — Python dependencies. :contentReference[oaicite:3]{index=3}

## Features

- Single POST endpoint: `/generate-story`
- Forwards prompts to Google Gemini (Generative Language API)
- Returns generated story text or error response

## API

### POST /generate-story

**Request JSON**
```json
{
  "prompt": "A prompt for the story",
  "max_tokens": 500
}

---

# Flow chart (process-level)

Use this Mermaid flow chart to show the request flow. Paste into your README or GitHub file — GitHub supports Mermaid rendering.

```mermaid
flowchart TD
  A[Client] -->|POST /generate-story| B[FastAPI (app.py)]
  B --> C{Validate request}
  C -->|invalid| D[400 Bad Request]
  C -->|valid| E[Prepare payload for Gemini]
  E --> F[Google Gemini REST API]
  F -->|200 / story| G[Parse response]
  G --> H[Return JSON { "story": ... }]
  F -->|error| I[Return error to client]
