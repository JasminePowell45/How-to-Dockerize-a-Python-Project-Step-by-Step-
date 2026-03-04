# How to Dockerize a Python Project (Step-by-Step)

## Overview

This tutorial explains how to containerize a simple Python REST API using Docker. 
By the end of this guide, you will be able to package a Python application into a Docker container and run it locally.

The example project uses: 
- Python
- FastAPI 
- Docker 

---

## Prerequisites 

Before starting, make sure you have:

- Python 3 installed
- Docker Desktop installed
- Basic familiarity with the terminal 

---

## Step 1: Create the Project Structure

Create a project folder and a directory for the application code.

---

## Step 2: Create the Pyrhon API

Inside `app/main.py` create a simple FastAPI application.

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def root():
    return {"message": "Hello from Docker + Python"}

@app.get("/health")
def health():
    return {"status": "ok"}
```

---

## Step 3: Add Dependencies 

Create a requirement.txt file:
```
fastapi
uvicorn[standard]
```

Install dependencies locally:
```
pip install -r requirements.txt
```

Run the API:
```
uvicorn app.main:app --host 127.0.0.1 --port 8000
```
---

## Step 4: Create the Dockerfile 

Create a Dockerfile in the project root.
```
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirments.txt

COPY app ./app

EXPOSE 8000

CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]
```
---

## Step 5: Build the Docker Image 

Build the Docker image using the following command:
```
docker build -t dockerize-python .
```

---

## Step 6: Run the Container 

Run the container and expose port 8000.
```
docker run -p 8000:8000 dockerize-python
```

Open a browser and navigate to:
```
http://localhost:8000
```

You should see the API response.

## Troubleshooting 

Common issues include: 
* Docker not installed 
* Port 8000 already in use
* Missing dependencies

## Future Improvements 

Possible improvements include:
* Adding environment variables
* Using Docker Compose
* Adding automated tests

