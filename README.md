# 🚀 AI-Powered B2B Lead Enrichment Workflow

An automated ETL (Extract, Transform, Load) pipeline built with **n8n** that scrapes company websites and uses Large Language Models (LLMs) to extract structured business intelligence for lead generation.

![n8n](https://img.shields.io/badge/n8n-Workflow-orange?style=flat-square) ![AI](https://img.shields.io/badge/AI-Model%20Agnostic-blueviolet?style=flat-square) ![Google Sheets](https://img.shields.io/badge/Google-Sheets-green?style=flat-square)

> **Note:** Read this in Ukrainian: [Українська версія](./README.uk.md)

## 📌 Project Overview

**The Challenge:** Sales teams spend hours manually opening websites to understand what a company does, its business model, and whether it fits their Ideal Customer Profile (ICP).

**The Solution:** This n8n workflow automates the research process:
1.  **Reads** a list of URLs from Google Sheets.
2.  **Scrapes** the raw HTML content (handling basic anti-bot headers).
3.  **Analyzes** the content using AI (Gemini, OpenAI, Claude, etc.).
4.  **Enriches** the data with structured tags and personalized outreach lines.
5.  **Updates** the Google Sheet automatically.

---

## ⚙️ Features

* **Smart Scraping:** Includes custom User-Agent headers to mimic a real browser and bypass basic blocking.
* **Model Agnostic:** While configured for **Google Gemini 1.5 Pro** (cost-effective), you can easily swap the AI node for **GPT-4**, **Claude 3**, or even local models via **Ollama**.
* **JSON Cleaning:** Automated script to sanitize AI responses, preventing JSON parsing errors.
* **Error Handling:** The workflow continues processing the list even if one website fails to load.

---

## 🛠 Prerequisites & Setup

### 1. Google Sheets Configuration
Create a new Google Sheet. The **first row** must contain the following headers exactly:

| Column Header | Description |
| :--- | :--- |
| `Website URL` | **Input.** Paste your list of domains here (e.g., https://example.com). |
| `Business Model` | Output. (e.g., B2B, B2C). |
| `Role` | Output. (e.g., Platform, Agency). |
| `Description` | Output. 1-sentence summary. |
| `Market` | Output. (Global, EU, LATAM, etc.). |
| `Audience Needs` | Output. (Yes/No). |
| `Outreach` | Output. Personalized cold email opener. |
| `Confidence` | Output. AI confidence score. |

**Important:** Share this sheet with your Google Service Account email (Editor access).

### 2. n8n Setup
1.  **Import:** Download the `workflow.json` from this repository and import it into n8n.
2.  **Credentials:**
    * **Google Sheets:** Set up a generic Google Cloud Service Account credential.
    * **AI Model:** Add your API Key for Gemini (Google AI Studio) or your preferred provider.

### 3. Customizing the AI Model
You are not locked into Gemini. To use GPT-4 or Claude:
1.  Delete the "Gemini Chat" node.
2.  Add an "OpenAI" or "Anthropic" node.
3.  Copy the **System Prompt** from the original node description.
4.  Connect it between the "Scraper" and "Clean JSON" nodes.

---

## 🚀 How to Run

1.  Fill the `Website URL` column in your Google Sheet with target domains.
2.  Open the workflow in n8n.
3.  Click **Execute Workflow**.
4.  Watch the Google Sheet populate in real-time!

## 📝 License

This project is open-source. Feel free to fork and adapt it to your specific lead generation needs.