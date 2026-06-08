# Automated-Task-Distribution-EOD-Worklog-Consolidator


An asynchronous, two-way automation ecosystem built in n8n that eliminates administrative project management overhead. The system uses Large Language Models (LLMs) to automatically parse assignment files and distribute personalized tasks, while simultaneously hosting an active listener pipeline to ingest and organize end-of-day (EOD) team worklogs into a centralized master database.


---

## 🚀 How It Works

The system is split into two independent, decoupled pipeline workflows:

### 1. The Assignment Distribution Pipeline (Top Workflow)
* **Trigger:** Manually executed when a project sprint kicks off.
* **Ingestion:** Downloads a raw project specification PDF or blueprint from a dedicated Google Drive folder.
* **AI Parsing:** Passes the document text to the **Google Gemini Model**. A custom **Task Parser** structures the LLM's output into strict JSON format, mapping out specific modules, deadlines, and team member email addresses.
* **Distribution:** The **Split Tasks** node breaks the array into separate items, prompting Gmail to send individualized, targeted milestone emails to each team member.

### 2. The EOD Worklog Consolidation Pipeline (Bottom Workflow)
* **Trigger:** An active **Gmail Trigger** node that listens for incoming daily updates from team members.
* **Extraction:** Aggregates incoming emails, extracts unstructured worklogs, and standardizes them into clean metrics (Date, Developer, Completed Tasks, Blockers).
* **Database Sync:** The workflow separates data lines and uses an `appendOrUpdate` action against a master Excel/Google Sheet. This ensures updates to existing sprint elements modify rows safely, while net-new entries are safely appended without duplicate row errors.

---

## 🛠️ Tech Stack & Integrations

* **Automation Core:** n8n (Workflow Orchestration)
* **AI Orchestration:** Google Gemini LLM Engine & Structured Output Parsers
* **Communication & Storage:** Gmail API, Google Drive API
* **Database/Tracking:** Google Sheets / Microsoft Excel

---
