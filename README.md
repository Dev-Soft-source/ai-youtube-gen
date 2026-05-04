# Gemini YouTube Automation

The project includes a GitHub Actions workflow that runs daily at 7:00 AM UTC. It:
- Generates lesson scripts using Gemini.
- Produces long-form and short YouTube videos.
- Uploads them automatically with appropriate thumbnails and metadata.

## Project Structure
```text
gemini-youtube-automation/
├── .github/
│   └── workflows/
│       └── main.yml         # GitHub Actions workflow configuration
├── src/                     # Source directory for Python modules
│   ├── init.py          # Initializes the 'src' package
│   ├── generator.py         # Code for generating content and video
│   └── uploader.py          # Code for uploading to YouTube
├── .gitignore               # Files and directories to ignore in version control
├── content_plan.json        # Contains topics for moving forward.
├── main.py                  # Main entry point to run the application
└── requirements.txt         # List of Python packages needed
```

## Setup Instructions

1. **Clone the repository** and open a terminal in the project root (the folder that contains `main.py`).

2. **Install dependencies** (Python 3 recommended):
   ```bash
   pip install -r requirements.txt
   ```

3. **Environment variables**
   - **`GOOGLE_API_KEY`** (required): Google AI / Gemini API key.
   - **`PEXELS_API_KEY`** (optional): If unset, slide backgrounds fall back to solid colors.

4. **YouTube upload (local)**
   - Create a YouTube Data API OAuth **Desktop app** client in Google Cloud and download the JSON as `client_secrets.json` in the project root.
   - On the first run, the app opens a browser to complete OAuth and writes `credentials.json` for later runs.

## Execution methods

### Run locally

From the project root, with `GOOGLE_API_KEY` set (and optionally `PEXELS_API_KEY`):

```bash
python main.py
```

On Windows, if `python` is not on your PATH, try `py main.py`.

This loads or creates `content_plan.json`, produces up to one pending lesson (long + short video), uploads to YouTube, updates lesson status, and writes artifacts under `output/`. Ensure [FFmpeg](https://ffmpeg.org/) is available if MoviePy or audio conversion fails on your system.

### Run on GitHub Actions (scheduled)

The repo is intended to run on a **daily schedule** (for example **7:00 AM UTC**) via a workflow under `.github/workflows/` (for example `main.yml`). Typical setup:

1. Add **repository secrets** for `GOOGLE_API_KEY` and, if you use stock imagery, `PEXELS_API_KEY`.
2. Provide **YouTube credentials** in CI the same way your workflow expects (for example writing `client_secrets.json` and/or `credentials.json` from secrets before `python main.py`), so `src/uploader.py` can refresh tokens non-interactively.
3. Push to the branch your workflow uses (usually `main`); use **Actions → Run workflow** if the workflow defines `workflow_dispatch` for manual runs.

Adjust steps to match your actual workflow file once it is committed.
