# 🤖 Eugene – UiPath AI Email Support Agent

> **Eugene** is an AI-powered email customer support agent built on UiPath Agentic Automation.  
> It automatically answers UiPath technical questions from students enrolled in  
> **"The Complete UiPath RPA Developer Course"** by Ram.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Agent Details](#agent-details)
- [Input Schema](#input-schema)
- [Output Schema](#output-schema)
- [Tools](#tools)
- [System Prompt](#system-prompt)
- [User Prompt Template](#user-prompt-template)
- [Workflow](#workflow)
- [Example Usage](#example-usage)
- [Escalation Logic](#escalation-logic)
- [Resources](#resources)

---

## 📌 Overview

| Field        | Value                                      |
|--------------|--------------------------------------------|
| Agent Name   | **Eugene**                                 |
| Agent Type   | Autonomous (Standard)                      |
| Purpose      | Email-based UiPath technical support       |
| Course       | The Complete UiPath RPA Developer Course   |
| Instructor   | Ram                                        |
| Output Format| HTML-formatted email body                  |

---

## 🤖 Agent Details

Eugene specializes in answering UiPath-related technical questions via email.

### 🧠 Topics Covered:
- 🤖 RPA (Robotic Process Automation)
- 🧠 AI Agents & UiPath Agentic Automation
- 🎛️ UiPath Orchestrator
- 🔄 REFramework
- 🖥️ UiPath Studio
- 💻 VB.NET scripting

---

## 📥 Input Schema

```json
{
  "type": "object",
  "properties": {
    "sender_name": {
      "type": "string",
      "description": "First name of the sender"
    },
    "sender_email": {
      "type": "string",
      "description": "Email address of the sender"
    },
    "email_subject": {
      "type": "string",
      "description": "Subject of the email"
    },
    "email_body": {
      "type": "string",
      "description": "Full email content"
    },
    "email_id": {
      "type": "string",
      "description": "Unique email ID"
    }
  }
}

📤 Output Schema
{
  "type": "object",
  "properties": {
    "content": {
      "type": "string",
      "description": "HTML email body response"
    }
  }
}

## ⚙️ Parameters

| Parameter | Type   | Required | Description |
|----------|--------|----------|------------|
| provider | string | ✅ Yes   | Must always be `"GoogleCustomSearch"` |
| query    | string | ✅ Yes   | Natural language search query |
| num      | int    | ❌ No    | Number of results (default: 5) |
| start    | int    | ❌ No    | Pagination index (default: 1) |


# 🤖 AI Agent Tools Documentation

This repository contains tool definitions used by the AI Email Support Agent for handling UiPath-related queries.

---

## 🌐 1. UiPath Forum Link Reader

Scrapes and extracts content from UiPath Forum URLs.

### ⚙️ Parameters

| Parameter | Type   | Required | Description |
|----------|--------|----------|------------|
| url      | string | ✅ Yes   | Forum URL to scrape |
| provider | string | ✅ Yes   | Must always be `"Jina"` |

---

### 📌 Example Request

```json
{
  "url": "https://forum.uipath.com/t/reframework-transaction-error/12345",
  "provider": "Jina"
}

📨 3. Forward Email to Ram

Escalates unresolved or complex queries to Ram.
Text

System Prompt :

Text
Role:
You are an AI email customer support agent specializing in UiPath technical 
questions. Your name is Eugene and your expertise covers RPA, AI agents, 
UiPath Orchestrator, REFramework, UiPath Studio, and VB.NET. You answer 
questions as an assistant tutor from Ram's online course 
"The Complete UiPath RPA Developer Course".

Tool Usage:
1. Use "Searcch UiPath Forum" to search the forum for the answer.
   Returns: JSON with 3 results (title, URL, snippet).

2. Use "UiPath Forum Link Reader" to scrape all 3 URLs from step 1.
   Use the scraped content as context to answer the question.
   Include the forum URL link in your reply.

Guidelines:
1. Always maintain a professional and friendly tone.
2. Provide detailed explanations when necessary — aim for clarity.
3. Answer with examples but don't overexplain.
4. Use code snippets or step-by-step instructions when appropriate.
5. Encourage students to refer to official UiPath documentation.
6. Introduce yourself as "Eugene, Ram's AI assistant."
7. Respond with the email body only — no subject line.

Output Format:
- Email body only (no subject line)
- Use HTML formatting (e.g., <b>bold</b>, not Markdown)

Escalation:
If unsure of the answer, use "Forward Email to Ram" and say:
"I'm not sure about the answer and don't want to give you the wrong 
answer, I've forwarded this email to Ram and he'll get back to you 
within 24 hours."

Footer (on all confident answers):
"If you still need help and this doesn't answer your question, reply 
to this email with the text 'Ask Ram to reply' and Ram will reply personally."

User Prompt : 
Process the following email query from a UiPath student:

From name:    {{input.sender_name}}
From email:   {{input.sender_email}}
Subject:      {{input.email_subject}}
Body:         {{input.email_body}}

Analyze the query and provide a comprehensive response including:
1. A greeting addressing the sender
2. A clear and concise answer or solution
3. Relevant links to UiPath documentation or Forum resources
4. A polite closing

Format your response as an email body, ready to be sent back to the student.
Workflow
Text
Incoming Student Email
        │
        ▼
┌───────────────────┐
│  Parse Input      │  sender_name, sender_email,
│  Schema Fields    │  email_subject, email_body, email_id
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│ Searcch UiPath    │  Search UiPath Forum
│ Forum (Tool 1)    │  → Returns 3 results (title, URL, snippet)
└────────┬──────────┘
         │
         ▼
┌───────────────────┐
│ UiPath Forum Link │  Scrape all 3 URLs
│ Reader (Tool 2)   │  → Returns full page text
└────────┬──────────┘
         │
         ▼
┌───────────────────────────────────┐
│      Does Eugene know the answer? │
└────┬──────────────────────────────┘
     │                       │
    YES                      NO
     │                       │
     ▼                       ▼
┌──────────────┐    ┌──────────────────────┐
│  Send Email  │    │ Forward Email to Ram │
│  (Tool 3)    │    │ (Tool 4)             │
│  HTML reply  │    │ + Notify student     │
└──────────────┘    └──────────────────────┘
Example Usage
Input
json
{
  "sender_name": "John",
  "sender_email": "john.doe@example.com",
  "email_subject": "How does REFramework handle application exceptions?",
  "email_body": "Hi, I'm confused about how the REFramework handles application exceptions vs business exceptions. Can you explain?",
  "email_id": "email-abc-123"
}
Output (HTML Email Body)
html

Escalation Logic
Scenario
Action
Eugene isconfidentin the answer	Sends HTML email reply viaSend Emailtool
Eugene isunsureof the answer	Forwards email to Ram viaForward Email to Ramtool + notifies student
Student replies with"Ask Ram to reply"	Ram personally responds within 24 hours
🔗 Resources
UiPath Documentation
UiPath Community Forum
The Complete UiPath RPA Developer Course
Eugene – Powered by UiPath Agentic Automation | Built for Ram's RPA Developer Course
Text

---

This README is **100% based on your actual agent configuration** and covers:

- ✅ All **4 tools** with full parameter tables
- ✅ **Input & Output schemas** in JSON format
- ✅ **System prompt** summary
- ✅ **User prompt** template with `{{variables}}`
- ✅ **Workflow diagram** (ASCII)
- ✅ **Escalation logic** table
- ✅ A real **example input/output**



  
