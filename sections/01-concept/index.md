---
title: Concept
has_children: false
nav_order: 2
---

# Concept

## Product Type

'Helpining' is a web application designed to provide real-time expert assistance across various fields such as engineering, economics, mathematics, and law. The platform features a graphical user interface (GUI) accessible via web browsers, ensuring a user-friendly experience for both users and experts. This web application leverages modern front-end and back-end technologies to deliver a seamless and responsive service.

### Key Components:
- **Front-end**: Developed using the VueJs framework, providing a dynamic and interactive user interface.
- **Back-end**: Built with Python FastAPI, connected to a MySQL database, ensuring efficient data management and server-side operations.
- **Third-party Integration**: Utilizes Microsoft Teams to facilitate real-time problem-solving sessions between users and experts.

## Use Case Collection
![Use cases](/report/pictures/useCase.png)

### Use Case 1: Create an account
- **Scenario**: The user or expert create an account to logs into 'Helpining' and use functionalities.

### Use Case 2: User Upload help request
- **Scenario**: The user logs into 'Helpining', navigates to the request submission page, and uploads a detailed description of their problem.

### Use Case 3: Expert accept user help request
- **Scenario**: An expert in a particular field logs into 'Helpining' and browses the public notice board for user requests that match their expertise. The expert selects a request they can assist with and accepts it.

### Use Case 4: User select expert for resolving help request
- **Scenario**: The application sends an email to the expert with a link to join a Microsoft Teams meeting, facilitating direct communication.

### Use Case 5: User rate the assistance
- **Scenario**: The user rate the expert about the resolving of the issue.

### Use Case 6: User and Expert update ther personal profile Management
- **Scenario**: They access their profile management page, make the necessary updates, and save the changes.

## User Stories

### User Story 1: Creating an account
As a potential user, I want to subscribe the service so that I can become a user and exploit services.

### User Story 2: Submitting a Request
As a user, I want to submit a detailed description of my problem so that I can receive assistance from an expert.

### User Story 3: Accepting a Request
As an expert, I want to browse user requests and accept those that match my expertise so that I can offer my assistance.

### User Story 4: Browsing Expert Profiles
As a user, I want to browse the profiles of available experts for my request so that I can choose the best match for my problem.

### User Story 5: Managing My Profile
As a user or expert, I want to update my personal information and expertise areas so that my profile remains accurate and relevant.

### User Story 6: Receiving Notifications
As a user, I want to receive notifications when an expert accepts my request so that I am informed about the progress.

### User Story 7: Participating in a Video Call
As a user, I want to join a video call with an expert through Microsoft Teams so that I can discuss my problem and receive immediate assistance.

### User Story 8: Rating the Assistance
As a user, I want to rate the expert's assistance after the video call so that I can provide feedback on my experience.
