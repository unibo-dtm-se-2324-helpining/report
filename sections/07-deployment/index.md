---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

## Steps to Deploy Backend

### Step 1: Dockerize the Backend Application
Create a Dockerfile in the root directory of your project to define the Docker image for your FastAPI application.

### Step 2: Create a Docker Compose File
Create a docker-compose.yml file to manage your application and the connection to MySQL database.

### Step 3: Deploy the Application
Build and Start the Containers: Use Docker Compose to build and start the containers.

```sh
  docker-compose up -d --build
```
Verify the Containers: Check if the containers are running.

```sh
  docker-compose ps
```
### Step 4: Access the Application
Open your browser and go to http://server-ip:8000/docs to access the application api.

## Steps to Deploy Frontend

### Step 1: Dockerize the Frontend
Create a Dockerfile in the Vue.js project root directory to define the Docker image for the frontend.

### Step 2: Create a Docker Compose File
Create a docker-compose.yml file to manage your application and its dependencies.

### Step 3: Deploy the Application
Build and Start the Containers: Use Docker Compose to build and start the containers.

```sh
  docker-compose up -d --build
```
Verify the Containers: Check if the containers are running.

```sh
  docker-compose ps
```

### Step 4: Access the Frontend
Open your browser and go to http://server-ip to access the frontend pages
