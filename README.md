# Django Docker

A basic Django application containerized using Docker.

This project demonstrates how a Django application can be packaged into a Docker container so that it can run consistently across different development environments.

## Project Overview

A common problem in application development is:

> "It works on my machine."

Different developers may have different operating systems, Python versions, dependencies, and configurations. This can make it difficult for others to run and contribute to the same project.

Docker helps solve this problem by packaging the application and its required environment into a reproducible container.

In this project, a Django application is containerized using a Dockerfile.

## Technologies Used

* Python
* Django
* Docker
* Git
* GitHub

## Project Structure

```text
django-docker/
├── .gitignore
└── devops/
    ├── Dockerfile
    ├── manage.py
    ├── requirements.txt
    ├── devops/
    │   ├── settings.py
    │   ├── urls.py
    │   ├── asgi.py
    │   └── wsgi.py
    └── polls/
        ├── admin.py
        ├── apps.py
        ├── models.py
        ├── tests.py
        ├── urls.py
        └── views.py
```

## Dockerfile

The Dockerfile defines how the Docker image for the application is created.

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

### What it does

* `FROM` — Uses Python 3.12 as the base environment.
* `WORKDIR` — Sets `/app` as the working directory inside the container.
* `COPY requirements.txt` — Copies the project's Python dependencies.
* `RUN pip install` — Installs the dependencies inside the image.
* `COPY . .` — Copies the Django application into the image.
* `EXPOSE 8000` — Documents that the application uses port 8000.
* `CMD` — Starts the Django development server.

## Running the Project with Docker

### 1. Clone the repository

```bash
git clone https://github.com/anishdimri3a/django-docker.git
cd django-docker/devops
```

### 2. Build the Docker image

```bash
docker build -t django-docker .
```

The `.` tells Docker to use the current directory as the build context.

### 3. Run the container

```bash
docker run -d -p 8000:8000 django-docker
```

The `-p` option maps:

```text
Host port 8000 → Container port 8000
```

### 4. Access the application

Open:

```text
http://localhost:8000/polls/
```

You should see:

```text
Hello, world. You're at the polls index.
```

## Docker Workflow

The workflow used in this project is:

```text
Django Application
       ↓
requirements.txt
       ↓
Dockerfile
       ↓
docker build
       ↓
Docker Image
       ↓
docker run
       ↓
Docker Container
       ↓
Running Django Application
```

## Why Docker?

Without Docker, another developer may need to manually configure:

* Python
* Django
* Python dependencies
* Environment configuration
* Application setup

Docker allows the required environment and application setup to be defined consistently.

The source code is shared through GitHub, while Docker provides a consistent environment in which the application can run.

## What I Learned

Through this project, I learned:

* Basic Django application structure
* Git and GitHub workflow
* How `requirements.txt` manages Python dependencies
* What a Dockerfile is
* How Docker build context works
* How to build a Docker image
* How to run a Docker container
* Port mapping between host and container
* The difference between an image and a container
* How to containerize a web application
* Why containerization helps solve environment differences

## Future Improvements

This project is intentionally basic and focuses on understanding the fundamentals of containerization.

Possible next steps:

* Docker Compose
* PostgreSQL
* Environment variables
* Gunicorn
* Nginx
* GitHub Actions CI/CD
* Deployment to AWS EC2

## Author

**Anish Dimri**
