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

### Use Case 1: User Seeking Expert Assistance
- **Scenario**: A user encounters a complex problem in their field of study or work.
- **Action**: The user logs into 'Helpining', navigates to the request submission page, and uploads a detailed description of their problem.
- **Outcome**: The request appears on a public notice board visible to relevant experts, who can then choose to offer assistance.

### Use Case 2: Expert Offering Assistance
- **Scenario**: An expert in a particular field logs into 'Helpining' and browses the public notice board for user requests that match their expertise.
- **Action**: The expert selects a request they can assist with and accepts it.
- **Outcome**: The request is added to the user's personal notice board, and the user is notified of the expert's acceptance.

### Use Case 3: Scheduling and Conducting a Video Call
- **Scenario**: A user selects an expert from their personal notice board to address their problem.
- **Action**: The application sends an email to the expert with a link to join a Microsoft Teams meeting, facilitating direct communication.
- **Outcome**: The user and expert engage in a real-time video call through the third-party application, allowing the expert to provide immediate assistance.

### Use Case 4: Profile Management
- **Scenario**: Users and experts need to update their personal information or expertise areas.
- **Action**: They access their profile management page, make the necessary updates, and save the changes.
- **Outcome**: The updated information ensures that the platform remains relevant and accurate, improving the matching process between users and experts.

## User Stories

### User Story 1: Submitting a Request
As a user, I want to submit a detailed description of my problem so that I can receive assistance from an expert.

### User Story 2: Browsing Expert Profiles
As a user, I want to browse the profiles of available experts so that I can choose the best match for my problem.

### User Story 3: Accepting a Request
As an expert, I want to browse user requests and accept those that match my expertise so that I can offer my assistance.

### User Story 4: Managing My Profile
As a user or expert, I want to update my personal information and expertise areas so that my profile remains accurate and relevant.

### User Story 5: Receiving Notifications
As a user, I want to receive notifications when an expert accepts my request so that I am informed about the progress.

### User Story 6: Participating in a Video Call
As a user, I want to join a video call with an expert through Microsoft Teams so that I can discuss my problem and receive immediate assistance.

### User Story 7: Rating the Assistance
As a user, I want to rate the expert's assistance after the video call so that I can provide feedback on my experience.

'Helpining' is designed to provide an efficient, reliable, and user-friendly platform for real-time expert assistance, leveraging modern web technologies to connect users and experts seamlessly.
