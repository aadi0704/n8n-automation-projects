# Automated LinkedIn Job Tracker with n8n

## Project Title
Automated LinkedIn Job Tracker with n8n

## Description
This n8n workflow provides a robust and automated solution for job seekers to effortlessly track new job postings on LinkedIn. It is designed to continuously monitor LinkedIn for relevant job listings based on predefined criteria, notify users of new opportunities, and maintain a structured record of all tracked jobs, significantly streamlining the job search process.

## Problem It Solves
Job searching can be an incredibly time-consuming, repetitive, and often overwhelming task. Manually browsing LinkedIn for new job postings across various keywords, locations, and companies is inefficient, prone to human error, and can lead to missing out on valuable, time-sensitive opportunities. This project addresses these challenges by offering an automated system that:
*   **Eliminates manual searching:** Frees up job seekers from constantly checking LinkedIn.
*   **Ensures timely updates:** Provides real-time or scheduled notifications for new openings.
*   **Centralizes job tracking:** Keeps a structured record of all potential opportunities.
*   **Reduces missed opportunities:** Ensures no relevant job goes unnoticed due to manual oversight.

## How the Workflow Works
The n8n workflow is designed to operate seamlessly through a series of automated steps:

1.  **Scheduled Trigger:** The workflow can be configured to run at regular intervals (e.g., hourly, daily) using a `Cron` or `Schedule Trigger` node.
2.  **Job Search:** It connects to LinkedIn (typically via an HTTP Request to a search URL, or through browser automation if a more dynamic interaction is required) to search for jobs based on specified keywords, locations, experience levels, and other filters.
3.  **Data Extraction:** Key information from each job posting is extracted, including job title, company name, location, job URL, description snippet, and posting date.
4.  **Duplicate Checking & Filtering:** Newly found jobs are compared against a historical record (e.g., in a Google Sheet, Notion database, or Airtable) to prevent sending duplicate notifications and to filter out already-viewed or irrelevant postings.
5.  **Data Storage:** Relevant new job postings are stored in a designated database or spreadsheet (e.g., Google Sheets, Notion, Airtable) for easy review, management, and long-term tracking.
6.  **Notifications:** Users receive real-time or summarized notifications (e.g., via Email, Slack, Telegram, Discord, Microsoft Teams) for newly discovered job opportunities, with direct links to the postings.

## Technologies Used
*   **n8n:** The primary workflow automation tool for orchestrating all steps.
*   **LinkedIn:** The platform for sourcing job opportunities.
    *   *Note:* Direct LinkedIn API access for job searching is highly restricted for third-party developers. This workflow typically leverages web scraping techniques (using `HTTP Request` or `Browser Automation` nodes) or integrates with third-party job board aggregators that may include LinkedIn postings.
*   **Google Sheets / Notion / Airtable (Optional):** For structured storage and management of tracked job postings.
*   **Email / Slack / Telegram / Discord / Microsoft Teams (Optional):** For sending custom notifications.

## Setup Instructions

1.  **Install n8n:**
    *   Ensure you have an n8n instance running. You can set it up locally, self-host on a server, or use n8n Cloud. Refer to the official [n8n documentation](https://docs.n8n.io/getting-started/) for detailed installation guides.

2.  **Import the Workflow:**
    *   Assuming the workflow JSON is available, download the workflow file (e.g., `workflow.json`).
    *   In your n8n instance, navigate to the "Workflows" section in the left sidebar.
    *   Click on "New" -> "Import from JSON" and paste the workflow JSON content or upload the file.

3.  **Configure Credentials:**
    *   The imported workflow will likely require credentials for various services (e.g., if using Google Sheets, Email, Slack, etc.).
    *   Locate the credential nodes within the workflow (indicated by a "red" or "yellow" warning icon if unconfigured).
    *   Click on each node, then select "Create New Credential" and follow the prompts to authenticate with your respective accounts (e.g., Google Account for Google Sheets, API token for Slack).

4.  **Customize Workflow Settings:**
    *   **Job Search Parameters:** Find the node responsible for making the LinkedIn search request (e.g., an `HTTP Request` or `Browser Automation` node). Modify the URL query parameters or input fields to specify your desired keywords, location, industry, experience level, and other filters.
    *   **Storage Integration (if used):** If using a Google Sheet, Notion database, or Airtable, configure the respective nodes with your spreadsheet ID, database ID, and ensure the column mappings match your desired data structure.
    *   **Notification Preferences (if used):** Adjust the email, Slack, Telegram, or Discord notification nodes with your recipient email address, channel ID, and customize the message content to your liking.

5.  **Activate and Schedule:**
    *   Once all configurations are complete, activate the workflow by toggling the "Active" switch in the top right corner of the workflow editor.
    *   Configure the `Schedule Trigger` node to run at your preferred frequency (e.g., every 3 hours, once a day) to continuously monitor for new jobs.
    *   Perform a manual test run by clicking "Execute Workflow" to ensure all steps function correctly and data is processed as expected.

## Example Use Case

Consider an experienced "Cloud Engineer" specializing in "AWS" looking for "remote" positions or roles specifically in "Dublin, Ireland". Instead of spending hours each day manually browsing LinkedIn, this n8n workflow can be set up to handle the repetitive tasks.

**Here's how it would work:**

1.  **Scheduled Execution:** The workflow is scheduled to run every 4 hours during weekdays.
2.  **Targeted Search:** It performs a LinkedIn job search for "Cloud Engineer", "AWS", with location filters for "Remote" and "Dublin, Ireland".
3.  **Smart Filtering:** New job postings are checked against a Google Sheet where previously tracked jobs are logged. Only genuinely new and relevant opportunities pass through.
4.  **Structured Storage:** Each new job (title, company, location, URL, description snippet) is added as a new row in your "Cloud Engineer Job Prospects" Google Sheet.
5.  **Instant Notifications:** A concise Slack message is sent to your personal "#job-alerts" channel, summarizing the new jobs found since the last run, including direct links. This allows you to quickly review them on your phone or computer and decide which ones to apply for.