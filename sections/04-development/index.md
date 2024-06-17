---
title: Development
has_children: false
nav_order: 5
---

# Development

## DVCS

The development process of my Helpining project adheres to a Distributed Version Control System (DVCS) model to streamline collaboration, ensure code quality, and facilitate continuous integration. This section delves into the conventions we have established for branch usage, commit practices, and other relevant aspects.

### Branch Usage Conventions

My branching strategy is designed to maximize efficiency and minimize risks associated with code integration. We utilize two primary branches: `dev` and `main`.

- **main**: The `main` branch serves as the backbone of my project. It is the production-ready branch, representing the most stable and thoroughly tested codebase. Merging into `main` signifies that the changes have undergone rigorous testing and review processes, ensuring that only the quality code reaches production environment. This branch is protected, requiring pull requests which are the alignment requests from the branch concerned to the programmer's computer.

- **dev**: The `dev` branch is the active development branch where all new features and bug fixes are initially integrated. By isolating development work from the production code, we can iterate rapidly without compromising the stability of the `main` branch. This approach allows developers to experiment and refine their code until it is stable enough to be merged into `main`.

### Commit Conventions

Commit messages play a critical role in the clarity and maintainability of my project. We enforce a strict convention to ensure that every commit is meaningful and traceable.

- **Conciseness and Descriptiveness**: Each commit message should succinctly describe the changes made.
  
- **Format**: Use the present and imperative mood for commit messages (Add, Update, Delete). This style conveys that a commit applies changes as of the moment of writing, providing a more direct and active tone. For example, use "Add user authentication feature".

- **Structure**: Start with a capital letter and avoid ending with a period.

### Additional Relevant Aspects

- **Branch Protection and Code Reviews**: Protecting the `main` branch by enforcing mandatory pull requests ensures that all changes are subject to peer review. This process is crucial for maintaining code quality and fostering a collaborative development environment. Peer reviews help identify potential issues early, provide opportunities for knowledge sharing, and enhance overall code quality.

- **Documentation and Code Comments**: Maintaining thorough documentation and code comments is a fundamental aspect of my development process. Clear documentation facilitates easier onboarding of new developers and enhances the maintainability of the codebase. Comments within the code should explain the 'why' behind complex logic, providing context that goes beyond the 'what' that is evident from the code itself.

### Implementation details

```python
from fastapi import FastAPI, APIRouter, HTTPException, Query, Request, Depends, Form, Body

# Import your business service and JWT extraction logic
from ..services.BusinessService import AccessService
from ..services.JWTService import extract_jwt, JWTextracted  # Assuming you have these for JWT handling

# Initialize FastAPI application
app = FastAPI()
controller = APIRouter()

# HelpRequest routes
@controller.post("/help_requests/")
async def upload_help_request(
    request: Request,
    id: str,
    title: str,
    body: str,
    skill: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to insert a new help request.
    """
    return service.insert_help_request(id, title, body, skill)

@controller.put("/help_requests/{id}/status/")
async def update_help_request_status(
    request: Request,
    id: str,
    new_status: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to update the status of a help request.
    """
    return service.update_help_request_status(id, new_status)

@controller.put("/help_requests/{id}/review/")
async def insert_review(
    request: Request,
    id: str,
    review: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to insert a review for a help request.
    """
    return service.insert_review(id, review)

@controller.delete("/help_requests/{id}/")
async def delete_help_request(
    request: Request,
    id: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to delete a help request.
    """
    return service.delete_help_request(id)

# Account routes
@controller.post("/accounts/")
async def insert_account(
    request: Request,
    email: str,
    name: str,
    surname: str,
    password: str,
    description: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to insert a new account.
    """
    return service.insert_account(email, name, surname, password, description)

@controller.put("/accounts/")
async def update_account_by_email(
    request: Request,
    email: str,
    name: str = Form(None),
    surname: str = Form(None),
    password: str = Form(None),
    description: str = Form(None),
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to update an existing account by email.
    """
    return service.update_account_by_email(email, name, surname, password, description)

@controller.delete("/accounts/")
async def delete_account_by_email(
    request: Request,
    email: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to delete an account by email.
    """
    return service.delete_account_by_email(email)

@controller.get("/accounts/experts_by_skill/")
async def get_experts_by_skill(
    request: Request,
    skill: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to get experts by skill.
    """
    return service.get_experts_by_skill(skill)

# Expert routes
@controller.post("/experts/{email}/skills/")
async def add_skill(
    request: Request,
    email: str,
    skill: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to add a skill to an expert.
    """
    return service.add_skill(email, skill)

@controller.delete("/experts/{email}/skills/")
async def remove_skill(
    request: Request,
    email: str,
    skill: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to remove a skill from an expert.
    """
    return service.remove_skill(email, skill)

# Operation routes
@controller.get("/operations/choose_expert/")
async def get_choose_expert(
    request: Request,
    expert_email: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to choose an expert.
    """
    return service.choose_expert(account, expert_email)

@controller.get("/operations/generate_send_call_email/")
async def get_generate_send_call_email(
    request: Request,
    expert_email: str,
    service: AccessService = Depends(AccessService),
    account: JWTextracted = Depends(extract_jwt)
):
    """
    Endpoint to generate and send a call email.
    """
    return service.generate_send_call_email(account, expert_email)

# Include the router in the FastAPI app
app.include_router(controller)
```

#### Import Statements:

Imports FastAPI, APIRouter, and necessary dependencies.
Imports the AccessService and JWT extraction logic (extract_jwt and JWTextracted).
#### Initialization:

Initializes the FastAPI app and APIRouter.

#### HelpRequest Routes:

insert_help_request: Inserts a new help request.
update_help_request_status: Updates the status of an existing help request.
insert_review: Inserts a review for a help request.
delete_help_request: Deletes an existing help request.

#### Account Routes:

insert_account: Inserts a new account.
update_account_by_email: Updates an existing account by email.
delete_account_by_email: Deletes an account by email.
get_experts_by_skill: Retrieves experts by skill.

#### Expert Routes:

add_skill: Adds a skill to an expert.
remove_skill: Removes a skill from an expert.

#### Operation Routes:

get_choose_expert: Chooses an expert.
get_generate_send_call_email: Generates and sends a call email.
Each route uses the Depends function to inject dependencies (AccessService and extract_jwt). The Request object and form parameters (Form) are used to handle incoming data, and responses are structured as JSONResponse, maintaining consistency with the architectural style.
