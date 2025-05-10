# 📝 Todo App – Flask + SQLite + HTML + Docker

This is a simple full-stack Todo application that allows users to **add** and **delete** tasks. It is built with:

- 🐍 **Flask** for the backend
- 💾 **SQLite** as the database
- 🌐 **HTML + JavaScript** for the frontend
- 🐳 **Docker** for containerization
- 📦 **Docker Compose** for managing both services together
- ☁️ Optional **Kubernetes** deployment support

---

## 📁 Project Structure Overview

```
todo-app/                      # Backend files
├── app.py                    # Main Flask application
├── requirements.txt          # Python dependencies
├── Dockerfile                # Backend Dockerfile
├── service.yaml              # K8s service for backend
└── deployment.yaml           # K8s deployment for backend

todo-frontend/                # Frontend files
├── index.html                # HTML + JavaScript UI
├── Dockerfile                # Frontend Dockerfile
├── frontend-service.yaml     # K8s service for frontend
└── frontend-deployment.yaml  # K8s deployment for frontend

.github/
└── workflows/
    └── deploy.yml            # Docker Compose file for running both apps

.gitignore                    # Git ignored files
README.md                     # Project overview
```

---

## 🚀 Features

- Add and delete tasks from a simple UI
- RESTful API with JSON responses
- Data persists using SQLite
- Completely containerized using Docker
- Ready for Kubernetes deployment
- Compatible with GitHub Actions structure

---

## 🧠 How It Works

### 🔙 Backend (Flask)

- Built with Flask and Flask-SQLAlchemy
- Exposes REST API for task management
- Stores data in `tasks.db` (SQLite)
- Provides a `/health` endpoint for health checks

### 🖼️ Frontend (HTML + JS)

- A clean and responsive UI
- Interacts with the backend using `fetch` API
- Uses `http-server` to serve static content in Docker

---

## 🔧 How to Run (Docker Compose)

### 🔹 Prerequisites:
- Docker & Docker Compose installed

### 🔹 Start everything:

```bash
docker compose -f .github/workflows/deploy.yml up --build
```

### 🔹 Access:

- Frontend: [http://localhost:8080](http://localhost:8080)
- API: [http://localhost:5000/tasks](http://localhost:5000/tasks)

---

## 🔗 API Endpoints

| Method | Endpoint         | Description         |
|--------|------------------|---------------------|
| GET    | `/tasks`         | Get all tasks       |
| POST   | `/tasks`         | Add a new task      |
| GET    | `/tasks/<id>`    | Get a single task   |
| DELETE | `/tasks/<id>`    | Delete a task       |
| GET    | `/health`        | Health check        |

---

## 🛠 Dockerfile Descriptions

### ✅ Backend - `todo-app/Dockerfile`

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["python", "app.py"]
```

### ✅ Frontend - `todo-frontend/Dockerfile`

```dockerfile
FROM node:18-alpine
RUN npm install -g http-server
WORKDIR /app
COPY . .
EXPOSE 8080
CMD ["http-server", "-p", "8080"]
```

---

## 📦 Docker Compose – `.github/workflows/deploy.yml`

```yaml
version: "3.8"

services:
  todo-app:
    build: ../../todo-app
    ports:
      - "5000:5000"
    volumes:
      - ../../todo-app:/app
    restart: always

  todo-frontend:
    build: ../../todo-frontend
    ports:
      - "8080:8080"
    restart: always
```

> 🔁 This connects backend and frontend via Docker Compose.

---

## ☸️ Kubernetes Support (Optional)

You can run this project on Kubernetes using the YAML files in each directory.

```bash
kubectl apply -f todo-app/
kubectl apply -f todo-frontend/
```

---

## 📄 .gitignore

Ensures unnecessary files aren't committed:

```
__pycache__/
*.pyc
.env
node_modules/
.vscode/
```

---

## 🙌 Author

Built with ❤️ by [Mohammadsadegh](https://github.com/yourusername)