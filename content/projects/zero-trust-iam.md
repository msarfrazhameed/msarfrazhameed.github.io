---
title: "Automated Zero-Trust IAM Onboarding Workflow"
date: 2026-04-25
draft: false
tags: ["Cybersecurity", "Agentic AI", "n8n", "IAM"]
summary: "An automated system utilizing n8n and Gemini to assign Zero-Trust IAM permissions based on dynamic Google Sheets data with human-in-the-loop approvals."
feature: "images/n8n-architecture.jpg"
---

## Project Overview
In modern cybersecurity, Identity and Access Management (IAM) is the first line of defense. I architected an automated onboarding system designed around the principles of Zero-Trust. 

Rather than manually provisioning accounts, this workflow dynamically assesses new hire data, determines the principle of least privilege, and executes the provisioning process with a human-in-the-loop security checkpoint.

## Architecture & Tech Stack
* **Orchestration:** n8n (Self-hosted via Docker)
* **LLM Engine:** Gemini (For role-to-permission mapping)
* **Data Ingestion:** Google Sheets API
* **Security Gate:** Discord API (Human-in-the-loop approval)

## Workflow Logic
1. **Data Ingestion:** The n8n workflow triggers when a new employee's job title and department are entered into a designated Google Sheet.
2. **AI-Driven Permission Mapping:** The raw job title is passed to Gemini. The LLM evaluates the role and determines the strict, minimum IAM permissions required for that specific job function (Zero-Trust).
3. **The Human Security Gate:** Before any permissions are actually applied, the workflow pauses. It sends a formatted message to a secure Discord channel detailing the user, their role, and the AI-proposed permissions.
4. **Execution:** An administrator reviews the Discord message and clicks an "Approve" or "Deny" button, which pings a webhook back to n8n to finalize the workflow.

## The Value
By integrating an LLM into an n8n pipeline, this system removes human error from the initial permission-mapping phase while maintaining strict administrative oversight through the Discord webhook integration. It is a practical application of Agentic AI solving a traditional cybersecurity bottleneck.