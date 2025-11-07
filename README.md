# EmailDrafter

AI-assisted email drafting app with a Python backend and a modern React + Vite + Tailwind frontend.

> This README is tailored to the current repository layout you shared. If your backend framework or ports differ, adjust the run commands accordingly.

## Overview

EmailDrafter helps you draft better emails faster. The frontend provides a clean UI for inputting context and seeing generated drafts. The backend exposes an API endpoint(s) to generate or refine email content.

## Tech Stack

- Frontend: React (Vite) + Tailwind CSS
- Backend: Python (framework defined in `backend/main.py`)
- Package managers: npm (frontend), pip (backend)

## Monorepo layout

```
EmailDrafter/
  backend/
    main.py
    requirements.txt
  frontend/
    my-app/
      package.json
      src/
        api.js
        App.jsx
        EmailDrafter.jsx
        ...
```

## Features

- Draft emails from prompts/context (tone/length/role are common controls)
- Live preview and editing before copy/send
- Simple API wrapper in `frontend/my-app/src/api.js`
- Developer-friendly: hot reload (Vite) and optional backend auto-reload

## Getting started (Windows / PowerShell)

### Prerequisites

- Node.js 18+ (LTS recommended)
- Python 3.9+ (3.10+ recommended)
- PowerShell (you are already using it)

### 1) Backend setup

```powershell
# From repo root
cd backend

# Create & activate virtual environment
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# Install dependencies
pip install -r requirements.txt

# Start the backend (choose the command that matches your framework)
# FastAPI (uvicorn):
# uvicorn main:app --reload --port 8000

# Flask:
# $env:FLASK_APP = "main.py"; flask run --port 8000

# Plain Python script (if main.py starts the server on its own):
# python .\main.py
```

Notes:
- Adjust the port if your app uses a different one.
- If CORS errors occur when opening the frontend, enable CORS in your backend or align ports.

### 2) Frontend setup

```powershell
# In a separate terminal (or background), from repo root
cd frontend\my-app

# Install dependencies
npm install

# Start dev server
npm run dev
```

Vite will print a local URL (typically http://localhost:5173).

If your backend runs on http://localhost:8000, ensure the frontend points to it. See `frontend/my-app/src/api.js` for base URL configuration.

## Configuration

- Frontend API base URL: check and edit `frontend/my-app/src/api.js`.
- Backend environment variables: check how `backend/main.py` reads configuration. Common patterns include:
  - `OPENAI_API_KEY` or similar (if using LLMs)
  - `PORT` or `HOST`

If you use environment variables, you can create a `.env` (not committed) and load it using your framework or `python-dotenv`.

### Example `.env` (if applicable)

```
# Backend
OPENAI_API_KEY=your_key_here
PORT=8000
```

## API (high level)

See `frontend/my-app/src/api.js` for the exact endpoints used. Typical patterns:

- POST `/api/draft`
  - Request JSON: `{ "prompt": string, "tone"?: string, "length"?: string }`
  - Response JSON: `{ "draft": string }`

- POST `/api/refine`
  - Request JSON: `{ "draft": string, "instructions": string }`
  - Response JSON: `{ "draft": string }`

If your routes differ, update this section and `api.js` accordingly.

## Scripts reference

Frontend (`frontend/my-app/package.json` typically includes):
- `npm run dev` – Start Vite dev server
- `npm run build` – Production build
- `npm run preview` – Preview production build locally
- `npm run lint` – Lint (if configured)

Backend:
- See the commands listed in the backend setup section; your exact command depends on the framework (FastAPI/Flask/custom).

## Development tips

- Keep backend and frontend in separate terminals for hot reload.
- If you change the backend port, reflect it in `src/api.js`.
- CORS: if the frontend cannot reach the backend due to CORS, enable CORS middleware (e.g., `fastapi.middleware.cors` or `flask-cors`).

## Troubleshooting

- Backend not reachable
  - Verify the server is running and note the port in your terminal output.
  - Update `src/api.js` base URL to match.
- CORS error in browser console
  - Enable CORS in backend or run both services on the same origin via a proxy.
- Vite dev server boots but shows a blank page
  - Check browser console for errors.
  - Ensure dependencies installed successfully (`npm install`).
- Python dependency issues
  - Verify the virtual environment is activated before `pip install` and running.

## Folder details

- `backend/` – Python app entrypoint (`main.py`) and `requirements.txt`.
- `frontend/my-app/` – React app (Vite). Key files:
  - `src/EmailDrafter.jsx` – main drafting UI
  - `src/api.js` – API calls
  - `vite.config.js` – Vite configuration
  - `tailwind.config.js` – Tailwind configuration

## Roadmap (examples)

- Prompt templates & presets
- Draft history and local storage
- Multi-language support
- Tone & style sliders
- Export to HTML/Markdown

## Contributing

Issues and pull requests are welcome. If proposing significant changes, please open an issue first to discuss what you’d like to change.

## License

No license specified. If you intend to open source, consider adding an OSS license (e.g., MIT) at the repo root as `LICENSE`.
