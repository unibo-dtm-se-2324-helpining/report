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

3. **Job Structure Frontend**:
      - **Test Backend**:
         
         ```yaml
         
         name: CI/CD
         on:
           push:
             paths-ignore:
               - '.gitignore'
               - 'LICENSE'
               - 'README.md'
           pull_request:
           workflow_dispatch:
         jobs:
           test:
             strategy:
               fail-fast: false
               matrix:
                 os:
                   - windows-latest
                 python-version:
                   - '3.10'
                   - '3.11'
                   - '3.12'
             runs-on: ${{ matrix.os }}
             name: Test on Python ${{ matrix.python-version }}, on ${{ matrix.os }}
             timeout-minutes: 45
             steps:
               - name: Setup Python
                 uses: actions/setup-python@v5
                 with:
                   python-version: ${{ matrix.python-version }}
         
               - name: Install poetry
                 run: pip install poetry
               
               - name: Checkout code
                 uses: actions/checkout@v4
         
               - name: Restore Python dependencies
                 run: poetry install
         
               - name: Test
                 shell: bash
                 run: poetry run python -m unittest discover -v -s tests
         
         ```
        - Sets up the Python environment.
        - Installs dependencies using Poetry.
        - Runs tests to ensure the backend code is functioning correctly.

   - **Release**:
           
         ```yaml
         
         release:
             needs: test
             if: github.ref == 'refs/heads/master'
             runs-on: ubuntu-latest
             name: Release on PyPI and GitHub
             permissions:
               contents: write
             steps:
               - name: Checkout code
                 uses: actions/checkout@v4
                 with:
                   fetch-depth: 0
                   token: ${{ secrets.GITHUB_TOKEN }}
         
               - name: Install poetry
                 run: pip install poetry
         
               - name: Restore Python dependencies
                 run: poetry install
         
               - name: Build Python Package
                 run: poetry build
         
               - name: Publish on TestPyPI
                 run: poetry publish --repository pypi-test --username __token__ --password ${{ secrets.TEST_PYPI_TOKEN }}
         
               - name: Create GitHub Release
                 shell: bash
                 run: |
                   RELEASE_TAG=$(poetry version --short)
                   gh release create $RELEASE_TAG dist/* -t v$RELEASE_TAG -F CHANGELOG.md
                 env:
                   GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
         
         ```
     
     - Builds the Fastapi backend application.
     - Deploys the built application to the server TestPyPI and creates the GitHub release.
       
5. **Job Structure Frontend**:
   - **Build Frontend**:
     - Sets up the Node.js environment.
     - Installs dependencies.
     - Builds the Vue.js frontend application.
   - **Deployment**:
     - Deploys the built application to the server Hosting.
