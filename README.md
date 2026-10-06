# LeadPilot AI — Intelligent Lead Generation & Outreach Agent

LeadPilot AI is an automated lead-generation and outreach system built with n8n.

It discovers businesses based on industry and location, analyzes their websites, identifies potential automation opportunities, qualifies leads using AI, stores qualified businesses in a CRM, and generates personalized Gmail outreach drafts for manual review.

## The Problem

Finding potential business clients manually requires searching for companies, visiting their websites, collecting contact information, understanding their business, deciding whether they are a suitable prospect, and writing personalized outreach emails.

LeadPilot AI automates most of this research and preparation process while keeping the final outreach decision under human control.

## How It Works

Industry + Location
        ↓
Google Places Business Discovery
        ↓
Duplicate Lead Detection
        ↓
Business Website Analysis
        ↓
Email & Business Information Extraction
        ↓
AI Lead Qualification
        ↓
Lead Scoring
        ↓
Automation Opportunity Identification
        ↓
Google Sheets CRM
        ↓
AI Personalized Outreach
        ↓
Gmail Draft
        ↓
Manual Review & Send

## Key Features

- Dynamic business search by industry, city, and country
- Google Places API integration
- Duplicate lead prevention
- Business website analysis
- Public business email extraction
- AI-powered lead qualification
- Lead scoring system
- Automation opportunity identification
- Automatic service matching
- Google Sheets CRM integration
- AI-generated personalized outreach
- Gmail draft creation
- Human review before sending
- Error handling for failed website requests

## AI Qualification

The AI analyzes the available business information and website content and determines:

- What the business does
- Whether it is a suitable automation lead
- Lead score
- Relevant automation opportunity
- Recommended automation service
- Reason for qualification

Only leads scoring 60 or higher continue through the outreach pipeline.

## Technology Stack

- n8n — Workflow automation
- Google Places API — Business discovery
- DeepSeek — Business analysis and outreach generation
- Google Sheets — Lead CRM
- Gmail — Outreach draft creation
- Business websites — Business research and public contact discovery

## Outreach Approach

LeadPilot AI does not automatically send cold emails.

Qualified leads receive a personalized Gmail draft that can be reviewed, edited, and manually sent.

This keeps a human in control of the final outreach decision.

## What This Project Demonstrates

This project demonstrates my ability to build production-oriented automation systems involving:

- API integrations
- AI/LLM integration
- Web data extraction
- Data cleaning
- Structured AI outputs
- Conditional workflow logic
- Duplicate prevention
- CRM automation
- Email automation
- Error handling
- Multi-step business automation

## Current Version

**Version:** 1.0  
**Status:** Completed  
**Platform:** n8n  
**Project Type:** AI Automation / Lead Generation
