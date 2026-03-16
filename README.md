# Meeting Assistant Agent

An automated meeting assistant built with n8n that reads meeting notes, extracts action items using Gemini AI, creates Trello cards, saves tasks to CSV, and sends a Slack notification.

## How It Works

Paste your meeting notes and run the workflow — everything else happens automatically.

## Nodes

**1. Manual Trigger**
Starts the workflow when you click "Execute Workflow" in n8n.

**2. Code in JavaScript (Meeting Notes)**
Contains the meeting transcript as text and passes it to the next node.

**3. HTTP Request (Gemini AI)**
Sends the meeting transcript to Google Gemini AI and asks it to extract all action items as a JSON array with title, description, assignee, and due_date fields.

**4. Code in JavaScript (Parse Response)**
Takes Gemini's response and converts it into individual task items that n8n can loop through one by one.

**5. Create a Card (Trello)**
Creates a Trello card for each task in the Meeting Tasks board under the To Do list, with the task title and description.

**6. Convert to File (CSV)**
Converts all the extracted tasks into a CSV file for record keeping.

**7. HTTP Request (Slack)**
Sends a notification to a Slack channel informing the team that new tasks have been added to Trello.

## Workflow

```
Manual Trigger
→ Meeting Notes (Code Node)
→ Gemini AI (HTTP Request)
→ Parse Tasks (Code Node)
→ Create Trello Cards
→ Save to CSV
→ Slack Notification
```

## Tools Used

- n8n (workflow automation)
- Google Gemini 2.5 Flash (AI)
- Trello API
- Slack Webhook

## Setup

1. Import `workflow.json` into n8n
2. Add your Gemini API key to the HTTP Request node URL
3. Add your Trello API Key and Token to the Trello node
4. Add your Slack Webhook URL to the final HTTP Request node
5. Click Execute Workflow
