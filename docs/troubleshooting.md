# 🛠️ Troubleshooting Guide

Common issues and solutions while running the AI GitHub Issue Automation workflow.

---

# 1. Webhook Returns 404

## Problem

GitHub webhook shows:

```
Response 404
```

## Cause

Using n8n test webhook URL instead of production webhook URL.

## Solution

Use:

```
/webhook/
```

instead of:

```
/webhook-test/
```

Activate the workflow before testing.

---

# 2. Webhook Returns 401 Unauthorized

## Problem

GitHub receives:

```
Response 401
```

## Cause

Webhook secret mismatch.

## Solution

Ensure GitHub webhook secret matches n8n trigger configuration.

---

# 3. AI Returns Invalid Categories

## Problem

Switch node does not route output.

Example:

```
Technical Issue
```

instead of:

```
Technical
```

## Solution

Update AI prompt with fixed category values.

Allowed:

```
Bug
Feature
Technical
Documentation
UI/UX
Performance
Security
Question
```

---

# 4. Labels Are Not Added

## Problem

Workflow executes but GitHub label is missing.

## Check:

- GitHub credentials
- Repository permissions
- Label name spelling

Example:

```
bug
```

must exactly match GitHub label.

---

# 5. AI Comment Not Created

## Problem

Issue label works but comment does not appear.

## Solution

Verify:

- GitHub OAuth permissions
- Comment node mapping
- Issue number expression

---

# 6. Assignment Fails

## Problem

Issue is not assigned.

## Solution

Verify assignee expression:

```javascript
{{$node["Edit Fields"].json.owner}}
```

The username must have repository access.

---

# Debugging Workflow

Recommended debugging order:

```
GitHub Trigger
        ↓
Edit Fields
        ↓
AI Response
        ↓
Code Parser
        ↓
Switch Output
        ↓
GitHub Actions
```

Check each node execution output individually.

---

# Production Recommendations

For production deployment:

- Enable workflow error notifications
- Store execution logs
- Add monitoring
- Secure webhook endpoints
