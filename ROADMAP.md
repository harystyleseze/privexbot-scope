# 🚀 **PrivexBot Development Roadmap (MVP Core Features)**

---

## 🔁 **Phase 0: Project Setup (Week 1)**

| Task                           | Description                                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------------------------ |
| **Monorepo Structure**         | Set up with `apps/` for frontend/gateway and `services/` for backend (API, embedding, ingestion) |
| **Dockerized Dev and Prod Environment** | PostgreSQL, Redis, FastAPI service, Next.js, gateway                                                |
| **CI/CD Bootstrapping**        | GitHub Actions with basic build, test, and deployment                          |
| **Database Schema v1**         | Users, Organizations, Workspaces, Chatbots, Leads, Files, Embeddings, Roles, etc.                        |

---

## 🧱 **Phase 1: Authentication & Multi-Tenant Core (Week 2–3)**

### 🎯 Goal: Multi-organization structure with workspace/chatbot scoping and auth

| Feature               | Description                                                            |
| --------------------- | ---------------------------------------------------------------------- |
| Email + Wallet Auth   | Email/password + wallet connect  |
| Organization Creation | Automatically create default organization and workspace on signup, Create or modify organization      |
| Multi-Org Switching   | UI and backend support for switching organizations                     |
| Roles & Permissions   | Admin, Editor, Viewer roles scoped per workspace/chatbot               |
| API Key Generation    | Unique per chatbot, rate limiting, linked to org/workspace for scoping                |

---

## 🤖 **Phase 2: Chatbot Creation & Knowledge Ingestion (Week 4–6)**

### 🎯 Goal: Users can create a chatbot, ingest content, and generate embeddings

| Feature                 | Description                                                                     |
| ----------------------- | ------------------------------------------------------------------------------- |
| Chatbot Setup Wizard    | UI flow for name, base prompt, Secret AI model, configuration - temperature, visibility                   |
| File Upload Support     | `.pdf`, `.txt`, `.docx`, `.xlsx`, `.csv` with processing backend                |
| URL Crawler             | Input a URL → scrape content using backend         |
| Manual Text Input       | Text editor to paste or write knowledge base content                            |
| Google Docs/Sheets Sync | OAuth + polling/webhook setup (Google API integration)                       |
| Notion Sync             | Use Notion API to fetch pages, with authentication and sync                     |
| AI Processing/Ingestion/LLM inference      | Implementation through Secret AI SDK |
| Vector Storage & Retrieval Layer     | Configure embedding strategy, implement query-time retrieval logic for top-k matches  |
| Chatbot Versioning     | Save draft, publish, rollback to earlier chatflow or prompt versions|
| Annotation  | Q/A knowledge source mapper  |

---

## 🧠 **Phase 3: Visual Chatflow Studio (Week 7–10)**

### 🎯 Goal: Drag-and-drop visual builder to control chatbot logic and flows

| Feature            | Description                                               |
| ------------------ | --------------------------------------------------------- |
| Chatflow Canvas UI | Drag and Drop feature, visual editor, block palette implementations, add knowledge sources    |
| Nodes & Branches   | Conditionals, messages, user input, API call, logic gates |
| Live Preview Panel | Inline test of conversation logic                         |
| Save/Load Chatflow | Persist logic to DB per chatbot                           |
| Live Chat Support        | Handover to human, connect via mobile, configure live chat setting/UI                                 |
| Export Flow and Chat history        | Option to export chat history and clear history                                  |

---

## 🌐 **Phase 4: Deployment & Embedding (Week 11–12)**

### 🎯 Goal: Easily share and deploy chatbot to various channels

| Feature                    | Description                                             |
| -------------------------- | ------------------------------------------------------- |
| Web Embeds                 | iframe + JS SDK (custom colors, logo, alignment)        |
| Public Pages               | Auto-hosted chatbot URLs on subdomains or custom domain |
| Domain Whitelist           | Prevent unauthorized embedding                          |
| Lead Management          | Collect, capture, or manage Leads                        |
| Discord/Slack Bots         | Connect bots using Webhooks and APIs                    |
| Telegram/WhatsApp Bots     | Set up via BotFather (Telegram) and Twilio (WhatsApp)   |
| Zapier & WordPress Plugins | Basic integration to support workflows                  |
| Automated Action            | Add Automated actions such as send Email, Calendly, and integrate with chatbot/chatflow           |
| Chatbot White Labeling           | Personalise Brand/Appearance and domain                         |

---

## 📈 **Phase 5: Analytics & Feedback (Week 13)**

### 🎯 Goal: Provide usage visibility and chatbot insights

| Feature             | Description                                   |
| ------------------- | --------------------------------------------- |
| Usage Dashboard     | Tokens, request count, latency, user sessions |
| Feedback Collection | Collect thumbs up/down + comments per message |
| Chat Ratings        | End-of-conversation rating option             |
| CSV/JSON Export     | Export chats and leads                        |
| Heatmaps (Advanced) | Visualize popular paths in chatflow           |

---

## 💳 **Phase 6: Billing & Subscriptions (Week 14–15)**

### 🎯 Goal: Monetization and subscription control per org

| Feature            | Description                                            |
| ------------------ | ------------------------------------------------------ |
| Plans & Tiers      | Free, Starter, Pro, Enterprise |
| Crypto Payments    | Implement crypto payment via Secret token, USDT, USDC       |
| Usage Limits       | Soft enforcement (warn) + hard limits (block)          |
| Invoices           | Auto-generated PDF or CSV downloads                    |
| Stripe Integration | Card payments with webhooks for plan enforcement       |

---

## 👥 **Phase 7: Team Collaboration & Notifications (Week 16)**

| Feature            | Description                                         |
| ------------------ | --------------------------------------------------- |
| Team Invites       | Email invites to join org/workspace                 |
| Role Management    | View/manage member roles per workspace              |
| Chat Notifications | Set email/webhook for chat alerts                   |
| Activity Logs      | View recent user actions (uploads, bot edits, etc.) |

---

## 📜 **Optional Phase 8: Marketplace, Plugin, Template, Agency Portal, Referral Program (Post-MVP)**

| Feature                    | Description                                       |
| -------------------------- | ------------------------------------------------- |
| Marketplace       | Place for plugins, utils, extensions, etc |
| Plugin | All things extensible such as LLM models, Text to voice converter, browser, etc        |
| Template             | Use, preview, and deploy chatbot from existing templates |
| Agency Portal        | Monetise your chatbots as a resell add-on           |
| Referral Program       | Refer to use premium features for free           |

---

## ✅ Summary of Milestones

| Milestone                   | Description                                  | Target Week |
| --------------------------- | -------------------------------------------- | ----------- |
| ✅ Project Bootstrap         | Repo, stack, infra setup (monorepo, Docker, CI/CD, DB schema) | Week 1      |
| ✅ Auth & Org Structure      | Wallet/email authentication, multi-organization support, roles & API keys | Week 2–3    |
| ✅ Chatbot Setup + Ingestion | Chatbot creation wizard, file/URL ingestion, Google Docs/Notion sync, embeddings | Week 4–6    |
| ✅ Visual Studio             | Visual chatflow builder with drag & drop, live preview, chatflow save/load, live chat support | Week 7–10   |
| ✅ Deployment                | Web embeds, public chatbot URLs, domain whitelist, lead management, multi-channel bots (Discord, Slack, Telegram, WhatsApp), Zapier & WordPress integration, white labeling | Week 11–12  |
| ✅ Analytics & Feedback      | Usage dashboard, feedback collection, chat ratings, export capabilities, heatmaps | Week 13     |
| ✅ Billing & Plans           | Subscription plans & tiers, crypto & card payments, usage limits, invoice generation | Week 14–15  |
| ✅ Team & Notifications      | Team invites, role management, chat notifications, activity logs | Week 16     |
| 🛡️ Plugin and Marketplace    | Extensible marketplace with plugins, templates, agency portal, referral program | Post-MVP    |
