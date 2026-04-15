# 🤖 Robot 6: Email Customer Support Agentic AI (UiPath Eugene)

## 📌 Overview

This project demonstrates an Agentic AI-powered email customer support system built using UiPath. The AI agent, named **"UiPath Eugene"**, automatically responds to technical UiPath-related queries received via email.

The system uses event-driven automation, AI decision-making, and tool-based knowledge retrieval to provide fast and accurate responses. If the agent is not confident or the user requests human support, it escalates the query.

---

## 🚀 Key Features

- Instant email replies within seconds  
- Event-based trigger using Gmail webhook  
- AI-powered response generation using LLM  
- UiPath Forum search and scraping capability  
- Context-aware answers using grounded data  
- Human escalation when required  
- HTML formatted email responses  
- Performance evaluation using scoring system  

---

## 🏗️ Architecture
Gmail Inbox (Trigger)
↓
UiPath Maestro (BPMN Process)
↓
AI Agent (LLM)
↓
Decision Engine
↙ ↘
Auto Reply Escalate to Human
↓
Send Email Response
---

## ⚙️ Workflow Explanation

### 1. Email Trigger
- Process starts when a new email is received in Gmail
- Trigger is configured using webhook

### 2. Email Parsing
- Extract sender, subject, and body
- Detect keywords like "Hi Eugene" or "Speak to human"

### 3. AI Processing
- AI agent understands the query
- Uses tools to search and scrape UiPath Forum
- Generates response using grounded context

### 4. Decision Logic
- High confidence → Auto reply
- Low confidence or user request → Escalation

### 5. Response Handling
- Sends HTML formatted response
- Or forwards email to human agent

---

## 🧠 AI Agent Capabilities

- Natural Language Understanding  
- Context grounding  
- Tool usage (search + scraping)  
- Prompt-based behavior control  
- Confidence-based decision making  

---

## 🛠️ Tech Stack

- UiPath Studio Web  
- UiPath Maestro (BPMN)  
- UiPath Orchestrator  
- OpenAI LLM  
- Gmail API / Webhook  
- HTML Email Templates  

---

## 📹 Demo

Add your demo video link here

---

## 📚 Skills Demonstrated

- Agentic AI workflow design  
- BPMN process modeling  
- Prompt engineering  
- Context grounding  
- Gmail integration  
- Decision-based automation  
- HTML email formatting  
- Deployment using Orchestrator  
- Debugging and testing  
- LLM evaluation and scoring  

---

## 🔄 Escalation Logic

| Condition | Action |
|----------|--------|
| High confidence | Auto reply |
| Low confidence | Escalate |
| "Speak to human" | Immediate escalation |

---

## 📈 Future Enhancements

- Multi-language support  
- Integration with ServiceNow / Zendesk  
- Feedback-based learning  
- Sentiment analysis  
- Omnichannel support (chat + voice)  

---

## 📬 Sample Email Flow

**User Email:**Hi Eugene, how to use selectors in UiPath?


**Bot Response:**

Hello [User Name],

Here’s how you can use selectors in UiPath...

If you need more help, feel free to reply.

Best Regards,
UiPath Eugene 🤖


---

## 📌 Conclusion

This project demonstrates how Agentic AI combined with RPA can automate customer support efficiently. It reduces response time, improves accuracy, and ensures seamless human fallback when needed.
