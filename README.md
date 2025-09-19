# Project Overview

This project is an automated messaging system that sends a daily WhatsApp message to a specific user. The message content is a dynamic countdown of the number of days remaining in the year 2025. The system operates autonomously on a cloud server, requiring no manual intervention after initial setup.

# Functional Specifications

### Core Function
Calculate the number of days between the current date and December 31, 2025.

### User Interaction
Send a daily message to a single, pre-configured WhatsApp number.

### Output
The message body must contain the calculated number of remaining days. For example, "Hello! 👋 There are 105 days left in the year 2025."

### Scheduled Execution
The script must run automatically once per day at a predefined time.

# Technical Stack

### Programming Language
Python 3.x

### Libraries/Dependencies
- **twilio**: A Python SDK for interacting with the Twilio API. This library handles the API calls to send the WhatsApp message.
- **datetime**: A built-in Python module used for date and time calculations.

### Messaging API
Twilio's WhatsApp Business API (Sandbox)

### Hosting Environment
PythonAnywhere (or a similar cloud service with a free tier and scheduled task capabilities).

### Operating System
Linux (the standard operating system for PythonAnywhere servers).

# System Architecture

The system follows a simple client-server model:

- **Scheduled Task (PythonAnywhere)**: A cron job-like task is configured on the PythonAnywhere server. This task is the trigger for the entire process.
- **Script Execution**: At the scheduled time, PythonAnywhere executes the `whatsapp_agent.py` script.
- **Date Calculation**: The script uses Python's `datetime` library to calculate the difference between the current date and the end of the year.
- **API Call**: The script uses the `twilio` library to make an HTTPS POST request to the Twilio API. This request contains the sender number, recipient number, and the message body.
- **Message Delivery (Twilio)**: Twilio receives the API request, processes it, and sends the message to the target WhatsApp number via its WhatsApp Business API.

# Deployment and Operations

- **Deployment Method**: The Python script is deployed via file upload to the PythonAnywhere server. The `twilio` library is installed via a Bash console using `pip install --user twilio`.
- **Scheduling**: The daily execution is managed by PythonAnywhere's built-in "Scheduled tasks" feature, with the time specified in UTC.
- **Maintenance**: The system requires minimal maintenance, primarily limited to a weekly or monthly login to extend the free scheduled task's expiry date on PythonAnywhere.
- **Error Handling**: The Python script includes a `try...except` block to gracefully handle potential errors, such as a network failure or an invalid API key. This will print an error message to the task log on PythonAnywhere for debugging.

# Security Considerations

- **API Keys**: Twilio credentials (Account SID and Auth Token) are stored directly within the Python script. For a more robust production system, these would ideally be stored as environment variables, but for this simple project, storing them directly in the script is acceptable.
- **Access Control**: Access to the PythonAnywhere account is secured by the user's password. Only the user can view and edit the script or scheduled task.
