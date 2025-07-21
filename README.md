# 📘 Project Scope Document: PrivexBot

## 🔖 Project Name

**PrivexBot — Privacy-First AI Chatbot Builder Powered by Secret VM**

---

## 📌 Overview

**PrivexBot** is a privacy-focused, secure chatbot builder platform that empowers organizations to build and deploy AI-powered chatbots trained on their own data. Unlike traditional platforms, all AI workloads—including training, inference, and data ingestion—are executed within **Secret Network’s Trusted Execution Environments (TEEs)** using **Secret VMs**, ensuring **confidential computation**, **compliance**, and **zero data leakage**.

PrivexBot enables multi-platform chatbot deployment via embeddable widgets, Discord, Telegram, WhatsApp, Slack, or even custom-hosted URLs. Teams, enterprises, and agencies can easily create, manage, and distribute custom AI assistants (powered by  **Secret AI LLM**) with full control over data, plugins, and workflow logic.

---

## 🚀 Project Goals

* Build a **scalable, multi-tenant chatbot builder** with per-org workspaces
* Provide a **drag-and-drop chatbot builder** with real-time preview and plugin support
* Run **100% of AI computation inside Secret VMs** for security and compliance
* Offer a **plugin marketplace** for extensibility (e.g., web scrapers, Text to audio converter, Secret AI LLM Model, CRM tools, custom actions)
* Enable **agency tooling** for managing and reselling bots to clients
* Support **knowledge source ingestion** from Notion, Google Docs, websites, PDFs, CSVs, etc.
* Allow **deployment across multiple platforms** (Web, Discord, Telegram, WhatsApp, Zapier, etc)
* Include **analytics, billing, access control**, and team collaboration tools

---

## 🔐 Why Secret VMs and Trusted Infrastructure Matter

PrivexBot is not just another chatbot builder. It’s designed for a **privacy-first future**. Here’s why building on **Secret VMs** makes a difference:

### Advantages of Secret VMs

* **End-to-End Confidentiality:** All chatbot data, user prompts, and LLM responses stay encrypted in memory during compute.
* **Remote Attestation:** Cryptographically prove that code and data weren’t tampered with during inference.
* **Zero Trust Architecture:** Privexbot ensures that user data is protected from tampering during execution.
* **Regulatory Compliance:** Meet enterprise-grade standards such as Health Insurance Portability and Accountability Act (HIPAA)

By running all inference and processing in Secret VMs, PrivexBot becomes the **most secure** way to deploy an AI chatbot.

---

## 🧠 Core Features

### AI Chatbot Builder

* Drag-and-drop visual studio to build conversational flows (chatbots with workflow capabilities)
* Live testing/preview inside the builder
* Add logic, conditional branches, plugin actions, and nodes

### Secure Data Ingestion

* Upload `.pdf`, `.txt`, `.csv`, `.docx`, `.xlsx` files (up to 20MB)
* Paste text directly
* Sync from Notion, Google Docs, Google Sheets
* URL crawler for public webpages

### Multi-Platform Deployment

* Embed on websites via iframe or JS
* Public web URLs (auto-hosted chatbot pages)
* Integrations with Discord, WhatsApp, Telegram, Slack, WordPress, Zapier

### Organization & Workspace Management

* Multi-tenant model: Organization → Workspace → Chatbot
* Invite team members, assign roles, manage API keys
* Custom chatbot domains for white-labeled bots

### Plugin Marketplace

* Discover, install, and configure plugins (e.g., web scrapper, text to audio converter, video transcriber, Secret AI LLM model)
* Monetization support for plugin developers
* Submit custom plugins to the marketplace

### Agency Portal (Reseller Tools add-ons)

* Manage multiple client bots
* Set client billing preferences (use Privex or direct payments)
* Track client usage, access logs, generate reports

### Billing & Plans

* Subscription and usage-based pricing
* Accept crypto payments
* Downloadable invoices and usage analytics

### Analytics & Feedback

* View chatbot performance (token usage, latency, interaction counts)
* Collect user feedback, reviews, and chatbot ratings
* Plugin-specific analytics

---

## 🛠️ MVP Feature Scope

The **Minimum Viable Product (MVP)** will focus on delivering the core functionality required for building, deploying, and managing AI chatbots within a secure, multi-tenant environment.

| **Feature**                      | **Description**                                                                                          |
| -------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **User Registration**            | Secure sign-up and login with support for organization and workspace creation.                           |
| **Chatbot Studio**               | Drag-and-drop builder for designing chatbot flows, with real-time in-browser testing.                    |
| **Knowledge Ingestion**          | Upload `.pdf`, `.docx`, `.txt`, `.csv`, `.xlsx` files or sync from Notion/Google Docs.                   |
| **Plugin Marketplace**           | Basic plugin system to browse, install, and configure third-party or internal tools.                     |
| **Deployment Options**           | Embed via iframe/JS, generate public URLs, and integrate directly with Discord, Telegram, WhatsApp, etc. |
| **Secure Inference (Secret VM)** | All chatbot interactions and model processing run in Secret VMs for full data confidentiality.           |
| **Chatbot API Access**           | Generate secure API keys to access chatbot from external services.                                       |
| **Analytics Dashboard**          | Track token usage, number of interactions, latency, and feedback for each chatbot.                       |
| **Billing System**               | Handle subscriptions and crypto-based usage billing, with downloadable invoices.                         |
| **Team & Roles**                 | Invite team members, assign roles (e.g., admin, editor, viewer), and manage access.                      |
| **Agency Tools**                 | Create/manage bots for clients, control pricing and deployment, and track usage analytics.               |

---

## 🎨 User Interface & Core Pages

These are the main UI components the users will interact with, organized by functionality. Each page focuses on simplifying the process of building, managing, and scaling chatbots.

| **Page**              | **Core Functionality**                                                                                 |
| --------------------- | ------------------------------------------------------------------------------------------------------ |
| **Dashboard**         | High-level overview of organization usage, plan details, recent chatbot activity.                      |
| **Create Chatbot**    | Guided setup: import knowledge sources, define behavior, test and deploy bots.                         |
| **Knowledge Sources** | View, upload, or sync documents and web content used for chatbot training.                             |
| **Chatflow Studio**   | Visual workflow editor to build logic and conversational paths using drag-and-drop.                    |
| **Deployments**       | Generate embed codes, connect to external platforms (e.g., Discord, Telegram), and manage webhooks.    |
| **Marketplace**       | Explore and install plugins that extend chatbot capabilities (e.g., web scrapers, API actions).        |
| **Templates**         | Browse and clone prebuilt chatbot templates for various industries or tasks.                           |
| **Analytics**         | Monitor chatbot performance including usage statistics, latency, token consumption, and user feedback. |
| **Billing**           | View and manage subscriptions, payment methods, crypto invoices, and plan usage.                       |
| **Team Settings**     | Invite and manage team members, assign roles, and generate/revoke API keys.                            |
| **Agency Portal**     | Tools for agencies to create, manage, and monetize client bots with deployment tracking.               |
| **Referral Program**  | Share referral links, track invites, and earn rewards for bringing new users when they upgrade plan    |

[See mock images for the UI](./user-interfaces.md)

---

## 📂 System Architecture & Folder Structure

### Microservice-Based Architecture

PrivexBot will follow a modular, scalable architecture separating concerns into services:

```
privexbot/
├── frontend/           # Next.js or React UI for dashboard & builder
├── backend/            # API logic (auth, orgs, billing, chat logs)
├── ai-services/        # LLM orchestration, vector embeddings (in Secret VMs)
├── gateway/            # Secure routing layer to VMs
├── plugins/            # Dynamic plugin loader & registry
├── worker/             # Background jobs (ingestion, syncing, email)
├── infra/              # Terraform, deployment configs
```
[Click here for detailed architecture](./architecture-guide.md#project-structure)

### Why This Architecture?

* **Separation of concerns:** Clear division between UI, AI logic, plugins, and core backend
* **Scalability:** Each service can scale independently
* **Security:** AI runs in isolated Secret VMs
* **Dev agility:** Teams can extend plugins or UI without touching core backend

---

## 🔍 Target Market, Personas & Journeys

### 🎯 Target Market

* Privacy-conscious enterprises (finance, healthcare, education)
* Web3 orgs/DAOs needing compliant chat interfaces
* Agencies and AI service providers
* Developer platforms needing embedded helpdesk bots

### 👤 User Personas

1. **Compliance-Focused Enterprise CTO**

   * Needs chatbot on internal docs with HIPAA compliance
   * Concerned with data leakage and trust

2. **Startup Marketer with No-Code Skills**

   * Wants AI chatbot on website trained on Notion and Docs
   * Uses drag-drop builder and embeds widget

3. **Agency Owner**

   * Creates branded bots for multiple clients
   * Uses agency portal to manage billing and analytics

4. **Developer/Engineer**

   * Wants helpdesk bot trained on API or technical docs
   * Help visitors or anyone ask specific questions about the ecosystem or from the doc
   * Uses web embeds, slack, or webhook integrations for deployment

### 🧭 User Journey Example

| Step             | Action                                              |
| ---------------- | --------------------------------------------------- |
| 1. Sign up       | Create account, org, and workspace                  |
| 2. Add Knowledge | Upload docs or connect Notion/Google Drive          |
| 3. Build Bot     | Use visual studio to define conversation logic      |
| 4. Test          | Use live chat preview                               |
| 5. Deploy        | Embed on website or integrate with Discord/Telegram |
| 6. Monitor       | View usage, analytics, and feedback                 |
| 7. Extend        | Add plugins, enable agency tools, upgrade plan      |

---

## 🛎️ Use Case Examples

### 🛡️ Privacy-First Customer Support Bot

* Trained on support docs, product manuals, Tech doc, FAQs
* Handles chat/questions, escalates to live agent, creates tickets or send email to a dedicated email address
* Deployed on website, Discord, etc

### 🧠 Internal Knowledge Assistant (for Teams/DAOs)

* Trained on internal workflows and docs from websites
* Personalized answers based on team role
* Discord + Zapier + Web + Telegram deployment

### 🚀 Onboarding/Training Bot

* Walks new hires or contributors through SOPs
* Generates summaries and sends to email/Slack
* Deployed via website, Discord or WhatsApp

### 👨‍💻 Developer Docs Helpdesk

* Answers API and SDK questions in real time
* Embedded in Gitbook, supports webhooks
* Fully confidential with Secret VM-powered inference
