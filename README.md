# 🚀 LeadPilot AI — Intelligent Lead Generation & Outreach Agent

LeadPilot AI is an **n8n-powered lead generation and outreach automation** that discovers businesses based on a selected industry and location, analyzes their websites, qualifies potential leads using AI, stores qualified leads in a Google Sheets CRM, and creates personalized Gmail drafts for manual review.

> **Important:** LeadPilot AI creates email drafts only. It does **not automatically send cold outreach emails**.

---

## 🎯 What LeadPilot AI Does

The workflow automatically:

1. Accepts an **Industry, Country, and City** from an n8n form.
2. Reads existing leads from the CRM to prevent duplicates.
3. Searches **Google Places** for relevant businesses.
4. Checks whether each business has a website.
5. Opens the business website.
6. Extracts publicly available business email addresses and useful website content.
7. Cleans and limits website content before AI analysis.
8. Uses **DeepSeek AI** to analyze and score each business.
9. Determines the most relevant automation opportunity.
10. Continues only when the lead score is **60 or higher**.
11. Stores qualified leads in **Google Sheets**.
12. Generates a personalized outreach email using AI.
13. Creates the email as a **Gmail draft**.
14. Updates the CRM with the draft information and lead status.

---

## ⚙️ Workflow Architecture

```text
Lead Search Form
        ↓
Get Existing Leads
        ↓
Google Places Search
        ↓
Split Businesses
        ↓
Duplicate Check
        ↓
Website Available?
        ↓
Open Homepage
        ↓
Extract Email + Website Content
        ↓
Clean Website Content
        ↓
Email Found?
        ↓
Prepare Lead
        ↓
DeepSeek Lead Qualification
        ↓
Qualified? (Score ≥ 60)
        ↓
Google Sheets CRM
        ↓
DeepSeek Outreach Generation
        ↓
Create Gmail Draft
        ↓
Update CRM
```

The production workflow can also use a separate **n8n Error Workflow** for error handling.

---

## ✨ Main Features

- 🌍 Dynamic industry, city, and country search
- 🔎 Google Places business discovery
- ♻️ Duplicate lead prevention using Google Place ID
- 🌐 Business website validation
- 📧 Public business email extraction from website `mailto:` links
- 🧹 Website content cleaning and context limiting
- 🤖 AI-powered business analysis
- 🎯 AI lead qualification
- 📊 Lead scoring
- 💡 Automation opportunity identification
- 🛠️ Automation service matching
- 📋 Google Sheets CRM integration
- ✉️ Personalized outreach email generation
- 📨 Gmail draft creation
- 👤 Human review before sending outreach
- ⚠️ Handling for missing or unreachable websites

---

## 🧠 AI Lead Qualification

LeadPilot analyzes the available business information and website content.

The AI is instructed to:

- Use only the provided business information.
- Avoid inventing business problems or requirements.
- Avoid inventing employees, tools, processes, results, or statistics.
- Recommend only one relevant automation service.
- Lower the lead score when there is insufficient evidence.
- Provide a reason for the qualification decision.

### Lead Scoring

| Score | Classification |
|---|---|
| **80–100** | Strong opportunity |
| **60–79** | Good potential lead |
| **40–59** | Weak or uncertain opportunity |
| **0–39** | Poor fit |

A business proceeds to the outreach stage only when its score is **60 or higher**.

---

## 🛠️ Supported Automation Services

LeadPilot can identify opportunities for:

- Lead capture and lead management automation
- Automated lead follow-up workflows
- Real-estate property matching automation
- Customer inquiry/support automation
- Invoice and payment tracking automation
- Email notification and reminder automation
- AI content creation workflows
- Social media content workflow automation
- Data entry and Google Sheets automation
- CRM workflow automation
- Reporting and business process automation
- Custom n8n workflow automation

The qualification system is specifically instructed **not** to recommend:

- Website development
- Website design
- SEO
- Domains
- Hosting
- Website security
- Website maintenance

---

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| **n8n** | Workflow automation |
| **Google Places API (New)** | Business discovery |
| **DeepSeek** | Lead analysis and outreach generation |
| **Google Sheets** | Lead CRM |
| **Gmail** | Outreach draft creation |
| **Business Websites** | Business context and public email discovery |

---

## 📋 Requirements

Before using the workflow, you need:

- n8n
- Google Places API (New)
- DeepSeek API access
- Google Sheets account
- Gmail account
- Google Sheets OAuth2 credential in n8n
- Gmail OAuth2 credential in n8n
- A Google Sheet using the required CRM structure

---

# 🚀 Setup Guide

## 1. Import the Workflow

Download:

```text
LeadPilot-AI-Public.json
```

Open n8n and import the workflow.

The public workflow should remain inactive until your own credentials and resources have been configured.

---

## 2. Configure Google Places API

Open the:

```text
GET BUSINESS
```

HTTP Request node.

Replace:

```text
YOUR_GOOGLE_PLACES_API_KEY
```

with your own **Google Places API key**.

For security, restrict your API key appropriately in Google Cloud.

The workflow uses Google Places Text Search to retrieve information such as:

- Business ID
- Business name
- Address
- Website
- Phone number
- Business type

---

## 3. Configure Google Sheets

Create a Google Sheet and add a sheet/tab called:

```text
Leads
```

Connect your own Google Sheets OAuth2 credential to the Google Sheets nodes.

Then select your own spreadsheet inside each Google Sheets node.

The CRM stores information including:

- Lead ID
- Business name
- Website
- Country
- City
- Industry
- Business email
- Email source
- Business summary
- Automation opportunity
- Recommended service
- Lead score
- Qualification reason
- Email subject
- Email body
- Gmail draft ID
- Status
- Discovery date
- Draft creation date
- Contact/reply information
- Notes

---

## 4. Configure DeepSeek

Connect your own **DeepSeek API credential** to the DeepSeek nodes.

LeadPilot uses AI for two different tasks.

### Lead Qualification

The first AI stage analyzes the business and determines:

- Business summary
- Lead score
- Qualification status
- Recommended automation service
- Automation opportunity
- Qualification reason

### Outreach Generation

The second AI stage creates:

- Email subject
- Personalized email body

---

## 5. Configure Gmail

Connect your own **Gmail OAuth2 credential** to:

```text
Create a draft
```

The workflow creates an email draft instead of automatically sending the email.

This allows the user to:

1. Review the generated email.
2. Edit it if necessary.
3. Decide whether the business should be contacted.
4. Manually send the email.

---

# 🔍 Example Search

A user could submit:

```text
Industry: Real estate agencies
Country: UAE
City: Dubai
```

LeadPilot will then search for matching businesses and process the results through the qualification pipeline.

---

# 🔁 Duplicate Prevention

LeadPilot retrieves existing CRM records before processing businesses.

Each business is compared using its **Google Place ID**.

If the Place ID already exists in the CRM, the lead is skipped.

This prevents the same business from repeatedly entering the outreach pipeline.

---

# 🌐 Website Analysis

For each new business, LeadPilot checks whether a website exists.

When available, the workflow extracts:

- Page title
- Meta description
- Headings
- Relevant paragraphs
- Public `mailto:` email links

The extracted content is cleaned before being sent to the AI model.

Website context is also limited in length to help control AI token usage.

---

# 📧 Outreach Strategy

LeadPilot follows a **human-reviewed outreach model**.

The generated emails are designed to:

- Be short and natural
- Reference the identified automation opportunity
- Avoid unsupported claims
- Avoid fake statistics
- Avoid fake case studies
- Avoid aggressive sales language
- Avoid fake urgency
- End with a simple, low-pressure call to action

The goal of the first email is to **start a conversation or offer a brief demo**, rather than immediately close a sale.

---

# 🛡️ Responsible Use

Do not upload the following to a public repository:

```text
API keys
OAuth tokens
Credential files
Private customer information
Real lead databases
Environment secrets
Private email data
```

Always review AI-generated outreach before sending it.

Users are responsible for following applicable:

- Privacy laws
- Email regulations
- Anti-spam requirements
- API provider policies
- Platform terms

---

# ⚠️ Current Limitations

LeadPilot AI Version 1 currently has several intentional limitations:

- Google Places itself does not provide business emails through this workflow.
- Email addresses are extracted from publicly available business websites.
- The workflow currently checks the homepage for `mailto:` email links.
- It does not crawl contact pages.
- Businesses without websites may be skipped.
- Businesses without detectable homepage emails may be skipped.
- Some websites may block automated requests.
- Some websites may temporarily be unreachable.
- AI qualification quality depends on the available website information.
- The Google Places search currently uses a small result count for controlled processing.

---

# 📁 Repository Structure

```text
leadpilot-ai/
│
├── README.md
├── LeadPilot-AI-Public.json
└── LeadPilot-AI-CRM-Template.xlsx
```

You can replace the example spreadsheet filename with the name of your own clean CRM template.

---

# 🔮 Future Improvements

Potential future versions could include:

- Contact-page email discovery
- Improved business email selection
- Google Places pagination
- Batch processing
- Automated reply tracking
- Follow-up workflows
- Additional CRM integrations
- More advanced lead scoring
- Lead analytics dashboard
- Additional business data sources

---

# 📌 Project Information

**Project:** LeadPilot AI  
**Version:** 1.0  
**Status:** Completed — Portfolio Project  
**Automation Platform:** n8n  
**AI Model:** DeepSeek  
**Business Discovery:** Google Places API (New)  
**CRM:** Google Sheets  
**Outreach:** Gmail Drafts  

---

## Disclaimer

LeadPilot AI is a reusable automation template and portfolio project.

Users are responsible for configuring their own credentials, reviewing generated content, and ensuring that their use of the workflow complies with applicable laws, outreach requirements, and third-party service policies.
