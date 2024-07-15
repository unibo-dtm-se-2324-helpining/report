---
title: Requirements
has_children: false
nav_order: 3
---

# Requirements

## Goals
- Provide a platform for users to receive real-time expert assistance in various fields.
- Ensure a user-friendly graphical interface.
- Facilitate effective communication between users and experts using Microsoft Teams.

## Functional Requirements

### User Authentication
- **Requirement**: Users must be able to register and log in to the application. Users can create an account with an email and password and log in using their credentials.

### Request Submission
- **Requirement**: Users must be able to submit detailed help requests. Users can fill out a form with their problem description and upload any relevant documents.

### Expert Browsing and Acceptance
- **Requirement**: Experts must be able to browse and accept user requests. Experts can view a list of user requests, filter them by category, and accept a request, triggering a notification to the user.

### Profile Management
- **Requirement**: Users and experts must be able to update their personal profiles. Users and experts can edit their personal information, expertise areas, and save changes successfully.

### Real-time Communication
- **Requirement**: Users and experts must be able to communicate in real-time via Microsoft Teams. Users receive a link to a Microsoft Teams meeting once an expert accepts their request, and they can join the meeting at the scheduled time.

### Rating System
- **Requirement**: Users must be able to rate the assistance received from experts. After a session, users can submit a rating and feedback for the expert's assistance.

### Notification System
- **Requirement**: Users must receive notifications about their request status. Users receive email notifications when their request is accepted and when updates are made to their request.

## Non-functional Requirements

### Security
- **Requirement**: User data must be securely stored and transmitted by a JWT session management. Data is encrypted in transit and at rest, and users can reset their passwords securely.

### Usability
- **Requirement**: The application must be easy to navigate and use. Users can complete common tasks without errors and receive clear instructions and feedback.

### Scalability
- **Requirement**: The application must handle increasing numbers of users and requests. The application performs well under load and can be scaled horizontally to handle additional traffic.

## Implementation Requirements

### Technology Stack
- **Requirement**: The application must be built using VueJs for the front-end and Python FastAPI for the back-end. The front-end is developed using VueJs, and the back-end is implemented with Python FastAPI.

### Database
- **Requirement**: The application must use MySQL for data storage. All application data is stored and managed in a MySQL database.

### Integration
- **Requirement**: The application must integrate with Microsoft Teams for video calls. Users and experts can join video calls through Microsoft Teams, initiated from the application.
