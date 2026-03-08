# Automated LinkedIn Job Tracker with n8n

![n8n Workflow Diagram](https://img.shields.io/badge/Workflow%20Built%20With-n8n-FF6600?style=for-the-badge&logo=n8n)

## Table of Contents
- [Description](#description)
- [Problem it Solves](#problem-it-solves)
- [How the Workflow Works](#how-the-workflow-works)
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
- [Example Use Case](#example-use-case)

## Description
This n8n workflow provides a robust and customizable solution for automating the tracking and management of job applications, particularly those on platforms like LinkedIn. It aims to reduce manual effort by consolidating application statuses, sending timely reminders, and providing daily summaries directly to your preferred communication channels.

## Problem it Solves
Manually tracking numerous job applications across various platforms can be overwhelming, time-consuming, and prone to errors. Key challenges include:
- **Lack of Centralization:** Difficulty in maintaining an organized overview of all submitted applications and their current statuses.
- **Missed Follow-ups:** Forgetting to follow up on applications after a certain period, potentially missing opportunities.
- **Inefficient Status Updates:** Spending valuable time manually checking the status of each application.
- **Information Overload:** Struggling to digest the current state of all applications without a consolidated summary.

This workflow addresses these issues by automating the data aggregation and notification process, ensuring you stay organized and informed without constant manual intervention.

## How the Workflow Works
This n8n workflow operates on a scheduled basis (e.g., daily) to process your job application data and deliver actionable insights. While the exact implementation can be customized, a typical flow involves the following steps:

1.  **Scheduled Trigger:** The workflow is activated at a predefined interval (e.g., every morning) using an n8n Cron node or manually invoked when needed.
2.  **Data Retrieval:** It fetches your current job application data. This data can originate from various sources such as:
    *   A dedicated spreadsheet (e.g., Google Sheets, Airtable, Excel).
    *   A database (e8.g., PostgreSQL, MySQL).
    *   A Notion database or similar structured data repository.
    *   Internal n8n data storage (e.g., using `Set` and `Get` nodes with `workflow-static-data`).
3.  **Data Processing & Filtering:** The workflow processes the retrieved data to identify key information:
    *   **Applications Awaiting Response:** Jobs for which you've applied and are still in an "active" or "pending" state.
    *   **Follow-up Reminders:** Applications that have passed a specific timeframe (e.g., 7-10 days) since the last interaction and require a follow-up.
    *   **New Applications:** Potentially identifies new applications added to your tracker since the last run.
4.  **Summary Generation:** It compiles a concise summary based on the processed data, highlighting critical updates and action items.
5.  **Notification Delivery:** The generated summary is then sent to your preferred communication channel(s), such as:
    *   **Email:** Via Gmail, Outlook, or a generic SMTP server.
    *   **Messaging Apps:** Slack, Telegram, Discord.
    *   **Other Platforms:** Any service with an available n8n integration.
6.  **Data Update (Optional):** Optionally, the workflow can update the status of applications in your data source (e.g., marking "followed-up" or changing status based on external input).

## Technologies Used
-   **n8n:** An extendable workflow automation platform that allows you to connect any app with an API to build powerful automations.
-   **LinkedIn:** The primary platform for job searching and application (though direct interaction with LinkedIn's private APIs is generally not supported, this workflow focuses on *tracking your interactions* with LinkedIn jobs).
-   **Data Storage (Choose one or more, depending on your setup):**
    *   Google Sheets / Excel Online
    *   Airtable
    *   Notion
    *   Baserow
    *   Any SQL Database
-   **Communication Channels (Choose one or more):**
    *   Email (e.g., Gmail, Outlook, SMTP)
    *   Slack
    *   Telegram
    *   Discord

## Setup Instructions
To get this workflow up and running, follow these steps:

### 1. Prerequisites
*   An active n8n instance (self-hosted or cloud-hosted).
*   An account with your chosen data storage service (e.g., Google, Airtable, Notion).
*   (Optional) An account with your preferred notification service (e.g., email provider, Slack).

### 2. Import the Workflow
1.  Open your n8n instance in your web browser.
2.  Navigate to the "Workflows" section.
3.  Click on "New" or "Add Workflow", then select "Import from JSON".
4.  Paste the workflow JSON below into the import dialog:

    ```json
    <!-- The sanitized workflow JSON would be placed here. As the provided Workflow JSON was '[object Object]', please replace this comment with your actual n8n workflow JSON. -->
    ```

### 3. Configure Credentials
Once imported, you'll need to configure the credentials for the various nodes used in the workflow:
1.  **Email Node (e.g., Gmail, SMTP):** Set up your email credentials to allow n8n to send notifications.
2.  **Data Storage Node (e.g., Google Sheets, Airtable, Notion):** Configure credentials for the service where your job application data is stored.
3.  **Messaging App Node (e.g., Slack, Telegram):** If you're using a messaging app for notifications, set up the relevant API keys or webhooks.

    *Refer to the n8n documentation for detailed instructions on configuring each credential type.*

### 4. Customize the Workflow
Adjust the workflow nodes to fit your specific needs:
1.  **Trigger Node:** Modify the Cron node to set your desired schedule (e.g., daily at 8 AM, every weekday morning).
2.  **Data Source Node:** Update the configuration of your data retrieval node (e.g., Google Sheets, Airtable) to point to your specific spreadsheet, table, or database.
3.  **Logic & Filtering Nodes:** Customize the `Code` or `Filter` nodes to match your tracking fields (e.g., `status`, `applicationDate`, `followUpDate`) and desired logic for identifying applications needing attention.
4.  **Notification Node:** Adjust the message content, subject line, and recipient(s) in your email or messaging app node to personalize your daily summary.

### 5. Activate the Workflow
After all configurations are complete, activate the workflow by toggling the "Active" switch in the top right corner of the n8n editor. The workflow will then run according to its schedule.

## Example Use Case
Imagine a job seeker, Sarah, who has applied to several positions on LinkedIn and other platforms. She uses a Google Sheet to track each application with fields like 'Company', 'Role', 'Application Date', 'Status', and 'Last Follow-up Date'.

This n8n workflow can be configured to:
*   **Daily Morning Digest:** Send Sarah a Slack message every weekday at 9:00 AM.
*   **Summary Content:** The message includes:
    *   A list of all applications currently in 'Applied' or 'Interviewing' status.
    *   A specific section for applications where the 'Last Follow-up Date' is more than 7 days ago, prompting her to send a follow-up email.
    *   A reminder for any upcoming interviews scheduled for the day.
*   **Streamlined Actions:** Sarah can quickly glance at her Slack message to understand her job search status, prioritize follow-ups, and prepare for interviews, all without manually sifting through her spreadsheet or LinkedIn notifications.