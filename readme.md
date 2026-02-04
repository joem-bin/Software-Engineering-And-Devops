# Flask Helpdesk Ticketing App

## Overview

A Flask-based web application for submitting, managing, and resolving support tickets. Built with SQLite, modularized logic, GOV.UK styling, integrated logging, security scanning, and CI automation.
<br>
<br>

## Live Demo

This project is deployed and live on Render:  
[https://it-ticket-system-joe-m.onrender.com/dashboard]

Note: It may take a few seconds to wake up after inactivity (free-tier cold start).

<br>
<br>



# Setup Instructions



## 1. **Clone the repository:**

```bash
git clone https://github.com/joem-bin/Agile-project.git
cd your-repo
```
<br>
<br>

## 2. **Create and activate a virtual environment:**

- **Windows:**

```bash
python -m venv .venv
source .venv/Scripts/activate
```

- **macOS/Linux:**

```bash
python -m venv .venv
source .venv/bin/activate
```
<br>
<br>

## 3. **Install dependencies:**

```bash
pip install -r requirements.txt
```
<br>
<br>

## 4. **Set environment variables:**

Create a `.env` file in the project root. Here's a safe example:

```
FLASK_ENV=development
SECRET_KEY=supersecretkey
DB_NAME=app.db
LOG_DIR=logs
LOG_LEVEL=INFO
LOG_FILE=app.log
```
Never commit `.env` to version control—use `.env.example` for sharing structure. you will need to add your own key.

<br>
<br>

## 5. **(Optional) Run logging setup (clears old logs and verifies setup):**


```
python setup_logs.py

```

<br>
<br>

## 6. **reset the db (puts 10 sample records in the db)**

```
python setup_db.py
python setup_logs.py

```

<br>
<br>

## 7. **Run the app:**

```
python app.py

```


<br>
<br>

# Running the App with Docker (Recommended)

This project can be run locally using Docker and Docker Compose, removing the need for Python virtual environments or manual dependency management.
Prerequisites

- Docker Desktop (Windows / macOS / Linux)
- Docker Compose (included with Docker Desktop)

<br>
<br>

## 1. Create a .env file

```
FLASK_ENV=development
SECRET_KEY=your-secret-key
DB_NAME=app.db
LOG_DIR=logs
LOG_LEVEL=INFO
LOG_FILE=app.log

```

** Never commit .env to version control. **
<br>
<br>


## 2. Build and run the app

From the project root:

```
docker compose up --build

```


This will:

- build the Docker image
- start the Flask app
- expose it on port 5000

Access the app at:
http://localhost:5000

<br>
<br>

## 3. Stopping the app

Press Ctrl + C to stop the containers.

To fully clean up:

```
docker compose down
```

Stop and remove everything Docker created
This shuts down containers, removes the network, and deletes the built images created by Compose:
```
docker compose down--rmi local --remove-orphansShow more lines
```

If you ever add named volumes and want those gone too:
```
docker compose down --rmi local --volumes --remove-orphans
```

<br>
<br>

## 4. Running helper scripts and tests

Run one-off commands inside the same container environment:

```
# Reset database (creates sample data)
docker compose run --rm web python setup_db.py

# Reset logs
docker compose run --rm web python setup_logs.py

# Run tests
docker compose run --rm web pytest tests
```
<br>
<br>

## 5. Data persistence

- SQLite database (app.db) is stored on the host and persists between runs
- Logs are written to the logs/ directory on the host


<br>
<br>

# Testing

### Run tests locally:

```bash
python -m pytest tests
```


### Format + lint before committing:

```bash
black .
flake8
```

### Security scan before pushing:

```bash
bandit -r . -x tests,venv,.venv,__pycache__ -s B101,B311
```

### Lint templates:

```bash
djlint templates/ --check
```

<br>
<br>

#  Useful Dev Commands

```bash
# Freeze current dependencies into requirements.txt
pip freeze > requirements.txt

# Deactivate the current Python virtual environment
deactivate

# Delete the virtual environment folder
rm -rf .venv        # macOS/Linux
rmdir /s /q .venv   # Windows

# Run Flask locally
python app.py
```

<br>
<br>


## 🛠️ Future Improvements

- [X] Dockerization for deployable containers  
- [ ] Role-based access control enhancements  
- [ ] Email notifications for ticket updates  
- [ ] Pagination/search for large ticket queues  

