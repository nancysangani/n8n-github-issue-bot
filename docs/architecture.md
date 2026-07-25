# 🏗️ System Architecture

The project implements an event-driven AI automation architecture using n8n.

---

# High-Level Architecture

```
              GitHub Repository

                    |
                    |
             Issue Created Event

                    |
                    ↓

             GitHub Webhook

                    |
                    ↓

              n8n Workflow Engine

                    |
                    ↓

             Groq LLM Analysis

                    |
                    ↓

          AI Decision & Classification

                    |
          ---------------------
          |        |          |
          ↓        ↓          ↓

       Labels   Comments   Assignment

                    |
                    ↓

             Updated GitHub Issue
```

---

# Component Details

## GitHub

Responsible for:

- Issue creation
- Webhook events
- Labels
- Comments
- Assignment


---

## n8n

Acts as the workflow orchestration layer.

Responsibilities:

- Event handling
- Data transformation
- API communication
- Automation execution


---

## Groq LLM

Responsible for:

- Issue understanding
- Category prediction
- Priority estimation
- Recommendation generation


---

# Design Decisions

## Event Driven Architecture

Instead of polling GitHub periodically, the system uses webhooks.

Benefits:

- Real-time processing
- Lower resource usage
- Faster response


---

## Modular Workflow Design

The automation is divided into reusable components:

```
Trigger
AI Analysis
Routing
Actions
```

Benefits:

- Easier debugging
- Better maintainability
- Independent feature development


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
Assignment Agent
```

---

## Analytics Pipeline

Future:

```
GitHub
 |
 n8n
 |
 Google Sheets / Database
 |
 Dashboard
```
