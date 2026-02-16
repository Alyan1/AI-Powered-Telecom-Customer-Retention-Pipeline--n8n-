# 🚀 (n8n)-Powered Telecom Customer Retention Pipeline

![n8n](https://img.shields.io/badge/n8n-Workflow_Automation-FF6600?style=for-the-badge&logo=n8n)
![Google Gemini](https://img.shields.io/badge/Google_Gemini-2.5_Flash_Lite-4285F4?style=for-the-badge&logo=google)
![Telegram API](https://img.shields.io/badge/Telegram-Bot_API-2CA5E0?style=for-the-badge&logo=telegram)

## 📉 The Business Problem
In the telecommunications sector, manual customer support triage leads to high churn rates. When an angry customer submits a network or billing complaint, it often sits in a generic queue for 24 to 48 hours. By the time a human agent reads the ticket and realizes the customer is a high flight risk, the customer has already ported their number to a competitor. Traditional support systems are reactive, not proactive.

## 💡 The Solution
I architected an autonomous, end-to-end triage pipeline for enterprise telecom providers that reduces support classification time from days to seconds. 

## 🎯 Use Case Scenario
**Meet "Usama" (The Flight Risk):** Usama's 4G connection drops constantly. He is furious and submits a support ticket threatening to switch to a rival telecom company. 
* **Without this pipeline:** Usama waits 2 days for an email reply. He gets frustrated and switches networks.
* **With this pipeline:** Within 3 seconds of clicking "Submit", the AI reads his angry intent, grades him a 10/10 flight risk, and instantly pings the Telecom Retention Team on Telegram. A human agent calls Usama 5 minutes later with a free 5GB data apology. Usama is retained.

## ⚙️ How It Works (The Architecture)

*(Drag and drop your full n8n workflow canvas screenshot right here!)*

The workflow executes in 4 distinct engineering phases:

### 1. Data Ingestion (Google Workspace)
A live Google Form captures the customer's support ticket, name, phone number, and email. An n8n Google Sheets trigger securely listens for this payload via OAuth2 integration.

### 2. The AI Brain (Google Gemini 2.5)
The raw text is pushed to a Google Gemini model programmed as an Expert Triage Architect. Through strict prompt engineering, the LLM analyzes the text and outputs a structured JSON response containing:
* **Intent Classification:** (e.g., Network, Billing, General)
* **Sentiment Analysis:** (e.g., Negative, Neutral, Positive)
* **Churn Risk Score:** An integer from 1 to 10 predicting the likelihood of the customer leaving the network.

### 3. Logic Routing (n8n IF Node)
The pipeline programmatically parses the AI's JSON output. If the `Churn_Risk_Score` is 8 or higher, it routes to the High-Risk branch. If it is 7 or lower, it routes to the Routine branch.

### 4. Automated Execution
* **🔴 High-Risk Action (Telegram API):** Bypasses standard queues and instantly sends an enterprise alert to the Retention Team's Telegram channel with the customer's phone number, issue intent, and an AI-generated retention offer.

*(Drag and drop your Telegram bot screenshot right here!)*

* **🟢 Routine Action (SMTP Email):** Connects to secure SMTP servers to automatically email the customer a polite, AI-contextualized digital receipt to assure them their issue is being reviewed by the standard support team.

*(Drag and drop your Email screenshot right here!)*

## 📊 The Impact
* **Zero-Minute Triage:** Eliminated manual ticket reading and classification.
* **Proactive Churn Mitigation:** Empowers retention staff to contact high-risk flight threats within minutes of complaint submission, actively saving company revenue.
* **Automated CX Communication:** Routine customers receive instant automated acknowledgments, reducing the manual email workload for human agents by 100% on low-tier tickets.

## 🛠️ How to Replicate
1. Clone this repository and import the `.json` file into your n8n instance.
2. Configure your Google Cloud OAuth2 credentials for the Sheets trigger.
3. Provision a Google AI Studio API key and insert it into the Gemini node.
4. Set up a Telegram Bot via `@BotFather` and add your unique Chat ID and Bot Token to the routing branch.
