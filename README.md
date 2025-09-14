
### Project name

FastAPI Gemini Story Generator[1]

### Overview

A minimal FastAPI service exposing POST /generate-story that sends a prompt to Google’s Gemini API and returns generated story text.[2]

### Prerequisites

- Python 3.9+ and a terminal/shell environment.[1]
- A valid Gemini API key with access to a text-capable model.[2]

### Installation

- Create and activate a virtual environment:  
  - macOS/Linux: python -m venv .venv && source .venv/bin/activate[1]
  - Windows (CMD): py -m venv .venv && .venv\Scripts\activate[1]
- Install dependencies: pip install -r requirements.txt[1]
- Set the API key as an environment variable (recommended):  
  - macOS/Linux: export GEMINI_API_KEY="YOUR_KEY"[2]
  - Windows (CMD): set GEMINI_API_KEY=YOUR_KEY[2]

### Configuration

- Update app.py to read the key from the environment and avoid hardcoding: os.getenv("GEMINI_API_KEY").[2]
- The default Gemini REST endpoint used is models.generateContent.[2]

### Run the server

- Development with Uvicorn: uvicorn app:app --reload --host 0.0.0.0 --port 8000[3][4]
- Once running, interactive docs are available at http://localhost:8000/docs.[1]

### Usage

- Endpoint: POST /generate-story[1]
- Request JSON:  
  { "prompt": "A child finds a magic backpack", "max_tokens": 400 }[2]
- Example curl:  
  curl -X POST http://localhost:8000/generate-story -H "Content-Type: application/json" -d '{"prompt":"A child finds a magic backpack","max_tokens":400}'[2]
- Example Python:  
  import requests; requests.post("http://localhost:8000/generate-story", json={"prompt":"A child finds a magic backpack","max_tokens":400})[2]

### Expected response

- Success: { "story": "<generated text>" }[2]
- Error: { "error": "<upstream error text>" }[2]

### Notes and best practices

- Do not commit API keys; use environment variables or a secret manager.[1][2]
- Prefer the latest Gemini “flash” or “pro” text model compatible with generateContent. Update model name if needed.[5][2]
- For longer outputs or better UX, consider streamGenerateContent.[2]
- In production, run behind a reverse proxy and tune request timeouts/retries.[6][1]

### Troubleshooting

- 401/403 from Gemini: verify GEMINI_API_KEY and model availability.[2]
- 404/405 locally: confirm uvicorn app:app and correct route path /generate-story.[3][1]
- Docs not loading: ensure server is running and visit /docs.[1]

