# Automated LLM Code Deployment API (FastAPI)

## Overview

This project implements a robust, fully automated backend for code generation, deployment, and evaluation using Large Language Models (LLMs) and GitHub. Users submit structured tasks via API; the service generates application code, saves and manages attachments, creates/manages GitHub repos, enables GitHub Pages, and notifies an external evaluator.

- **Stack:** FastAPI, Gemini API, GitHub API, httpx, GitPython, Pydantic
- **Workflow:** Receives POSTed tasks, validates secrets, orchestrates code generation and deployment in background tasks with heartbeat/status endpoints.

## Key Features

- **/ready**: Main POST endpoint for submitting tasks (with attachments and metadata).
- **Automated LLM Generation:** Integrates Gemini API for code and document generation, with minimal/surgical update capability for subsequent task rounds.
- **GitHub Integration:** Creates public repos, commits generated code, manages LICENSE/README, enables Pages hosting and pushes updates.
- **Attachment Management:** Securely receives, saves, and references image/file attachments as required by task briefs.
- **Evaluator Notification:** Reports repository and deployment status (with commit info) to an external system.

## Usage

1. **Start the service** as a Docker container or on Hugging Face Spaces.
2. **Send a POST request** to `/ready` with JSON body:

- The endpoint responds immediately (“ready”), and processes in background.

## Endpoints

- `POST /ready` — Submit deployment/evaluation task.
- `GET /status` — Check last received task and processing state.
- `GET /health` — Service heartbeat.
- `GET /logs?lines=N` — View last N lines of log file.

## Configuration

- Set environment variables for API keys/secrets: `GEMINI_API_KEY`, `GITHUB_TOKEN`, `GITHUB_USERNAME`, `STUDENT_SECRET`—configure via `.env` or Hugging Face Spaces Variables.
- All logs are stored at `logs/app.log`.

## Deployment

- **Hugging Face Spaces:** Upload all source files and Dockerfile, set env secrets in Space Variables.
- **GitHub Repo:** All code and generated files are committed and pushed automatically; GitHub Pages is enabled for repo-based app hosting.

## License

Distributed under the MIT License. Full license text is in `LICENSE`.

---

