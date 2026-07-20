# AI-Powered Intelligent News Aggregation and Newsletter Generation System

## 1. Project Overview

### Project Title

**AI-Powered Intelligent News Aggregation, Personalization, and Error Handling System using n8n**

### Project Description

This project is an advanced enhancement of an AI-powered automated workflow developed using n8n. The improved solution completely automates the lifecycle of news collection, data processing, content personalization, and error management using multiple specialized AI agents.

Instead of relying on a single, fragile monolithic workflow, the system is divided into **three independent but interconnected workflows**. Each workflow is responsible for a specific stage of the data pipeline, significantly improving scalability, maintainability, fault tolerance, and modularity.

---

## 2. Project Objectives

The system is designed to achieve the following capabilities:

* **Automated Collection:** Gather news dynamically from multiple online publications.
* **Data Sanitization:** Clean and transform messy HTML, RSS, and JSON payloads into structured data.
* **Centralized Storage:** Store extracted news in Google Sheets for downstream processing.
* **Intelligent Personalization:** Tailor news content specifically to the target audience's preferences.
* **AI Generation:** Draft professional, distribution-ready newsletters automatically.
* **Automated Monitoring:** Instantly detect workflow and AI execution failures.
* **Root-Cause Diagnosis:** Use AI to diagnose system errors and recommend clear fixes.
* **High Availability:** Improve overall system reliability using AI model fallback mechanisms.

---

## 3. System Architecture

The solution architecture consists of three decoupled workflows acting as independent operational layers:

```text
                    +----------------+
                    | Schedule Trigger|
                    +-------+--------+
                            |
                            v
              WORKFLOW 1 - DATA EXTRACTION
                            |
                            v
                  Google Sheets Database
                            |
                            v
              WORKFLOW 2 - CHIEF EDITOR
                            |
                            v
                Personalized Newsletter
                            |
                            v
                     Email Distribution

        Any Workflow Failure
                 |
                 v
          WORKFLOW 3 - ERROR HANDLER
                 |
                 v
      Error Diagnosis + Recommended Fix
```

### 📋 Workflow 1: Data Extraction Workflow

**Purpose:** Serves as the data ingestion layer. It collects news articles from multiple online publications, extracts the most crucial headlines, summarizes the articles using AI, and structures the data for storage.

* **Inputs:** RSS feeds, raw HTML pages, and JSON responses.
* **Monitored Sources:** *TechCabal, Nation Africa, Standard Media, Techweez, Smart Farmer, Kilimo News*.
* **Fault Isolation:** Uses multiple HTTP Request nodes configured with `Continue on Error`, ensuring a single broken source layout does not interrupt the remaining extractions.

#### Main Components:

* **Schedule Trigger:** Automatically runs at designated intervals to kick off the extraction pipeline.
* **HTTP Request Nodes:** Handles parallel, independent fetching to ensure strict error isolation across sources.
* **AI Data Cleaning Agents:** Individualized AI Agents assigned to each news source to clean raw HTML, strip out advertisements/navigation menus, identify the core article, and output a concise summary.
* **Structured Output Parser:** Standardizes the AI agent outputs into a unified JSON format:

```json
{
  "source": "Source Name",
  "headline": "Main Article Headline",
  "summary": "Concise summary of the article content."
}

```

* **Google Sheets Repository:** Appends the structured data using columns for *Date, Source, Headline, and Summary* to serve as the centralized processing database.

---

### 📝 Workflow 2: Chief Editor Workflow

**Purpose:** Transforms the raw, structured news repository into a highly personalized, human-reviewed newsletter.

* **Inputs:** Activated automatically via a Google Sheets Trigger whenever new rows are appended.
* **AI Editorial Agent:** Reads all compiled summaries, groups similar stories, strips duplicate data, and merges related articles into unified, coherent summaries to maximize readability.
* **Audience Personalization:** A secondary AI agent formats the newsletter structure, refines the tone, and generates clean HTML optimized for email layout distribution based on target subscriber profiles.
* **Human-in-the-Loop Approval:**
> Before mass publication, the workflow generates a preview draft and emails it to a human editor, pausing execution. Once the editor clicks approval, the newsletter is instantly distributed to subscribers.



---

### 🛠️ Workflow 3: AI Error Management Workflow

**Purpose:** Monitors and mitigates operational exceptions or AI failures across the system.

* **Trigger:** Webhook nodes capture failures instantly from Workflow 1 or Workflow 2.
* **AI Error Analysis:** A dedicated troubleshooting agent analyzes the raw error logs to produce:
* Error Summary & Root Cause
* Actionable Recommended Solution
* Priority Level & Prevention Strategy


* **Structured Auditing:** Diagnostic data is logged back into a dedicated Google Sheet for developer review.
* **Developer Notification:** Dispatches an immediate email containing the diagnostic breakdown to the engineering team for rapid debugging.

---

## 4. AI & Technology Stack

### AI Agent Architecture

The system intentionally avoids a single general-purpose model, utilizing specialized agents to simplify prompt management and maintain output quality:

| AI Agent | Core Responsibility |
| --- | --- |
| **Data Cleaner** | Sanitizes raw HTML/JSON and extracts clean, structured news tokens. |
| **Chief Editor** | Dedupes, merges, summarizes, and personalizes daily news components. |
| **Error Analyzer** | Automatically diagnoses workflow runtime failures and writes recommendations. |

### Technologies Used

* **n8n:** Workflow orchestration, node management, and automation logic.
* **Google Sheets:** Centralized lightweight data storage and relational triggers.
* **Mistral AI:** Primary Large Language Model (LLM) handling standard generation tasks.
* **OpenRouter:** AI infrastructure layer providing seamless model fallback routing.
* **Gmail / Webhooks:** Data distribution, human approval loops, and cross-workflow communications.

---

## 5. Key Improvements Over Previous Iterations

* **Modularity:** Transitioned from a single monolithic file into three independent micro-workflows.
* **Performance:** Introduced parallel extraction architectures to handle multiple endpoints concurrently.
* **Data Integrity:** Implemented localized AI cleaning layers to strip clutter before storage.
* **Quality Assurance:** Integrated a mandatory Human-in-the-Loop step ensuring editorial oversight.
* **Resilience:** Created a centralized AI-driven error handler paired with OpenRouter model fallback logic to isolate and self-diagnose system failures.

---

## Conclusion

This architecture demonstrates a production-ready approach to blending workflow automation with specialized artificial intelligence. By splitting core tasks into distinct pipelines for extraction, editorial synthesis, and automated error diagnostics, the system ensures a scalable, highly reliable, and self-correcting platform capable of delivering curated content with minimal manual overhead.
