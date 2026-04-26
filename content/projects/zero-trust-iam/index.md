---
title: "Automated Zero-Trust IAM Onboarding Workflow"
date: 2026-04-25
draft: false
tags: ["Cybersecurity", "Agentic AI", "n8n", "IAM"]
summary: "An automated system utilizing n8n and Gemini to assign Zero-Trust IAM permissions based on dynamic Google Sheets data with human-in-the-loop approvals."
layout: "hero"
---
{{< button href="https://github.com/msarfrazhameed/YOUR-REPO-NAME" target="_blank" >}}
<span class="flex items-center gap-2">
  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
  View Source Code on GitHub
</span>
{{< /button >}}

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