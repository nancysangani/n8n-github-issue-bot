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
"category":"Bug",
"priority":"High",
"comment":"Investigate backend failure."
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

# 5. Label Assignment

## Purpose

Automatically applies GitHub labels.

Example:

AI Output:

```
Category: Bug
```

Result:

```
GitHub Label:
bug
```

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

Planned:

- Multiple AI-generated labels
- Team-based assignment
- Issue analytics
- Notification systems
