---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

Deploying both the backend, built with FastAPI, and the frontend, developed using Vue.js.

### Backend (FastAPI)

There are the steps of building and publishing my FastAPI project using Poetry, a dependency management tool for Python. This is how to configure your project for publication to both Test-PyPI and PyPI, allowing you to distribute your application effectively.

1. **Build Your Project**:
    Use Poetry to build the project, creating the necessary distribution archives.

     ```sh
       poetry build
      ```
    Publish to Test-PyPI:
    Ensure your credentials are set for Test-PyPI:
    
     ```sh
    poetry config pypi-token.testpypi <pypi-token>
     ```
     
    Then publish to Test-PyPI, a separate instance of PyPI used for testing the distribution process. Useful for ensuring that the package can be correctly built, uploaded, and installed before releasing to the main PyPI.
    
     ```sh
    poetry publish --repository testpypi
     ```
    
    Publish to PyPI:
    Ensure your credentials are set for PyPI:
    
     ```sh
      poetry config pypi-token.pypi <pypi-token>
     ```
    
    Then publish to PyPI:
    
     ```sh
      poetry publish
     ```
     
### Frontend (Vue.js)

Next, we will cover the steps to build your Vue.js project for production. This is how to generate the necessary production-ready files and prepare your application for deployment to a hosting service, ensuring your frontend is live and accessible to users.

1. **Build Your Project**:
Run the build command to generate the production-ready files.
    
     ```sh
      npm run build
     ```
    
1. **Deployng to hosting service**:
Choose an hosting service like AWS for the accessibility to users. 
