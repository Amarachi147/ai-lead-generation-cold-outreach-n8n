# AI Lead Generation & Cold Outreach Automation (n8n)

An n8n workflow that finds businesses that need automation every morning, scrapes their contact details, writes a personalized cold email with AI, sends it, and logs everything, with no manual work.

![Workflow canvas](images/workflow-canvas.png)

## What it does

Every day at 7AM the workflow:

1. Searches the web for businesses that could benefit from automation (via Serper)
2. Targets multiple countries: Canada, Australia, UK, France, India
3. Checks a Google Sheet so it never contacts the same lead twice
4. Scrapes the business homepage for a contact email
5. If none is found, scrapes the contact page
6. If still no email, logs the lead for manual follow-up
7. Writes a personalized cold email with OpenAI, in the lead's own language for non-English markets
8. Sends the email through Gmail
9. Logs every lead to Google Sheets
10. Emails me a summary of the run

## Tech stack

- **n8n** (workflow automation)
- **Serper API** (Google search results)
- **OpenAI** (cold email writing)
- **Gmail** (sending and notifications)
- **Google Sheets** (lead database and logs)

## Workflow overview

| Stage | Nodes |
|---|---|
| Trigger | Schedule 7AM, Config |
| Lead discovery | Search Web (Serper), Extract Candidates |
| Deduplication | Get Existing Leads, Filter New Leads |
| Email finding | Scrape Homepage, Extract Site Email, Scrape Contact Page, Extract Contact Email |
| Outreach | Write Cold Email (OpenAI), Parse Email, Send Cold Email (Gmail) |
| Logging | Log Sent Lead, Log No-Email Lead |
| Reporting | Merge Results, Build Summary, Notify Email |

## Google Sheet setup

Create a Google Sheet with these columns in row 1, in this order:

| Column | Name | Description |
|---|---|---|
| A | Date | Date and time the lead was processed |
| B | Company | Business name found in search results |
| C | Website | Full website URL |
| D | Domain | Website domain, used to avoid duplicate leads |
| E | Country | Country code of the lead (e.g. FR, UK, CA) |
| F | Contact Name | Contact person's name, if found |
| G | Contact Email | Email address scraped from the site |
| H | Position | Contact's role, if found |
| I | Subject | AI-written email subject line |
| J | Email Body | AI-written cold email, in the lead's language |
| K | Email Source | Where the email was found (homepage or contact page) |
| L | Status | Result of the run (e.g. Email sent) |

The workflow checks the **Domain** column before contacting a lead, so the same business is never emailed twice.

## Setup

1. Import `workflow.json` into n8n (**Workflows → Import from file**)
2. Create credentials for: Serper, OpenAI, Gmail, Google Sheets
3. Create the Google Sheet using the columns above
4. Open the **Config** node and set your target countries, search keywords, and sheet ID
5. Test with **Execute Workflow**, then activate it

## Notes

- Use a warmed-up email address and keep daily volume low to protect sender reputation
- Follow cold email laws in your target countries (for example CAN-SPAM, GDPR, CASL) and include an opt-out line in every email

## Author

**Amarachi Owoh**, AI Automation Specialist
[LinkedIn](https://www.linkedin.com/in/amarachi-owoh-a5aa31299) · [GitHub](https://github.com/Amarachi147)
