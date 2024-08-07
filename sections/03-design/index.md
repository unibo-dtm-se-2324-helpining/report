---
title: Design
has_children: false
nav_order: 4
---

# Design

## Architecture

![Architecture](/report/pictures/architectureDiagram.png)

- **VueJS App**: This includes the VueJs-based front-end that provides a dynamic and interactive user interface.
- **FastApi App**: Implemented using Python FastAPI, this layer handles the core functionality of the application, processing
  user requests, and managing data flow. This application is written following the Model-Controller-Service Architecture. The Model-Controller-Service is a software architectural pattern used on server-side applications to improve software maintainability and scalability. In this architecture, your backend application should be separated into three distinct parts that communicate with one another: namely the model, controller, and service layers.
  - **Controller**: This component acts as an API and handles incoming requests from the Vue frontend.
  - **Service**: These are all the parts of the beckend that include the business logic to process incoming requests from the controller.
  - **Model**: This component is responsible for interacting with the database to fulfill any business logic within our application. This could mean providing interfaces for other layers to get or insert data to the database.
- **MySQL server**: Stores all the data related to users, experts, and help requests.

## Modelling

### Domain Modelling
The domain model for 'Helpining' is designed using Unified Modelling Language (UML) principles, ensuring that the core business logic is well encapsulated and decoupled from technical details.

#### Class Diagrams:

1. **Class Diagram**:
   
   ![Class](/report/pictures/classDiagram.png)

   - **Account**: Is a role generalization of User and Expert and Contains all the attributes for managing accounts:  `email`, `name`, `surname`, and `password`.
   - **User**: Extends the account class to manage HelpRequests.
   - **HelpRequest**: Represents a help request submitted by a user. Attributes include `id`, `title`, `body`, and `review`.
   - **Expert**: Extends the Account class to include additional attributes specific to experts, such as `description` and `skills`.
   - **HelpStatus**: Enumeration representing the status of a help request (e.g., Open, Resolved).
   - **Skill**: Enumeration representing different areas of expertise (e.g., Engineering, Mathematics).

3. **Domain Diagram**:
   
    ![Domain](/report/pictures/domainDiagram.png)

   - **Account**: Contains all the private attributes to manage the single account and all the public operations about those attributes.
   - **Accounts**: Is a composition of many Account and contains all the public methods to manage the collection of Accounts.
   - **User**: Methods for profile management.
   - **Expert**: Methods for managing expert-specific data.
   -  **HelpRequest**: Contains the methods and the attributes for managing the single help request.
   -  **HelpRequests**: Is a composition of many HelpRequest and contains all the methods for managing help requests.


## Interaction

### Sequence Diagrams:
Sequence diagrams show how objects interact in a particular scenario of a use case.

1. **Profile Update Sequence**:
   
    ![Update Sequence ](/report/pictures/UpdateSeqDiagram.png)

   - **Person**: Initiates the update profile request through the Vue Client.
   - **Vue Client**: Sends the update request to the FastAPI server.
   - **FastAPI Server**: Validates the JWT token, processes the update query, and interacts with the MySQL database to update the user's profile.
   - **MySQL Database**: Updates the profile information and sends a response back through the FastAPI server to the Vue Client.

3. **Choose Expert for Call Sequence**:
   
    ![Call Sequence ](/report/pictures/callSeqDiagram.png)

   - **User**: Selects an expert for a call.
   - **Vue Client**: Sends a request to the FastAPI server to initiate the call.
   - **FastAPI Server**: Validates the JWT token, retrieves the expert's email, and sends a meeting request via email.
   - **MySQL Database**: Stores and retrieves necessary data related to the expert and the call.

## Behaviour

- This section explains the possible states that the system can be in and the events that cause the transition from one state to another.

### Flowchart Diagram:

[Flowchart](/report/pictures/flowchartDiagram.png)

- **Start**: Initial state when the user begins a help request.
- **Help Request**: User submits a help request.
- **Send Help Request**: The request is sent and validated.
- **Validate User JWT Token**: Authentication check.
- **Filter Experts**: Experts are filtered based on the help request domain.
- **Add Help Request to Expert Notice Board**: The request is added to the board for experts to view and respond.

## Data-related aspects

### Data Schema
The data schema of 'Helpining' is designed to efficiently manage user and expert information, help requests, and interactions.

#### MySQL Database Schema:

   - **Users Table**: Stores information about users and experts.
   - **HelpRequests Table**: Contains details of the help requests submitted by users.
   - **Skills Table**: Lists the skills and areas of expertise available in the system.
   - **Ratings Table**: Holds ratings and reviews given by users to experts.

### Data Persistence Technologies
- **MySQL**: Used for storing user and expert profiles, help requests, and ratings. It ensures data consistency and supports complex queries to facilitate the application's functionalities.


