# 🏢 CRE AI Underwriting & Risk Analysis Dispatcher

An automated end-to-end pipeline built using **n8n** and **Google Gemini AI** to extract, evaluate, log, and dispatch Commercial Real Estate (CRE) underwriting documents.

This workflow automatically processes property PDFs from Google Drive, calculates key underwriting metrics (DSCR, NOI, Occupancy), stores the audit log in Google Sheets, and generates dynamic HTML Investment Memos sent via Gmail based on the risk classification.

---

## 📌 Features & Key Capabilities

- 🔄 **Automated Document Retrieval**: Periodically scans a designated Google Drive folder (`01_Underwriting_Input`) for new documents.
- 📄 **PDF Text Extraction & Filtering**: Validates incoming files and extracts raw text from PDF proposals.
- 🧠 **AI-Powered Risk Analysis (Google Gemini)**: 
  - Extracts key metrics: *Property Name*, *Net Operating Income (NOI)*, *Debt Coverage Ratio (DSCR)*, and *Risk Factors*.
  - Applies a strict numerical **Decision Matrix**:
    - **Rejected**: DSCR < 0.50x OR Occupancy < 60% OR Tenant Bankruptcy.
    - **Approved**: DSCR ≥ 1.25x AND Occupancy ≥ 90%.
    - **Review Required**: Any margin in-between (e.g., DSCR between 0.50x and 1.24x).
- 📊 **Centralized Portfolio Tracking**: Automatically appends extracted metrics and recommendations into a **Google Sheets** master tracking document.
- 📁 **File Organization**: Moves processed files from the input queue to `02_Underwriting_Processed`.
- ✉️ **Dynamic Email Dispatcher**:
  - Uses AI Agents to draft tailored, executive-level HTML email memos.
  - Generates custom color-coded badges (**Approved** 🟢 / **Review Required** 🟠 / **Rejected** 🔴).
  - Sends notifications directly via **Gmail** to the investment committee.

---

## 🛠️ Tech Stack & Integrations

- **Automation Platform:** [n8n](https://n8n.io/)
- **LLM / AI Model:** Google Gemini (`gemini-3.1-flash-lite`) via LangChain / n8n AI Nodes
- **Cloud Storage:** Google Drive API
- **Database / Logging:** Google Sheets API
- **Notification:** Gmail API

---

## 📐 Workflow Architecture & Data Flow
