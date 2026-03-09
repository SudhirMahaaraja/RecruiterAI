# RecruiterAI - Intelligent Hiring Platform

## Table of Contents
- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Usage Guide](#usage-guide)
- [Project Architecture](#project-architecture)
- [License](#license)

## Overview
RecruiterAI is a modern, AI-powered hiring platform designed to streamline the recruitment process. It drastically reduces time-to-hire by automating screening, assessments, and candidate stage management. Geared towards mid-market companies and SMBs, RecruiterAI bridges the gap between manual screening and optimal candidate selection using AI insights and an integrated candidate assessment pipeline.

## Key Features
- **Integrated Candidate Pipeline**: Seamlessly guides candidates through customized hiring stages: Quick Apply → MCQ → Coding → Behavioural → Tech/HR Rounds.
- **AI-Assisted Resume Screening**: Automatically parses and extracts crucial data from uploaded resumes (PDF/DOCX) using NLTK to evaluate candidate suitability early in the process.
- **Robust Assessment & Proctoring System**: 
  - Dynamic Coding and MCQ Assessment interfaces.
  - Camera-based AI proctoring utilizing YOLOv8 object detection to identify multiple people or unauthorized devices (e.g., cellphones) during tests. 
  - Real-time logging and auto-termination logic for severe violations.
- **Role-Based Workspaces**: 
  - *Candidate Dashboard*: Centralized portal for applicants to view their application status, undergo coding/MCQ tests, and review feedback.
  - *HR/Recruiter Dashboard*: A comprehensive overview where HR can track active jobs, evaluate candidates across interview stages, record internal notes, and schedule meetings.
- **Workflow Automation**: Built-in APScheduler handles background tasks effectively, easing the manual tracking workload.

## Technology Stack
- **Backend**: Python, Flask, Flask-Login
- **Database**: MongoDB (via PyMongo / Flask-PyMongo)
- **Computer Vision & AI**: Ultralytics (YOLOv8), OpenCV Headless (for proctoring), Scikit-learn
- **Natural Language Processing**: NLTK, PyPDF2, Document processing (python-docx)
- **Utilities**: APScheduler (Task scheduling), Werkzeug, Bcrypt (Password hashing)
- **Frontend**: HTML5, CSS3, JavaScript, Jinja2 Templates

## Installation & Setup

### Prerequisites
- Python 3.9 or higher
- MongoDB instance (Local or hosted, such as MongoDB Atlas)

### Local Environment Setup

1. **Clone the repository:**
   ```bash
   git clone <repository_url>
   cd "RecruiterAI-Intelligent-Hiring-Platform" # or the local directory name
   ```

2. **Set up a Virtual Environment (.venv):**
   *Note: Ensure packages are installed within a virtual environment per best practices.*
   ```bash
   python -m venv .venv
   
   # For Windows:
   .venv\Scripts\activate
   
   # For macOS/Linux:
   source .venv/bin/activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

## Configuration
Application specifications and secrets are managed via `config.py` and environment variables. Key variables include:
- `SECRET_KEY`: Important for Flask secure session management.
- `MONGO_URI`: Specify your valid MongoDB connection string.
- Application paths like `MODELS_FOLDER` and `UPLOAD_FOLDER` are automatically configured in `app.py`. Ensure required YOLO weights (e.g., `yolov8n.pt`) are downloaded to the models directory.

## Usage Guide
1. **Starting the Server:**
   Launch the web server by running the app entry point:
   ```bash
   python app.py
   ```
   Or via Flask CLI:
   ```bash
   flask run
   ```
   The application will become available at `http://127.0.0.1:5000/`.

2. **Accessing the Portals:**
   - **Public Page / Apply:** Access the index/home page `/` to browse openly available positions.
   - **Candidate Portal:** Log in as an applicant via `/candidate_login` to track application progress and complete rounds.
   - **HR Portal:** Access backend controls via `/hr_login`. (HR accounts are seeded automatically on first run if configured via `seed_data()` or can be created as directed).

3. **Assessments & Proctoring:**
   Once a candidate moves to the assessment phase, AI proctoring requests access to the user's camera (via `/detect_frame` endpoint) and continually maps predictions for process integrity.

## Project Architecture
```text
/
├── app.py                         # Core application file handling all routing and REST logic
├── config.py                      # Configurations and environmental variables
├── models/                        # Contains locally downloaded machine-learning weights (YOLO models)
├── static/                        # Static assets (Stylesheets, JS scripts, logos)
├── templates/                     # Comprehensive Jinja2 views (HR dashboards, Candidate flows)
├── uploads/                       # Secured directory for candidate resume storage
├── utils/                         # Helper modules and independent backend scripts
├── requirements.txt               # PyPI dependencies list
└── RecruiterAI_Business_Brief.txt # Documentation of business use-cases and ICP expectations
```

