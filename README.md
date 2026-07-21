Technical Documentation
AI-Powered Intelligent News Aggregation, Personalization and Error Management System
________________________________________
1. Project Overview
1.1 Project Title
AI-Powered Intelligent News Aggregation, Personalization and Error Management System Using n8n and Artificial Intelligence
________________________________________
1.2 Project Description
This capstone project is an enhanced version of a previously developed AI-powered news aggregation workflow. The improved system adopts a modular architecture consisting of three independent workflows that work together to automate the collection, processing, personalization, approval, and distribution of news content while providing intelligent error diagnosis.
The solution combines workflow automation and artificial intelligence to transform raw news collected from multiple online publications into professionally formatted newsletters tailored to a specific audience. Unlike the previous implementation, this version introduces Human-in-the-Loop (HITL) approval before publication, AI model fallback mechanisms, and automated AI error diagnosis to improve reliability, maintainability, and scalability.
________________________________________
2. Project Objectives
The project aims to:
•	Automate the collection of news from multiple online news sources.
•	Clean and summarize unstructured news content using Artificial Intelligence.
•	Store structured news data in Google Sheets.
•	Generate audience-specific newsletters using AI.
•	Introduce human approval before newsletter publication.
•	Automatically distribute approved newsletters via email.
•	Detect AI workflow failures.
•	Diagnose workflow failures and recommend corrective actions.
•	Improve system reliability through AI fallback models.
________________________________________
3. System Architecture
The solution is divided into three independent but interconnected workflows.
Workflow 1 – Data Extraction Workflow
↓
Google Sheets Database
↓
Workflow 2 – Chief Editor Workflow
↓
Human Approval
↓
Newsletter Distribution
↑
Workflow 3 – Error Management Workflow
The modular architecture allows each workflow to operate independently while exchanging data through Google Sheets and webhooks, improving maintainability and fault tolerance.
________________________________________
4. Workflow 1 – Data Extraction Workflow
4.1 Purpose
The Data Extraction Workflow is responsible for automatically collecting news from multiple Kenyan news websites, extracting the most important information using AI, and storing standardized summaries in Google Sheets.
This workflow serves as the data ingestion layer of the entire system.
________________________________________
4.2 Workflow Process
 
Step 1: Schedule Trigger
The workflow starts automatically based on a predefined schedule.
This eliminates the need for manual execution and ensures that news is collected consistently.
 
________________________________________
Step 2: Parallel Data Collection
Multiple HTTP Request nodes simultaneously retrieve news content from different Kenyan news websites including:
•	TechCabal
 
•	Techweez
 
•	Nation Africa
 
•	Standard Media
 
•	Smart Farmer Africa
 
•	Kilimo News
           
Each source is processed independently. If one source becomes unavailable, the remaining sources continue processing without interruption.
________________________________________
Step 3: AI Data Cleaning
Each HTTP Request node is paired with a dedicated AI Data Cleaning Agent.
The AI agent performs the following tasks:
•	Removes HTML tags.
•	Removes advertisements.
•	Removes navigation menus.
•	Eliminates duplicate information.
•	Identifies the main technology-related story.
•	Extracts the headline.
•	Generates a concise summary.
•	Produces standardized JSON output.
This ensures that all extracted news follows a consistent structure regardless of the original website.
 
________________________________________
Step 4: Structured Data Storage
The cleaned information is stored in Google Sheets with the following fields:
•	Date
•	Source
•	Headline
•	Summary
The spreadsheet acts as the central repository for the next workflow.
 
________________________________________
5. Workflow 2 – Chief Editor Workflow
 
5.1 Purpose
The Chief Editor Workflow transforms the structured news summaries into a professional newsletter tailored to the intended audience.
Unlike the previous implementation, this workflow introduces editorial approval before publication and produces HTML-formatted newsletters suitable for email distribution.
________________________________________
5.2 Workflow Process
Step 1: Google Sheets Trigger
Whenever new records are added to Google Sheets, the workflow automatically starts.
This ensures that newsletter generation begins immediately after new summaries become available.
 
________________________________________
Step 2: AI Editorial Processing
The Chief Editor AI analyzes all incoming summaries and performs the following editorial tasks:
•	Groups related stories under common topics.
•	Combines multiple summaries discussing the same event.
•	Removes duplicate information.
•	Preserves all unique facts.
•	Improves readability.
•	Organizes information logically.
•	Produces a professionally formatted HTML newsletter.
The generated newsletter is optimized for email presentation and audience engagement.
 
________________________________________
Step 3: AI Context Memory
A Simple Memory component maintains contextual information throughout the AI processing stage.
This helps the AI generate consistent summaries and avoid repetitive content.
 
________________________________________
Step 4: AI Model Fallback
The workflow implements two AI language models:
Primary Model
•	Mistral Cloud
         
Fallback Model
•	OpenRouter
          
If the primary model fails due to timeout or service interruption, the workflow automatically switches to the fallback model.
This significantly improves workflow reliability.
________________________________________
Step 5: Human-in-the-Loop Approval
Before publication, the generated newsletter is emailed to the editor for review.
The workflow pauses while waiting for the editor’s decision.
The editor has two options:
•	Approve
•	Reject
This introduces human oversight into the automated publishing process.
 
________________________________________
Step 6: Newsletter Distribution
If the newsletter is approved:
•	The workflow automatically emails the newsletter to all subscribers.
If the newsletter is rejected:
•	Distribution stops immediately.
•	No newsletter is sent.
This ensures that only verified content reaches readers.
 
________________________________________
6. Workflow 3 – Error Management Workflow
 
6.1 Purpose
The Error Management Workflow monitors failures occurring throughout the AI workflows and provides intelligent diagnostics.
Instead of merely logging an error, the workflow analyzes the problem and recommends corrective actions.
________________________________________
6.2 Workflow Process
Error Detection
Whenever an AI Agent or workflow encounters an exception, the Error Workflow is triggered automatically.
 
________________________________________
AI Error Analysis
The Error Analysis AI examines the error and generates:
•	Error description
•	Root cause
•	Severity level
•	Recommended solution
•	Preventive measures
•	Confidence level
This enables developers to troubleshoot issues more efficiently.
 
________________________________________
Developer Notification
After analysis, the workflow automatically sends an email to the developer containing:
•	Workflow name
•	Failed AI agent
•	Error details
•	Root cause
•	Recommended solution
•	Prevention strategy
This minimizes downtime and accelerates issue resolution.
 
________________________________________
7. Artificial Intelligence Architecture
The system uses specialized AI agents, each responsible for a distinct function.
AI Agent	Responsibility
Data Cleaning Agent	Cleans raw news content and extracts structured information
Chief Editor Agent	Merges summaries, removes duplicates, and generates personalized HTML newsletters
Error Analysis Agent	Diagnoses workflow failures and recommends solutions
This modular AI architecture improves scalability, maintainability, and overall system performance.
________________________________________
8. Technologies Used
Technology	Purpose
n8n	Workflow orchestration and automation
HTTP Request Nodes	Collect news from online sources
Google Sheets	Central data storage and workflow trigger
Mistral Cloud	Primary AI language model
OpenRouter	AI fallback model
Gmail	Newsletter approval and email distribution
AI Memory	Maintains context during newsletter generation
JSON	Standardized data exchange
________________________________________
9. Key Features
The system provides:
•	Automated news collection from multiple sources.
•	Parallel processing of news websites.
•	AI-powered data cleaning and summarization.
•	Structured data storage.
•	Audience-focused newsletter generation.
•	HTML email formatting.
•	Human approval before publication.
•	Automatic newsletter distribution.
•	AI model fallback for improved reliability.
•	Intelligent error diagnosis and recommendations.
________________________________________
10. Improvements Over the Previous Project
Compared to the previous implementation, this capstone introduces several significant enhancements:
•	Three independent workflows instead of a single workflow.
•	Parallel processing of multiple news sources.
•	Dedicated AI agent for each news source.
•	Automatic storage of structured news summaries.
•	AI-based grouping and merging of related stories.
•	Professional HTML newsletter generation.
•	Human-in-the-Loop editorial approval.
•	Automated email distribution after approval.
•	AI model fallback for improved fault tolerance.
•	Intelligent AI-powered error diagnosis and solution recommendations.
________________________________________
11. Benefits of the System
The proposed solution offers several advantages:
•	Reduces manual news collection.
•	Improves consistency of extracted information.
•	Generates high-quality newsletters automatically.
•	Enhances audience engagement through personalized content.
•	Improves workflow reliability.
•	Reduces developer troubleshooting time.
•	Supports future scalability through modular workflow design.
________________________________________
12. Future Enhancements
Potential improvements include:
•	Integration with additional news sources.
•	Multi-language newsletter generation.
•	Real-time news monitoring.
•	AI-based sentiment analysis.
•	Automatic topic categorization.
•	Analytics dashboard for newsletter performance.
•	Integration with mobile applications.
________________________________________
13. Conclusion
The AI-Powered Intelligent News Aggregation, Personalization and Error Management System demonstrates how workflow automation and Artificial Intelligence can be combined to build a scalable, intelligent, and resilient news processing platform.
By separating the solution into dedicated workflows for data extraction, editorial processing, and error management, the system significantly improves automation, maintainability, and fault tolerance compared to the previous implementation.
The introduction of Human-in-the-Loop approval, AI model fallback, contextual memory, HTML newsletter generation, and intelligent error diagnosis makes the platform suitable for real-world newsroom and content management applications. The project reduces manual effort, enhances content quality, and provides a reliable end-to-end solution for automated newsletter production.
