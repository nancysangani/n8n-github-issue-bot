# ⚙️ Setup Guide

This guide explains how to configure and run the AI-Powered GitHub Issue Triage Automation locally using n8n.

---

# Prerequisites

Before starting, make sure you have:

- Docker installed
- Git installed
- GitHub account
- Groq API key
- GitHub repository with webhook access


Required tools:

| Tool | Purpose |
|------|---------|
| Docker | Run n8n locally |
| n8n | Workflow automation |
| GitHub API | Issue management |
| Groq API | AI classification |


---

# 1. Clone Repository

```bash
git clone https://github.com/nancysangani/n8n-github-issue-bot.git

cd n8n-github-issue-bot
```

---

# 2. Start n8n Using Docker

Run:

```bash
docker compose up -d
```

Verify container:

```bash
docker ps
```

n8n will be available at:

```
http://localhost:5678
```

---

# 3. Configure Groq API

Create a Groq API key and add it inside n8n credentials.

Navigate:

```
n8n
→ Credentials
→ Create Credential
→ Groq API
```

Add:

```
GROQ_API_KEY=<your_api_key>
```

---

# 4. Configure GitHub Authentication

Create a GitHub OAuth application or Personal Access Token.

Required permissions:

```
repo
issues
write:org (if required)
```

Add credentials:

```
n8n
→ Credentials
→ GitHub OAuth2 API
```

---

# 5. Import Workflows

Import workflow files from:

```
n8n/workflows/
```

Available workflows:

```
issue-trigger.json
ai-classifier.json
auto-label.json
auto-comment.json
auto-assign.json
```

---

# 6. Configure GitHub Webhook

In GitHub repository:

```
Settings
 → Webhooks
 → Add webhook
```

Configure:

Payload URL:

```
<your-n8n-production-webhook-url>
```

Content Type:

```
application/json
```

Events:

```
Issues
```

Enable:

```
Active
```

---

# 7. Test Workflow

Create a test issue:

Example:

```
Title:
Login page crashes

Description:
Users cannot login after password reset.
```

Expected result:

```
✓ AI classification
✓ Label added
✓ AI comment posted
✓ Issue assigned
```

---

# Deployment Notes

For production deployment:

- Use n8n cloud or hosted instance
- Configure environment variables
- Enable webhook security
- Configure error monitoring
