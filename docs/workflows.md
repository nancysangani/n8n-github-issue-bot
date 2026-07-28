# 🔄 Workflow Documentation

This document explains the complete AI GitHub Issue Triage workflow.

---

# Workflow Overview

```
GitHub Issue Created
          |
          ↓
GitHub Webhook Trigger
          |
          ↓
Extract Issue Information
          |
          ↓
Groq AI Classification
          |
          ↓
Parse AI Response
          |
          ↓
Category Routing
          |
          ↓
GitHub Automation Actions
```

---

# 1. GitHub Trigger

## Purpose

Receives GitHub issue events through webhook integration.

Triggered when:

```
issues.opened
```

Payload contains:

```json
{
"title":"",
"body":"",
"issue_number":"",
"repository":""
}
```

---

# 2. Edit Fields Node

## Purpose

Extracts required information from GitHub payload.

Extracted fields:

```json
{
"title":"",
"body":"",
"issue_number":"",
"owner":"",
"repository":""
}
```

This simplifies downstream workflow processing.

---

# 3. Groq AI Classification

## Purpose

Uses LLM-based analysis to classify issues.

Input:

```
Issue title
Issue description
```

Output:

```json
{
  "category": "Bug",
  "priority": "High",
  "labels": [
    "bug",
    "backend",
    "api"
  ],
  "comment": "Investigate backend failure."
}
```

Supported categories:

- Bug
- Feature
- Technical
- Documentation
- UI/UX
- Performance
- Security
- Question

---

# 4. Switch Node

## Purpose

Routes issues based on AI category.

Example:

```
Bug
 ↓
Bug Label Node
```

```
Feature
 ↓
Feature Label Node
```

This enables category-specific automation.

---

# 5. Intelligent Label Management

The label automation workflow performs the following steps:

1. AI generates multiple labels for the issue.
2. Existing repository labels are retrieved from GitHub.
3. Missing labels are identified.
4. Missing labels are automatically created.
5. Custom colors and descriptions are assigned to newly created labels.
6. All generated labels are applied to the GitHub issue.
7. The workflow continues with AI comment generation and automatic assignment.

---

## Workflow Flow

```
GitHub Issue
      ↓
Groq AI Analysis
      ↓
Generate Category, Priority & Labels
      ↓
Retrieve Existing Repository Labels
      ↓
Identify Missing Labels
      ↓
Create Missing Labels (if required)
      ↓
Apply Multiple Labels
      ↓
Generate AI Comment
      ↓
Assign Issue
```

### Key Capabilities

- Supports multiple AI-generated labels.
- Automatically creates repository labels when they do not exist.
- Assigns predefined colors and descriptions to newly created labels.
- Prevents duplicate label creation by checking existing repository labels.

---

# 6. AI Comment Generation

The workflow posts an AI-generated analysis.

Example:

```
AI Issue Analysis

Category:
Authentication

Priority:
High

Recommendation:
Investigate server-side login failure.
```

---

# 7. Automatic Assignment

The workflow assigns issues dynamically.

Current strategy:

```
Repository Owner
        ↓
GitHub Assignee
```

Expression:

```javascript
{{$node["Edit Fields"].json.owner}}
```

---

# Future Workflow Improvements

Planned enhancements:

- Smarter AI prioritization with confidence scores
- Team-based assignment strategies
- Discord / Slack notifications
- Google Sheets issue analytics
- Production logging and monitoring
- Duplicate issue detection
- Suggested fixes and root-cause analysis

---

# Workflow Summary

The workflow provides an end-to-end AI-powered GitHub issue management pipeline by:

- Receiving issue events through GitHub Webhooks.
- Analyzing issue content using Groq LLM.
- Generating category, priority, and multiple labels.
- Automatically creating missing repository labels.
- Applying labels, posting AI-generated comments, and assigning issues to maintainers.

This modular architecture enables scalable, event-driven issue triage with minimal manual intervention.
