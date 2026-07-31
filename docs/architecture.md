# 🏗️ System Architecture

The project implements an **event-driven AI automation architecture** using **n8n, Groq LLM, and GitHub REST API**.

The system automatically analyzes GitHub issues, performs AI-based classification, manages repository labels, generates AI-powered comments, and applies confidence-based automation decisions.

---

# High-Level Architecture

```
GitHub Issue Created
          |
          ↓
GitHub Webhook
          |
          ↓
n8n Workflow Engine
          |
          ↓
Issue Data Extraction
          |
          ↓
Groq AI Classifier
          |
          ↓
Structured Issue Analysis
          |
          ├── Category Detection
          |
          ├── Priority & Severity Analysis
          |
          ├── Confidence Scoring
          |
          ├── Label Generation
          |
          ├── Component Detection
          |
          └── Team Recommendation
          
          ↓

GitHub Automation Layer

          |
          ├── Fetch Existing Labels
          |
          ├── Create Missing Labels
          |
          ├── Apply Multiple Labels
          |
          ├── Generate AI Comment
          |
          ├── Confidence Evaluation
          |
          ├── Automatic Assignment
          |
          └── Human Review Workflow
```

---

# Component Details

## GitHub

Acts as the event source and issue management platform.

Responsible for:

- Issue creation
- Webhook events
- Repository labels
- Issue comments
- Issue assignment
- Review workflow


---

## n8n

Acts as the workflow orchestration layer.

Responsibilities:

- Receiving GitHub webhook events
- Processing issue data
- Connecting different automation components
- Calling external APIs
- Managing conditional workflows
- Executing confidence-based decisions


---

## Groq LLM

Provides AI-powered issue understanding and classification.

Responsible for:

- Issue category prediction
- Priority estimation
- Severity analysis
- Confidence score generation
- Label recommendation
- Affected component identification
- Development team suggestion
- Recommendation generation


---

## GitHub REST API

Used for automated repository operations.

Responsibilities:

- Fetch existing labels
- Create missing labels
- Apply multiple labels to issues
- Post AI-generated comments
- Assign issues to maintainers


---

# Design Decisions

## Event Driven Architecture

Instead of continuously polling GitHub for new issues, the system uses GitHub Webhooks.

Benefits:

- Real-time issue processing
- Reduced resource consumption
- Faster automation response
- Scalable event handling


---

## Modular Workflow Design

The automation pipeline is divided into independent workflow components:

```
Webhook Trigger
        |
        ↓
AI Analysis
        |
        ↓
Data Processing
        |
        ↓
Label Management
        |
        ↓
AI Communication
        |
        ↓
Confidence Routing
        |
        ↓
Automation Actions
```

Benefits:

- Easier debugging
- Better maintainability
- Independent feature development
- Reusable workflow components


---

# Confidence-Based Decision Architecture

The system uses AI confidence scores to control automation behavior.

```
AI Classification
        |
        ↓
Confidence Evaluation
        |
   ┌────┼────┐
   |    |    |
 ≥90 70-89 <70
   |    |    |
   ↓    ↓    ↓
Assign Review needs-review
```

### High Confidence (≥90%)

- Apply labels
- Generate AI comment
- Automatically assign issue

### Medium Confidence (70-89%)

- Apply labels
- Generate AI comment
- Require manual assignment

### Low Confidence (<70%)

- Add `needs-review` label
- Require human validation


---

# Future Architecture Improvements

## Multi-Agent System

Possible future design:

```
Classification Agent
        |
        ↓
Priority Agent
        |
        ↓
Root Cause Agent
        |
        ↓
Assignment Agent
```

Each agent would specialize in a specific issue management task.


---

## Analytics Pipeline

Future architecture:

```
GitHub
   |
   ↓
n8n Automation
   |
   ↓
Database / Google Sheets
   |
   ↓
Analytics Dashboard
```

Possible metrics:

- Issue categories
- Resolution time
- AI confidence accuracy
- Frequently occurring bugs
- Team workload


---

## Advanced AI Assistance

Future improvements:

- AI-generated suggested fixes
- Duplicate issue detection
- Automatic root cause analysis
- Code change recommendations
- Developer productivity analytics
