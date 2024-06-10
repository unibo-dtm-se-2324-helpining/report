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
ClassService is an important class of my project that is designed to automate the process of creating microsoft online meeting between user and exper.
In particular the method genarate_send_call_email handles the entire workflow of microsoft authentication, quering from the MySQL database the expert data, creating the meeting and sending the email to the expert with the call url. At the end of the method i close MySQL connsection and return to the user the meeting url.

```python
class CallService:

    def __init__(self):
        self.connector = mysql.connector

    def generate_send_call_email(self, expert_email, user_email, user_name, user_surname, client_id, client_secret, tenant_id):
        # input data from vue client
        # Authentication details
        resource = "https://graph.microsoft.com/"

        # Get access token
        auth_url = f"https://logisun.microsoftonline.com/{tenant_id}/oauth2/token"
        auth_data = {
            "grant_type": "client_credentials",
            "client_id": client_id,
            "client_secret": client_secret,
            "resource": resource
        }

        auth_response = requests.post(auth_url, data=auth_data)
        auth_response_data = auth_response.json()
        access_token = auth_response_data["access_token"]

        # Set headers
        headers = {
            "Authorization": "Bearer " + access_token,
            "Content-Type": "application/json"
        }

        # API endpoint to create a meeting
        create_meeting_url = "https://graph.microsoft.com/v1.0/me/onlineMeetings"

        # Set up the meeting payload
        start_call = datetime.now()
        end_call = datetime.now() + timedelta(minutes=15)
        meeting_payload = {
            "startDateTime": start_call.strftime(),
            "endDateTime": end_call.strftime(),
            "subject": "Help call meeting"
        }

        # Create the meeting
        response = requests.post(create_meeting_url, headers=headers, data=json.dumps(meeting_payload))

        if response.status_code == 200:
            meeting_data = response.json()
            meeting_id = meeting_data["id"]
            meeting_join_url = meeting_data["joinUrl"]
            print("Meeting created successfully. Meeting ID:", meeting_id)

            # Connect to MySQL database
            db_connection = self.connector.connect(
            host="db_host",
            user="db_user",
            password="db_password",
            database="db_name"
        )

            cursor = db_connection.cursor(dictionary=True)

            # Fetch participant details
            cursor.execute("SELECT email, name, surname FROM ACCOUNT_TABLE WHERE email = %s", (expert_email,))
            participant = cursor.fetchone()

            # Email details HTML
            email_subject = "Meeting Invitation: Help call meeting"
            email_body = f"""
            <p>Dear Expert {participant['name']} {participant['surname']},</p>
            <p>You have been invited to a meeting for helping {user_name} {user_surname}.</p>
            <p><b>Subject:</b> Help call meeting</p>
            <p><b>Start Time:</b> {start_call}</p>
            <p><b>End Time:</b> {end_call}</p>
            <p><b>Join URL:</b> <a href="{meeting_join_url}">{meeting_join_url}</a></p>
            <p>Best regards,<br>Helpining</p>
            """
            
            # API endpoint to send email
            send_mail_url = "https://graph.microsoft.com/v1.0/me/sendMail"
            email_payload = {
                "message": {
                    "subject": email_subject,
                    "body": {
                        "contentType": "HTML",
                        "content": email_body
                    },
                    "toRecipients": [
                        {
                            "emailAddress": {
                                "address": expert_email
                            }
                        }
                    ]
                }
            }

            # Close the database connection
            cursor.close()
            db_connection.close()
            
            # Send the email
            email_response = requests.post(send_mail_url, headers=headers, data=json.dumps(email_payload))
            if email_response.status_code == 202:
                print("Email sent successfully to:", expert_email)
                # return the meeting url also to the user client
                return meeting_join_url 
            else:
                print("Failed to send email. Status code:", email_response.status_code, "Response:", email_response.text)

        else:
            print("Failed to create meeting. Status code:", response.status_code)
```

