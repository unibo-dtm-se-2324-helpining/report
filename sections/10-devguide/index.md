---
title: Developer guide
has_children: false
nav_order: 11
---

# Developer Guide
## API Endpoint Explanations

### Authentication Route

#### POST /subscribe
- **Description**: Create an account and save credentials.
- **Parameters**:
  - `username` (str): The username of the user.
  - `role` (str): The role of the user.
  - `password` (str): The password of the user.
- **Response**: JSON message containing success or not.

#### POST /login
- **Description**: Authenticates a user and returns a JWT token.
- **Parameters**:
  - `username` (str): The username of the user.
  - `password` (str): The password of the user.
- **Response**: JSON message containing the JWT token.

### HelpRequest Routes

#### POST /help_requests/
- **Description**: Inserts a new help request.
- **Parameters**:
  - `id` (str): The ID of the help request.
  - `title` (str): The title of the help request.
  - `body` (str): The body content of the help request.
  - `skill` (str): Th 
- **Response**: JSON message indicating success.

#### PUT /help_requests/{id}/status/
- **Description**: Updates the status of an existing help request.
- **Parameters**:
  - `id` (str): The ID of the help request.
  - `new_status` (str): The new status to be set.
- **Response**: JSON message indicating success.

#### PUT /help_requests/{id}/review/
- **Description**: Inserts a review for a help request.
- **Parameters**:
  - `id` (str): The ID of the help request.
  - `review` (str): The review content.
- **Response**: JSON message indicating success.

#### DELETE /help_requests/{id}/
- **Description**: Deletes an existing help request.
- **Parameters**:
  - `id` (str): The ID of the help request.
- **Response**: JSON message indicating success.

### Account Routes

#### POST /accounts/
- **Description**: Inserts a new account.
- **Parameters**:
  - `email` (str): The email of the account.
  - `name` (str): The name of the account holder.
  - `surname` (str): The surname of the account holder.
  - `password` (str): The password for the account.
  - `description` (str): The description of the account.
- **Response**: JSON message indicating success.

#### PUT /accounts/
- **Description**: Updates an existing account by email.
- **Parameters**:
  - `email` (str): The email of the account to be updated.
  - `name` (str, optional): The new name of the account holder.
  - `surname` (str, optional): The new surname of the account holder.
  - `password` (str, optional): The new password for the account.
  - `description` (str, optional): The new description of the account.
- **Response**: JSON message indicating success.

#### DELETE /accounts/
- **Description**: Deletes an account by email.
- **Parameters**:
  - `email` (str): The email of the account to be deleted.
- **Response**: JSON message indicating success.

#### GET /accounts/experts_by_skill/
- **Description**: Retrieves experts by skill.
- **Parameters**:
  - `skill` (str): The skill to filter experts by.
- **Response**: JSON message indicating success and data.

### Expert Routes

#### POST /experts/{email}/skills/
- **Description**: Adds a skill to an expert.
- **Parameters**:
  - `email` (str): The email of the expert.
  - `skill` (str): The skill to be added.
- **Response**: JSON message indicating success.

#### DELETE /experts/{email}/skills/
- **Description**: Removes a skill from an expert.
- **Parameters**:
  - `email` (str): The email of the expert.
  - `skill` (str): The skill to be removed.
- **Response**: JSON message indicating success.

### Operation Routes

#### GET /operations/choose_expert/
- **Description**: Chooses an expert.
- **Parameters**:
  - `expert_email` (str): The email of the expert to be chosen.
- **Response**: JSON message indicating success.

#### GET /operations/generate_send_call_email/
- **Description**: Generates and sends a call email.
- **Parameters**:
  - `expert_email` (str): The email of the expert.
- **Response**: JSON message indicating success.

