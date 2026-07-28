# 🤖 AI GitHub Issue Automation

![License](https://img.shields.io/badge/license-MIT-green)
![n8n](https://img.shields.io/badge/n8n-Workflow-orange)
![Groq](https://img.shields.io/badge/Groq-LLM-blue)
![GitHub API](https://img.shields.io/badge/GitHub-API-black)

An AI-powered GitHub issue triage and automation system built using **n8n workflows** and **Groq LLM**.

The system automatically analyzes newly created GitHub issues, classifies them using AI, applies relevant labels, generates helpful comments, and assigns issues to maintainers — reducing manual issue management effort.

---

## ✅ AI Issue Classification

Uses the Groq LLM to analyze GitHub issue titles and descriptions.

The AI automatically determines:

- Issue category
- Priority level
- Multiple relevant labels
- AI-generated recommendation

Supported categories include:

- Bug
- Feature
- Technical
- Documentation
- UI/UX
- Performance
- Security
- Question

---

## ✅ Automatic GitHub Labels

Based on AI classification, issues are automatically labeled.

Examples:

```
Bug → bug
Feature → feature
Security → security
Documentation → documentation
```


## ✅ AI Generated Issue Comments

The workflow automatically posts an AI-generated analysis comment on the GitHub issue.

Example:

```
🤖 AI Issue Analysis

Category: Authentication

Priority: High

Recommendation:
Investigate server-side issue causing login failure.
```


## ✅ Automatic Issue Assignment

Issues are automatically assigned to the repository maintainer after classification.

The assignee is dynamically fetched from the repository owner information, making the workflow reusable across repositories.


## ✅ Event Driven Automation

The complete pipeline runs automatically whenever a new GitHub issue is created using GitHub Webhooks.


---

# 🏗️ Architecture

```
GitHub Issue Created
          │
          ▼
GitHub Webhook Trigger
          │
          ▼
Extract Issue Data
          │
          ▼
Groq AI Classification
          │
          ▼
Parse AI Response
          │
          ▼
Generate Multiple Labels
          │
          ▼
Fetch Existing Repository Labels
          │
          ▼
Create Missing Labels (if required)
          │
          ▼
Apply Multiple Labels
          │
          ▼
Generate AI Comment
          │
          ▼
Assign Issue
```

---

# 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| n8n | Workflow automation engine |
| Groq LLM | AI issue classification |
| GitHub API | Issue management and automation |
| GitHub Webhooks | Event triggering |
| Docker | Local deployment |
| JavaScript | Workflow data processing |


---

# 📂 Project Structure

```
ai-github-issue-automation/

│
├── n8n/
│   └── workflows/
│       ├── issue-trigger.json
│       ├── ai-classifier.json
│       ├── auto-label.json
│       ├── auto-comment.json
│       └── auto-assign.json
│
├── docs/
│   ├── architecture.md
│   ├── workflows.md
│   ├── setup.md
│   └── troubleshooting.md
│
├── images/
│   └── workflow screenshots
│
├── README.md
└── docker-compose.yml
```

---

# ⚙️ Workflow Components

| Component | Description |
|-|-|
| GitHub Trigger | Receives issue events |
| Edit Fields | Extracts issue information |
| Groq AI | Classifies issues using LLM |
| Code Parser | Parses AI response |
| Label Manager | Generates, creates, and applies labels |
| GitHub Comment Node | Posts AI analysis |
| GitHub Assign Node | Assigns repository owner |


---

# 📊 Current Progress

## Completed

- [x] GitHub webhook integration
- [x] Issue data extraction
- [x] Groq LLM integration
- [x] AI issue classification
- [x] Category-based routing
- [x] Multiple AI-generated labels
- [x] Dynamic GitHub label creation
- [x] Automatic label colors
- [x] Automatic label descriptions
- [x] AI generated comments
- [x] Automatic issue assignment


## Upcoming

- [ ] Smarter AI classification
- [ ] Discord notifications
- [ ] Google Sheets integration
- [ ] Production logging
- [ ] Error monitoring


---

## 🔄️ Features

### 🤖 AI Issue Classification
- Analyzes GitHub issues using Groq LLM
- Automatically detects:
  - Category
  - Priority
  - Relevant labels
  - Issue summary

### 🏷️ Intelligent Label Management
- Generates multiple labels using AI
- Checks existing repository labels
- Automatically creates missing labels
- Supports custom label:
  - Colors
  - Descriptions

### 💬 Automated Issue Communication
- Generates AI-powered comments
- Provides issue analysis directly on GitHub

### 👤 Automatic Issue Assignment
- Assigns issues automatically to maintainers

### 🔄 Event Driven Automation
- GitHub webhook based workflow
- Real-time issue processing through n8n


---

# 🧪 Example

Input GitHub Issue:

```
Title:
Login page crashes

Description:
Users cannot login after password reset.
Getting server error.
```

AI Output:

```json
{
  "category":"Bug",
  "priority":"High",
  "labels":[
      "bug",
      "backend",
      "api"
  ],
  "comment":"..."
}
```

Result:

```
Labels:
bug
backend
api

Comment:
AI generated analysis

Assignee:
Repository owner
```

---

# 🎬 Demo

When a new GitHub issue is created:

1. The GitHub webhook triggers the n8n workflow.
2. Groq LLM analyzes the issue.
3. Relevant labels are generated.
4. Missing labels are created automatically.
5. Labels are applied to the issue.
6. An AI-generated comment is posted.
7. The issue is automatically assigned to the maintainer.

---

# 📸 Workflow Preview

![AI GitHub Issue Automation Workflow](docs/images/workflow.png)
---

# 🚀 Setup

See:

- [Setup Guide](docs/setup.md)
- [Workflow Documentation](docs/workflows.md)
- [Architecture](docs/architecture.md)
- [Troubleshooting](docs/troubleshooting.md)


---

# 🎯 Project Highlights

- Built an end-to-end AI automation pipeline using n8n
- Integrated LLM-based decision making into GitHub workflows
- Automated repetitive issue management tasks
- Designed reusable event-driven architecture
- Implemented AI-assisted developer workflow automation


---

## 🙏 Acknowledgements

This project uses:

- n8n for workflow automation
- Groq LLM for AI-powered issue analysis
- GitHub REST API for repository automation

---

# 📄 License

This project is licensed under the MIT License.
