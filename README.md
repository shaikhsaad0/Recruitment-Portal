# CareerNest — Recruitment and Job Application Portal

A full-stack recruitment portal built with Python, Django, SQLite, HTML, CSS, and Bootstrap 5. This project is designed as a learning/internship assignment starter and runs locally without a separate database server. The source files are included in the ZIP; run the setup steps below on your computer.

## Features

- Candidate registration, login, and logout
- Django staff/admin login and role-based admin pages
- Job creation, editing, activation/deactivation, and deletion
- Public job listings, keyword search, and employment-type filtering
- Job details and application submission
- CV upload with extension and 5 MB size validation (PDF, DOC, DOCX)
- Prevents a candidate from applying twice to the same job
- Candidate application history and status tracking
- Admin application search, status filtering, CV access, and status updates
- Admin dashboard statistics for jobs, candidates, and application statuses
- Responsive Bootstrap-based layout
- Sample job listings and demo accounts
- Basic automated tests

## Requirements

- Python 3.10 or newer (Python 3.12/3.13 recommended)
- pip
- Internet connection on first page load for Bootstrap CDN (the app's core backend runs locally)

## Setup on Windows

Open the project folder in VS Code, then use the terminal.

### 1. Create and activate a virtual environment

```powershell
python -m venv venv
venv\Scripts\activate
```

If PowerShell blocks activation, use Command Prompt or run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\venv\Scripts\Activate.ps1
```

### 2. Install dependencies

```powershell
python -m pip install -r requirements.txt
```

### 3. Create database tables

```powershell
python manage.py migrate
```

### 4. Add demo users and sample jobs

```powershell
python manage.py seed_demo
```

Demo credentials:

- **Admin:** `portaladmin` / `AdminDemo123!`
- **Candidate:** `candidate` / `CandidateDemo123!`

These credentials are for local demonstration only. Change them before any deployment.

### 5. Start the development server

```powershell
python manage.py runserver
```

Open http://127.0.0.1:8000/

## Admin features

Sign in using the demo admin account. The dashboard has shortcuts for job management and applications. The separate Django administration interface is available at http://127.0.0.1:8000/django-admin/.

## Candidate flow

1. Register a candidate account or sign in with the demo candidate.
2. Browse and search job listings.
3. Open a job and select Apply.
4. Upload a PDF/DOC/DOCX CV (up to 5 MB).
5. Track application status under My applications.

## Run tests

```powershell
python manage.py test
```

## GitHub submission

Create a new empty GitHub repository, then run these commands from this project folder:

```powershell
git init
git add .
git commit -m "Build CareerNest recruitment portal"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

Replace the remote URL with your own repository URL. Do not commit your real CVs, production secrets, or a production database.

## Important notes before deployment

This is a development-ready assignment project, not a hardened production deployment. Before deploying:
- Set `DEBUG = False` and configure `ALLOWED_HOSTS`
- Move `SECRET_KEY` into an environment variable
- Configure HTTPS, secure cookies, and a production server
- Use managed/static media storage and restrict access to CV files
- Add malware scanning and stronger file-content validation for uploaded documents
- Review privacy, retention, backups, and access rules for candidate data
- Configure static-file collection and a production database if needed

## Main project structure

```text
config/                  Django project settings and URL configuration
jobs/models.py            Job and Application database models
jobs/forms.py             Registration, job, CV, and status forms
jobs/views.py              Public, candidate, and admin views
jobs/urls.py               URL routes
jobs/admin.py              Django admin configuration
jobs/management/commands/seed_demo.py
templates/                 HTML templates
static/css/style.css       Responsive custom styling
media/cvs/                 Uploaded CVs (created at runtime)
requirements.txt
```

## Database relationships

- A `Job` can have many `Application` records.
- A candidate (`User`) can have many `Application` records.
- Each application belongs to exactly one candidate and one job.
- A unique database constraint prevents duplicate candidate/job applications.
