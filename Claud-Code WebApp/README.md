# Claud-Code WebApp

A simple Flask web application built with Claude Code, deployable via Docker and Jenkins.

## Project Structure

```
Claud-Code WebApp/
├── app.py               # Flask application
├── requirements.txt     # Python dependencies
├── Dockerfile           # Docker image definition
├── docker-compose.yml   # Docker Compose for local runs
├── Jenkinsfile          # Jenkins CI/CD pipeline
└── README.md            # This file
```

## Prerequisites

- Python 3.12+
- Docker Desktop
- Jenkins (local desktop install)

---

## Run Locally (without Docker)

```bash
pip install -r requirements.txt
python app.py
```

Visit: http://localhost:5000

---

## Run with Docker

### Build and run manually:
```bash
docker build -t claud-code-webapp .
docker run -d -p 5000:5000 --name claud-code-webapp claud-code-webapp
```

### Using Docker Compose:
```bash
docker-compose up -d
```

Visit: http://localhost:5000

---

## Jenkins Setup (Local Desktop)

### 1. Install Jenkins
Download from https://www.jenkins.io/download/ and start it:
```bash
brew install jenkins-lts
brew services start jenkins-lts
```
Access Jenkins at: http://localhost:8080

### 2. Install Required Plugins
Go to **Manage Jenkins → Plugins** and install:
- Docker Pipeline
- Git

### 3. Create a Pipeline Job
1. Click **New Item** → name it `claud-code-webapp` → select **Pipeline**
2. Under **Pipeline**, set **Definition** to `Pipeline script from SCM`
3. Set **SCM** to `Git` and enter your repo URL
4. Set **Script Path** to `Claud-Code WebApp/Jenkinsfile`
5. Save and click **Build Now**

### 4. Jenkins needs Docker access
Make sure the Jenkins user can run Docker:
```bash
sudo usermod -aG docker jenkins
```
Or on macOS, ensure Docker Desktop is running when Jenkins builds.

---

## Pipeline Stages

| Stage | Description |
|---|---|
| Checkout | Pulls source code from SCM |
| Build Docker Image | Builds the Docker image |
| Stop Existing Container | Removes any running instance |
| Deploy Container | Starts the new container on port 5000 |
| Health Check | Verifies the app is responding |

---

## App Output

Visiting `http://localhost:5000` returns:

```
Hello Kalapriya, you are on the first Claude Code built App
```
