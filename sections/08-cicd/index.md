---
title: CI/CD Strategy
has_children: false
nav_order: 9
---

# CI/CD Strategy

## CI/CD Overview

CI/CD (Continuous Integration and Continuous Deployment) automates the process of testing, building, and deploying applications. For the 'helpining' project, CI/CD ensures that both components frontend and backend are always in a deployable state with automated checks to prevent integration issues.

## Setting Up CI/CD with GitHub Actions

### CI/CD Pipeline Configuration

1. **Workflow Definition**:
   - The CI/CD pipeline is configured using GitHub Actions.
   - The pipeline is defined in a workflow file located in the `.github/workflows` directory of frontend and backend repository.

2. **Workflow Triggers**:
   - The CI/CD workflow is triggered by specific events, such as pushes to the `main` branch and pull requests targeting the `main` branch.
   - This ensures that the pipeline runs automatically whenever there are changes to the codebase.

3. **Job Structure**:
   - **Build Backend**:
     - Sets up the Python environment.
     - Installs dependencies using Poetry.

        - To manage Python dependencies for the FastAPI backend, Poetry is used. Below is the configuration needed.
            ```toml
                [tool.poetry]
                name = "helpining-api"
                version = "0.1.0"
                description = "Backend for the helpining project"
                authors = ["alberto.signorin@studio.unibo.it"]
                
                [tool.poetry.dependencies]
                python = "^3.11"
                fastapi = "^0.111.0"
                uvicorn = "^0.30.1"
                
                [tool.poetry.dev-dependencies]
                pytest = "^8.2.2"
            ```
     - Runs tests to ensure the backend code is functioning correctly.
   - **Build Frontend**:
     - Sets up the Node.js environment.
     - Installs dependencies.
     - Builds the Vue.js frontend application.
   - **Deployment**:
     - Deploys the built application to the server [Deployment](../07-deployment/index.md).

4. **Secrets Management**:
   - GitHub Secrets are used to securely manage sensitive information required for deployment.
   - These secrets are configured in the repository settings and accessed securely within the workflow.
