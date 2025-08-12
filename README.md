# Digital Transformation Automations (n8n + AI)

This repository contains production-ready n8n workflows from my Digital Transformation Project at CareerOS. The automations integrate AI to:

- Create CRM contacts and deals from meeting transcripts
- Sales Call Feedback and Probability scores based on meeting transcripts
- Cold Outreach Template (Scalable for different organisations)
- Draft personalized follow-up emails
- Schedule and track social media posts
- Keep a human-in-the-loop for quality control via Slack approvals

These workflows are designed to be modular, secure, and easy to import into any n8n instance.

BONUS: Head into the 'Framework for creating Automations through Claude Opus 4' folder to create automations on N8N using prompts on Claude. Read the instructions.

## Highlights

- AI-enhanced data extraction from transcripts (LLM-powered)
- CRM creation and enrichment flows (contacts, companies, deals)
- Automated follow-up email drafting with human approvals
- Social media scheduling across multiple platforms
- Slack-based review, approvals, and exceptions handling
- Robust error handling and run-safe defaults

## Repository Structure

**workflows/**

- linkedIn_automation.json
- cold_outreach.json
- followup_email.json
- contact_and_deal_creation.json

**docs/**

- Steps to authenticate each Node on N8N & Slack.docx
- LinkedIn Guide for Setup on N8N.docx
- Copy of Cold Email List Template.xlsx
- README.md

## What Each Workflow Does

**CRM from Transcripts**

- Parses meeting transcripts
- Identifies participant entities, companies, intents, and next steps
- Creates sales call feedback on the highlights, key takeaways, red flags and potential opportunities from the meeting
- Generates a probability score of the deal working out
- Creates or updates CRM contacts/companies/deals

**Follow-up Email Drafter**

- Generates personalized follow-up emails based on meeting context
- Uses consistent tone and templates with dynamic variables
- Routes drafts to Slack for human review, edits, and send approval
- Can send via Gmail/Outlook or hand off to your preferred tool

**Social Media Post Generator**

- Takes insights on Slack through the slash command, validates entries from the topic to create a post through Tavily to create a short-form social post
- Supports queued scheduling and platform-specific formatting
- Slack approval chain to approve, reschedule, or cancel

**Human-in-the-Loop via Slack**

All key actions require a Slack approval step:

Approve/Edit email drafts before sending

Approve/Reschedule social posts

Approvals are captured as structured metadata for auditability on Slack

## Prerequisites

- n8n: Self-hosted or n8n Cloud (latest recommended)
- Access tokens/credentials for:
  - LLM provider (e.g., OpenAI, Anthropic, Azure OpenAI)
  - Slack (bot token with chat:write, channels:history as needed)
  - CRM (e.g., HubSpot, Pipedrive, Salesforce; choose one and configure)
  - Email provider (e.g., Gmail via OAuth2, Outlook/Microsoft 365)
  - Social platforms or scheduler (e.g., X/Twitter, LinkedIn, Buffer)
  - Storage for transcripts (optional): Google Drive, S3, or Notion

## Quick Start

1) Import workflows

- In n8n, New Workflow → three-dot menu → Import from File/URL
- Import the workflows in workflows/

2) Create credentials in n8n

- LLM provider key
- Slack bot credentials
- CRM API credentials (pick your CRM)
- Email provider OAuth2
- Social platform tokens or scheduler API

3) Configure environment variables (recommended)

- In n8n, use environment variables for secrets
- Map credentials to nodes after import

4) Set required variables in each workflow

- Slack channel IDs for approvals
- CRM pipeline/stage IDs
- Email sender account and default templates
- Social posting queue or workspace IDs

5) Test with sample data

- Use examples/sample-transcript.md
- Run each workflow with test mode, validate outputs
- Approve in Slack and confirm downstream actions

## Security and Privacy

- No secrets are committed to this repo
- Workflows are scrubbed of credentials and internal endpoints
- Use n8n Credentials for all tokens; never hardcode secrets in nodes
- Review HTTP Request nodes for headers/params before running
- Consider PII handling, retention, and logging policies

## Configuration Notes

**LLMs**

- Set model, temperature, and max tokens to suit your tone/length
- Use system prompts stored in docs/ or environment variables

**CRM**

- Map fields in data-models.md to your CRM schema
- Deduplicate by email + domain where possible

**Email**

- Customize templates in examples/email-templates
- Enable link tracking and UTM parameters if needed

**Social**

- Use platform-specific constraints (length, media)
- Consider scheduling windows and time zones

## Contact

For questions or collaboration, reach out via issues or connect with me on LinkedIn at : <https://www.linkedin.com/in/yashwantsingh15/>
