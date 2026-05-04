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

1. **Clone the repository:**
cd gemini-youtube-automation


2. **Install dependencies:**
Make sure you have Python installed, then run:
pip install -r requirements.txt

## Usage

To run the application, execute the following command:
python main.py

This will initiate the content generation and upload process.
