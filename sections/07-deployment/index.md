---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

## Prerequisites

1. **A server or cloud instance**: using a service like AWS.
2. **Docker installed**: Docker is used to containerize the application.
3. **Docker Compose installed**: Docker Compose is used to run multi-container Docker applications.
4. **Access to a MySQL database**: This is used to store the application data.
5. **The environment configuration file (`.env`)**: This file contains all the necessary environment variables.

## Steps to Deploy Backend

### Step 1: Prepare the Environment Configuration File

Create a `.env` file in the root directory of your project and add the necessary environment variables.

### Step 2: Dockerize the Backend Application
Create a Dockerfile in the root directory of your project to define the Docker image for your FastAPI application.

### Step 3: Create a Docker Compose File
Create a docker-compose.yml file to manage your application and its dependencies, such as the MySQL database.

### Step 4: Deploy the Application
Build and Start the Containers: Use Docker Compose to build and start the containers.

```sh
  docker-compose up -d --build
```
Verify the Containers: Check if the containers are running.

```sh
  docker-compose ps
```
### Step 5: Access the Application
Open your browser and go to http://server-ip:8000/docs to access the application api.

## Steps to Deploy Frontend

### Step 1: Build the Frontend
Navigate to the Vue.js project directory and run the following command to build the production files:

```sh
  npm run build
```

### Step 2: Dockerize the Frontend
Create a Dockerfile in the Vue.js project root directory to define the Docker image for the frontend.

### Step 4: Deploy the Application
Build and Start the Containers: Use Docker Compose to build and start the containers.

```sh
  docker-compose up -d --build
```
Verify the Containers: Check if the containers are running.

```sh
  docker-compose ps
```

### Step 5: Access the Frontend
Open your browser and go to http://server-ip to access the frontend pages
