---
title: Deployment
has_children: false
nav_order: 8
---

# Deployment

#### Backend (FastAPI)

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
    Then publish to Test-PyPI:
    
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
    
    Build Your Project:
    Run the build command to generate the production-ready files.
    
     ```sh
      npm run build
     ```
    
    Deploy to Hosting Service
