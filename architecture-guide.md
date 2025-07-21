# PrivexBot: Architecture Guide

---
### The Three Core Principles

- **Privacy (Priv)**: All data processing happens in Secret Network's Trusted Execution Environment (TEE)
- **Execution (Ex)**: Efficient, secure AI processing (secret ai LLM)
- **Bot**: User-friendly chatbot functionality

---

## Project Structure

```
privexbot/
├── README.md
├── docker-compose.yml                     # Orchestrates all services
├── docker-compose.dev.yml                # Development environment
├── docker-compose.prod.yml               # Production environment
├── .env.example                          # Environment variables template
├── .gitignore
├── LICENSE
├── CONTRIBUTING.md
│
├── frontend/                             # Next.js 15 React Frontend
│   ├── package.json
│   ├── package-lock.json
│   ├── next.config.js
│   ├── tailwind.config.js
│   ├── tsconfig.json
│   ├── Dockerfile
│   ├── public/
│   │   ├── icons/
│   │   ├── images/
│   │   ├── illustrations/
│   │   └── robots.txt
│   ├── src/
│   │   ├── app/                          # Next.js 15 App Router
│   │   │   ├── layout.tsx                # Root layout with wallet provider
│   │   │   ├── page.tsx                  # Landing page
│   │   │   ├── globals.css
│   │   │   ├── not-found.tsx             # 404 page
│   │   │   │
│   │   │   ├── auth/                     # Authentication pages
│   │   │   │   ├── signin/
│   │   │   │   │   ├── page.tsx          # Sign in with Keplr/Email
│   │   │   │   │   └── loading.tsx
│   │   │   │   ├── signup/
│   │   │   │   │   ├── page.tsx          # Sign up flow
│   │   │   │   │   ├── verify/page.tsx   # Email verification
│   │   │   │   │   └── [referralCode]/   # Referral signup
│   │   │   │   │       └── page.tsx      # Signup with referral code
│   │   │   │   ├── forgot-password/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── connect-wallet/
│   │   │   │       └── page.tsx          # Keplr wallet connection
│   │   │   │
│   │   │   ├── ref/                      # Referral landing pages
│   │   │   │   ├── [code]/               # Referral code landing
│   │   │   │   │   ├── page.tsx          # Landing with referral context
│   │   │   │   │   └── preview/          # Referrer preview
│   │   │   │   └── expired/              # Expired referral
│   │   │   │       └── page.tsx
│   │   │   │
│   │   │   ├── dashboard/                # Individual user dashboard
│   │   │   │   ├── page.tsx              # Personal dashboard
│   │   │   │   ├── layout.tsx            # Personal layout with sidebar
│   │   │   │   ├── studio/               # Personal studio
│   │   │   │   │   ├── page.tsx          # Personal studio home
│   │   │   │   │   ├── [botId]/          # Personal chatbot studio
│   │   │   │   │   │   ├── page.tsx      # Studio interface
│   │   │   │   │   │   ├── design/       # Design interface
│   │   │   │   │   │   ├── configure/    # Configuration
│   │   │   │   │   │   ├── knowledge/    # Knowledge base
│   │   │   │   │   │   ├── test/         # Testing interface
│   │   │   │   │   │   └── publish/      # Publishing
│   │   │   │   │   └── templates/        # Template gallery
│   │   │   │   ├── chatbots/             # Personal chatbots
│   │   │   │   │   ├── page.tsx          # My chatbots list
│   │   │   │   │   ├── create/           # Create new chatbot
│   │   │   │   │   └── [botId]/          # Chatbot management
│   │   │   │   ├── marketplace/          # Plugin marketplace
│   │   │   │   │   ├── page.tsx          # Marketplace home
│   │   │   │   │   ├── explore/          # Browse plugins
│   │   │   │   │   ├── installed/        # My plugins
│   │   │   │   │   └── [pluginId]/       # Plugin details
│   │   │   │   ├── billing/              # Personal billing
│   │   │   │   │   ├── page.tsx          # Billing overview
│   │   │   │   │   ├── upgrade/          # Upgrade plans
│   │   │   │   │   ├── usage/            # Usage tracking
│   │   │   │   │   └── payments/         # Payment history
│   │   │   │   ├── analytics/            # Personal analytics
│   │   │   │   │   ├── page.tsx          # Analytics dashboard
│   │   │   │   │   ├── usage/            # Usage analytics
│   │   │   │   │   └── reports/          # Custom reports
│   │   │   │   ├── profile/              # User profile
│   │   │   │   │   ├── page.tsx          # Profile overview
│   │   │   │   │   ├── settings/         # Profile settings
│   │   │   │   │   ├── wallet/           # Wallet management
│   │   │   │   │   ├── notifications/    # Notification settings
│   │   │   │   │   └── security/         # Security settings
│   │   │   │   ├── referrals/            # Referral program
│   │   │   │   │   ├── page.tsx          # Referral dashboard
│   │   │   │   │   ├── invite/           # Send invitations
│   │   │   │   │   │   ├── page.tsx      # Invite interface
│   │   │   │   │   │   ├── link/         # Generate referral links
│   │   │   │   │   │   └── email/        # Email invitations
│   │   │   │   │   ├── rewards/          # Reward management
│   │   │   │   │   │   ├── page.tsx      # Rewards overview
│   │   │   │   │   │   ├── history/      # Reward history
│   │   │   │   │   │   ├── withdraw/     # Withdraw USDC/USDT
│   │   │   │   │   │   └── pending/      # Pending rewards
│   │   │   │   │   ├── analytics/        # Referral analytics
│   │   │   │   │   │   ├── page.tsx      # Performance metrics
│   │   │   │   │   │   ├── conversions/  # Conversion tracking
│   │   │   │   │   │   └── leaderboard/  # Referral leaderboard
│   │   │   │   │   └── settings/         # Referral settings
│   │   │   │   │       ├── page.tsx      # Program settings
│   │   │   │   │       ├── notifications/ # Referral notifications
│   │   │   │   │       └── preferences/  # Referral preferences
│   │   │   │   └── organizations/        # Organization management
│   │   │   │       ├── page.tsx          # My organizations
│   │   │   │       ├── create/           # Create organization
│   │   │   │       │   ├── page.tsx      # Organization setup
│   │   │   │       │   ├── plan/         # Choose plan
│   │   │   │       │   ├── payment/      # Payment setup
│   │   │   │       │   └── invite/       # Invite team
│   │   │   │       ├── invitations/      # Organization invitations
│   │   │   │       │   ├── page.tsx      # Pending invitations
│   │   │   │       │   └── [inviteId]/   # Accept/decline invite
│   │   │   │       └── switch/           # Switch context
│   │   │   │
│   │   │   ├── workspace/                # Organization workspace
│   │   │   │   ├── page.tsx              # Workspace selector
│   │   │   │   ├── layout.tsx            # Workspace layout with sidebar
│   │   │   │   ├── [orgId]/              # Organization-scoped routes
│   │   │   │   │   ├── page.tsx          # Workspace dashboard
│   │   │   │   │   ├── loading.tsx
│   │   │   │   │   │
│   │   │   │   │   ├── studio/           # Chatbot Studio (Main Builder)
│   │   │   │   │   │   ├── page.tsx      # Studio home/templates
│   │   │   │   │   │   ├── [botId]/
│   │   │   │   │   │   │   ├── page.tsx  # Main studio interface
│   │   │   │   │   │   │   ├── layout.tsx # Studio layout with panels
│   │   │   │   │   │   │   ├── draft/
│   │   │   │   │   │   │   │   └── page.tsx # Draft workspace
│   │   │   │   │   │   │   ├── design/
│   │   │   │   │   │   │   │   ├── page.tsx # Visual flow designer
│   │   │   │   │   │   │   │   ├── orchestrate/
│   │   │   │   │   │   │   │   │   └── page.tsx # Workflow orchestration
│   │   │   │   │   │   │   │   ├── nodes/
│   │   │   │   │   │   │   │   │   └── page.tsx # Node management
│   │   │   │   │   │   │   │   └── tools/
│   │   │   │   │   │   │   │       └── page.tsx # Tool configuration
│   │   │   │   │   │   │   ├── configure/
│   │   │   │   │   │   │   │   ├── page.tsx # Bot configuration
│   │   │   │   │   │   │   │   ├── personality/
│   │   │   │   │   │   │   │   │   └── page.tsx # Personality settings
│   │   │   │   │   │   │   │   ├── features/
│   │   │   │   │   │   │   │   │   └── page.tsx # Feature toggles
│   │   │   │   │   │   │   │   ├── environment/
│   │   │   │   │   │   │   │   │   └── page.tsx # Environment variables
│   │   │   │   │   │   │   │   └── advanced/
│   │   │   │   │   │   │   │       └── page.tsx # Advanced settings
│   │   │   │   │   │   │   ├── knowledge/
│   │   │   │   │   │   │   │   ├── page.tsx # Knowledge management
│   │   │   │   │   │   │   │   ├── create/
│   │   │   │   │   │   │   │   │   └── page.tsx # Create knowledge base
│   │   │   │   │   │   │   │   ├── datasources/
│   │   │   │   │   │   │   │   │   ├── page.tsx # Data source management
│   │   │   │   │   │   │   │   │   ├── upload/
│   │   │   │   │   │   │   │   │   │   └── page.tsx # File upload (PDF, DOCX, CSV)
│   │   │   │   │   │   │   │   │   ├── web/
│   │   │   │   │   │   │   │   │   │   └── page.tsx # Website crawling
│   │   │   │   │   │   │   │   │   ├── notion/
│   │   │   │   │   │   │   │   │   │   └── page.tsx # Notion integration
│   │   │   │   │   │   │   │   │   ├── google-docs/
│   │   │   │   │   │   │   │   │   │   └── page.tsx # Google Docs integration
│   │   │   │   │   │   │   │   │   ├── direct-paste/
│   │   │   │   │   │   │   │   │   │   └── page.tsx # Direct content paste
│   │   │   │   │   │   │   │   │   └── api/
│   │   │   │   │   │   │   │   │       └── page.tsx # API integration
│   │   │   │   │   │   │   │   ├── processing/
│   │   │   │   │   │   │   │   │   └── page.tsx # Document processing
│   │   │   │   │   │   │   │   └── annotation/
│   │   │   │   │   │   │   │       └── page.tsx # Data annotation
│   │   │   │   │   │   │   ├── chatflow/
│   │   │   │   │   │   │   │   ├── page.tsx # Conversation flow design
│   │   │   │   │   │   │   │   ├── builder/
│   │   │   │   │   │   │   │   │   └── page.tsx # Flow builder interface
│   │   │   │   │   │   │   │   └── conditions/
│   │   │   │   │   │   │   │       └── page.tsx # Conditional logic
│   │   │   │   │   │   │   ├── workflow/
│   │   │   │   │   │   │   │   ├── page.tsx # Workflow management
│   │   │   │   │   │   │   │   ├── automation/
│   │   │   │   │   │   │   │   │   └── page.tsx # Automation rules
│   │   │   │   │   │   │   │   └── triggers/
│   │   │   │   │   │   │   │       └── page.tsx # Event triggers
│   │   │   │   │   │   │   ├── agents/
│   │   │   │   │   │   │   │   ├── page.tsx # Chat agent management
│   │   │   │   │   │   │   │   ├── create/
│   │   │   │   │   │   │   │   │   └── page.tsx # Create new agent
│   │   │   │   │   │   │   │   └── [agentId]/
│   │   │   │   │   │   │   │       └── page.tsx # Agent configuration
│   │   │   │   │   │   │   ├── test/
│   │   │   │   │   │   │   │   ├── page.tsx # Test interface
│   │   │   │   │   │   │   │   ├── preview/
│   │   │   │   │   │   │   │   │   └── page.tsx # Live preview
│   │   │   │   │   │   │   │   ├── conversation/
│   │   │   │   │   │   │   │   │   └── page.tsx # Conversation testing
│   │   │   │   │   │   │   │   └── scenarios/
│   │   │   │   │   │   │   │       └── page.tsx # Test scenarios
│   │   │   │   │   │   │   ├── version/
│   │   │   │   │   │   │   │   ├── page.tsx # Version history
│   │   │   │   │   │   │   │   ├── compare/
│   │   │   │   │   │   │   │   │   └── page.tsx # Version comparison
│   │   │   │   │   │   │   │   └── restore/
│   │   │   │   │   │   │   │       └── page.tsx # Version restore
│   │   │   │   │   │   │   ├── checklist/
│   │   │   │   │   │   │   │   └── page.tsx # Quality checklist/issues
│   │   │   │   │   │   │   ├── publish/
│   │   │   │   │   │   │   │   ├── page.tsx # Publish interface
│   │   │   │   │   │   │   │   ├── review/
│   │   │   │   │   │   │   │   │   └── page.tsx # Pre-publish review
│   │   │   │   │   │   │   │   └── deploy/
│   │   │   │   │   │   │   │       └── page.tsx # Deployment options
│   │   │   │   │   │   │   └── execute/
│   │   │   │   │   │   │       └── page.tsx # Execution monitoring
│   │   │   │   │   │   └── templates/
│   │   │   │   │   │       ├── page.tsx # Template gallery
│   │   │   │   │   │       ├── [templateId]/
│   │   │   │   │   │       │   └── page.tsx # Template details
│   │   │   │   │   │       └── create/
│   │   │   │   │   │           └── page.tsx # Create from template
│   │   │   │   │   │
│   │   │   │   │   ├── chatbots/          # Chatbot Management
│   │   │   │   │   │   ├── page.tsx       # All chatbots overview
│   │   │   │   │   │   ├── create/
│   │   │   │   │   │   │   ├── page.tsx   # Create new chatbot
│   │   │   │   │   │   │   ├── blank/
│   │   │   │   │   │   │   │   └── page.tsx # Create from scratch
│   │   │   │   │   │   │   └── template/
│   │   │   │   │   │   │       └── page.tsx # Create from template
│   │   │   │   │   │   └── [botId]/
│   │   │   │   │   │       ├── page.tsx   # Bot details/overview
│   │   │   │   │   │       ├── settings/
│   │   │   │   │   │       │   ├── page.tsx # Bot settings
│   │   │   │   │   │       │   ├── general/
│   │   │   │   │   │       │   │   └── page.tsx # General settings
│   │   │   │   │   │       │   ├── security/
│   │   │   │   │   │       │   │   └── page.tsx # Security settings
│   │   │   │   │   │       │   └── integrations/
│   │   │   │   │   │       │       └── page.tsx # Platform integrations
│   │   │   │   │   │       ├── analytics/
│   │   │   │   │   │       │   ├── page.tsx # Analytics dashboard
│   │   │   │   │   │       │   ├── conversations/
│   │   │   │   │   │       │   │   └── page.tsx # Conversation analytics
│   │   │   │   │   │       │   ├── performance/
│   │   │   │   │   │       │   │   └── page.tsx # Performance metrics
│   │   │   │   │   │       │   └── reports/
│   │   │   │   │   │       │       └── page.tsx # Custom reports
│   │   │   │   │   │       ├── monitoring/
│   │   │   │   │   │       │   ├── page.tsx # Real-time monitoring
│   │   │   │   │   │       │   ├── logs/
│   │   │   │   │   │       │   │   └── page.tsx # System logs
│   │   │   │   │   │       │   ├── errors/
│   │   │   │   │   │       │   │   └── page.tsx # Error tracking
│   │   │   │   │   │       │   └── health/
│   │   │   │   │   │       │       └── page.tsx # Health checks
│   │   │   │   │   │       └── api-access/
│   │   │   │   │   │           ├── page.tsx # API management
│   │   │   │   │   │           ├── keys/
│   │   │   │   │   │           │   └── page.tsx # API key management
│   │   │   │   │   │           ├── documentation/
│   │   │   │   │   │           │   └── page.tsx # API docs
│   │   │   │   │   │           └── webhooks/
│   │   │   │   │   │               └── page.tsx # Webhook configuration
│   │   │   │   │   │
│   │   │   │   │   ├── marketplace/       # Plugin Marketplace
│   │   │   │   │   │   ├── page.tsx       # Marketplace home
│   │   │   │   │   │   ├── explore/
│   │   │   │   │   │   │   ├── page.tsx   # Browse all plugins
│   │   │   │   │   │   │   ├── featured/
│   │   │   │   │   │   │   │   └── page.tsx # Featured plugins
│   │   │   │   │   │   │   ├── categories/
│   │   │   │   │   │   │   │   └── [category]/
│   │   │   │   │   │   │   │       └── page.tsx # Category view
│   │   │   │   │   │   │   └── search/
│   │   │   │   │   │   │       └── page.tsx # Search results
│   │   │   │   │   │   ├── installed/
│   │   │   │   │   │   │   ├── page.tsx   # Installed plugins
│   │   │   │   │   │   │   └── [pluginId]/
│   │   │   │   │   │   │       ├── page.tsx # Plugin details
│   │   │   │   │   │   │       ├── configure/
│   │   │   │   │   │   │       │   └── page.tsx # Plugin configuration
│   │   │   │   │   │   │       └── test/
│   │   │   │   │   │   │           └── page.tsx # Test plugin
│   │   │   │   │   │   ├── publish/
│   │   │   │   │   │   │   ├── page.tsx   # Publish plugin
│   │   │   │   │   │   │   ├── upload/
│   │   │   │   │   │   │   │   └── page.tsx # Upload plugin
│   │   │   │   │   │   │   ├── review/
│   │   │   │   │   │   │   │   └── page.tsx # Plugin review
│   │   │   │   │   │   │   └── submit/
│   │   │   │   │   │   │       └── page.tsx # Submit for approval
│   │   │   │   │   │   └── [pluginId]/
│   │   │   │   │   │       ├── page.tsx   # Plugin detail view
│   │   │   │   │   │       ├── install/
│   │   │   │   │   │       │   └── page.tsx # Install plugin
│   │   │   │   │   │       ├── reviews/
│   │   │   │   │   │       │   └── page.tsx # Plugin reviews
│   │   │   │   │   │       └── changelog/
│   │   │   │   │   │           └── page.tsx # Plugin changelog
│   │   │   │   │   │
│   │   │   │   │   ├── analytics/         # Organization Analytics
│   │   │   │   │   │   ├── page.tsx       # Analytics dashboard
│   │   │   │   │   │   ├── usage/
│   │   │   │   │   │   │   ├── page.tsx   # Usage analytics
│   │   │   │   │   │   │   ├── tokens/
│   │   │   │   │   │   │   │   └── page.tsx # Token usage
│   │   │   │   │   │   │   └── api/
│   │   │   │   │   │   │       └── page.tsx # API usage
│   │   │   │   │   │   ├── billing/
│   │   │   │   │   │   │   ├── page.tsx   # Billing overview
│   │   │   │   │   │   │   ├── payments/
│   │   │   │   │   │   │   │   └── page.tsx # Payment history
│   │   │   │   │   │   │   ├── staking/
│   │   │   │   │   │   │   │   └── page.tsx # SCRT staking
│   │   │   │   │   │   │   └── invoices/
│   │   │   │   │   │   │       └── page.tsx # Invoice management
│   │   │   │   │   │   └── reports/
│   │   │   │   │   │       ├── page.tsx   # Custom reports
│   │   │   │   │   │       ├── export/
│   │   │   │   │   │       │   └── page.tsx # Data export
│   │   │   │   │   │       └── scheduled/
│   │   │   │   │   │           └── page.tsx # Scheduled reports
│   │   │   │   │   │
│   │   │   │   │   ├── settings/          # Organization Settings
│   │   │   │   │   │   ├── page.tsx       # General settings
│   │   │   │   │   │   ├── members/
│   │   │   │   │   │   │   ├── page.tsx   # Team management
│   │   │   │   │   │   │   ├── invite/
│   │   │   │   │   │   │   │   └── page.tsx # Invite members
│   │   │   │   │   │   │   └── roles/
│   │   │   │   │   │   │       └── page.tsx # Role management
│   │   │   │   │   │   ├── security/
│   │   │   │   │   │   │   ├── page.tsx   # Security settings
│   │   │   │   │   │   │   ├── api-keys/
│   │   │   │   │   │   │   │   └── page.tsx # API key management
│   │   │   │   │   │   │   └── audit/
│   │   │   │   │   │   │       └── page.tsx # Audit logs
│   │   │   │   │   │   ├── billing/
│   │   │   │   │   │   │   ├── page.tsx   # Billing settings
│   │   │   │   │   │   │   ├── subscription/
│   │   │   │   │   │   │   │   └── page.tsx # Subscription management
│   │   │   │   │   │   │   └── payment-methods/
│   │   │   │   │   │   │       └── page.tsx # Payment methods
│   │   │   │   │   │   └── integration/
│   │   │   │   │   │       ├── page.tsx   # Integration settings
│   │   │   │   │   │       ├── webhooks/
│   │   │   │   │   │       │   └── page.tsx # Webhook configuration
│   │   │   │   │   │       └── api/
│   │   │   │   │   │           └── page.tsx # API configuration
│   │   │   │   │   │
│   │   │   │   │   └── profile/           # User Profile (org context)
│   │   │   │   │       ├── page.tsx       # Profile overview
│   │   │   │   │       ├── settings/
│   │   │   │   │       │   ├── page.tsx   # Profile settings
│   │   │   │   │       │   ├── preferences/
│   │   │   │   │       │   │   └── page.tsx # User preferences
│   │   │   │   │       │   └── notifications/
│   │   │   │   │       │       └── page.tsx # Notification settings
│   │   │   │   │       ├── wallet/
│   │   │   │   │       │   ├── page.tsx   # Wallet management
│   │   │   │   │       │   ├── connect/
│   │   │   │   │       │   │   └── page.tsx # Connect new wallet
│   │   │   │   │       │   ├── tokens/
│   │   │   │   │       │   │   └── page.tsx # Token management
│   │   │   │   │       │   └── transactions/
│   │   │   │   │       │       └── page.tsx # Transaction history
│   │   │   │   │       └── organizations/
│   │   │   │   │           ├── page.tsx   # Organization membership
│   │   │   │   │           ├── create/
│   │   │   │   │           │   └── page.tsx # Create organization
│   │   │   │   │           └── switch/
│   │   │   │   │               └── page.tsx # Switch organization
│   │   │   │   │
│   │   │   │   └── new/                   # Create organization
│   │   │   │       └── page.tsx
│   │   │   │
│   │   │   ├── explore/                   # Public exploration (no auth)
│   │   │   │   ├── page.tsx               # Explore home
│   │   │   │   ├── templates/
│   │   │   │   │   ├── page.tsx           # Public templates
│   │   │   │   │   └── [templateId]/
│   │   │   │   │       └── page.tsx       # Template preview
│   │   │   │   ├── showcase/
│   │   │   │   │   ├── page.tsx           # Bot showcase
│   │   │   │   │   └── [botId]/
│   │   │   │   │       └── page.tsx       # Bot demo
│   │   │   │   └── plugins/
│   │   │   │       ├── page.tsx           # Public plugin directory
│   │   │   │       └── [pluginId]/
│   │   │   │           └── page.tsx       # Plugin information
│   │   │   │
│   │   │   ├── pricing/                   # Pricing page
│   │   │   │   └── page.tsx
│   │   │   │
│   │   │   ├── docs/                      # Documentation
│   │   │   │   ├── page.tsx               # Documentation home
│   │   │   │   ├── getting-started/
│   │   │   │   │   └── page.tsx
│   │   │   │   ├── api/
│   │   │   │   │   └── page.tsx
│   │   │   │   └── guides/
│   │   │   │       └── page.tsx
│   │   │   └── api/                      # API routes
│   │   │       ├── auth/
│   │   │       │   ├── login/route.ts
│   │   │       │   ├── register/route.ts
│   │   │       │   ├── register-referral/route.ts  # Referral signup
│   │   │       │   └── refresh/route.ts
│   │   │       ├── referrals/                # Referral API endpoints
│   │   │       │   ├── generate-link/route.ts      # Generate referral link
│   │   │       │   ├── validate-code/route.ts      # Validate referral code
│   │   │       │   ├── invite/route.ts             # Send referral invites
│   │   │       │   ├── rewards/route.ts            # Get reward history
│   │   │       │   ├── withdraw/route.ts           # Withdraw rewards
│   │   │       │   ├── analytics/route.ts          # Referral analytics
│   │   │       │   └── leaderboard/route.ts        # Referral leaderboard
│   │   │       ├── webhooks/
│   │   │       │   ├── discord/route.ts
│   │   │       │   ├── slack/route.ts
│   │   │       │   ├── whatsapp/route.ts
│   │   │       │   └── payment-success/route.ts    # Payment webhook for referrals
│   │   │       └── proxy/
│   │   │           └── chat/route.ts
│   │   ├── components/                   # Reusable UI components
│   │   │   ├── ui/                       # shadcn/ui components
│   │   │   │   ├── button.tsx
│   │   │   │   ├── card.tsx
│   │   │   │   ├── dialog.tsx
│   │   │   │   ├── form.tsx
│   │   │   │   ├── input.tsx
│   │   │   │   └── toast.tsx
│   │   │   ├── wallet/                   # Keplr wallet integration
│   │   │   │   ├── WalletConnect.tsx      # Main wallet connection component
│   │   │   │   ├── WalletBalance.tsx      # Display wallet balances
│   │   │   │   ├── PaymentModal.tsx       # SCRT/SNIP-20 payment interface
│   │   │   │   ├── StakingInterface.tsx   # SCRT staking for pro features
│   │   │   │   ├── TokenSelector.tsx      # Token selection dropdown
│   │   │   │   └── TransactionHistory.tsx # Transaction history display
│   │   │   │
│   │   │   ├── studio/                   # Studio-specific components
│   │   │   │   ├── FlowCanvas.tsx         # Main flow design canvas
│   │   │   │   ├── NodeLibrary.tsx        # Draggable node library
│   │   │   │   ├── NodeEditor.tsx         # Node configuration panel
│   │   │   │   ├── PropertyPanel.tsx      # Properties sidebar
│   │   │   │   ├── StudioToolbar.tsx      # Studio toolbar with actions
│   │   │   │   ├── PreviewPanel.tsx       # Live chatbot preview
│   │   │   │   ├── VersionControl.tsx     # Version management UI
│   │   │   │   ├── PublishModal.tsx       # Publish/deploy modal
│   │   │   │   ├── ChecklistSidebar.tsx   # Quality checklist
│   │   │   │   ├── EnvironmentVars.tsx    # Environment variable editor
│   │   │   │   ├── FeatureToggles.tsx     # Feature configuration toggles
│   │   │   │   ├── PersonalityConfig.tsx  # Bot personality settings
│   │   │   │   ├── WorkflowOrchestrator.tsx # Workflow design interface
│   │   │   │   ├── AgentBuilder.tsx       # Chat agent configuration
│   │   │   │   ├── KnowledgeManager.tsx   # Knowledge base management
│   │   │   │   ├── DataAnnotation.tsx     # Data annotation interface
│   │   │   │   ├── TestInterface.tsx      # Chatbot testing interface
│   │   │   │   ├── ConversationTester.tsx # Conversation flow testing
│   │   │   │   ├── ScenarioBuilder.tsx    # Test scenario builder
│   │   │   │   └── ExecutionMonitor.tsx   # Live execution monitoring
│   │   │   │
│   │   │   ├── chatbot/                  # Chatbot management components
│   │   │   │   ├── ChatInterface.tsx      # Interactive chat component
│   │   │   │   ├── BotCard.tsx           # Chatbot overview card
│   │   │   │   ├── BotGrid.tsx           # Grid layout for multiple bots
│   │   │   │   ├── TrainingProgress.tsx   # Training status display
│   │   │   │   ├── AnalyticsDashboard.tsx # Analytics charts and metrics
│   │   │   │   ├── DeploymentStatus.tsx   # Deployment status indicators
│   │   │   │   ├── UsageMetrics.tsx       # Usage statistics component
│   │   │   │   ├── PerformanceChart.tsx   # Performance visualization
│   │   │   │   ├── ConversationList.tsx   # List of conversations
│   │   │   │   ├── MessageAnnotation.tsx  # Message annotation interface
│   │   │   │   └── BotSettings.tsx        # Bot configuration form
│   │   │   │
│   │   │   ├── marketplace/              # Marketplace components
│   │   │   │   ├── PluginCard.tsx         # Plugin overview card
│   │   │   │   ├── PluginGrid.tsx         # Grid of plugins
│   │   │   │   ├── PluginDetail.tsx       # Detailed plugin view
│   │   │   │   ├── InstallModal.tsx       # Plugin installation modal
│   │   │   │   ├── PluginConfig.tsx       # Plugin configuration interface
│   │   │   │   ├── ReviewsSection.tsx     # Plugin reviews and ratings
│   │   │   │   ├── PublishPlugin.tsx      # Plugin publishing form
│   │   │   │   ├── CategoryFilter.tsx     # Plugin category filtering
│   │   │   │   ├── SearchFilter.tsx       # Plugin search interface
│   │   │   │   ├── InstalledPlugins.tsx   # Manage installed plugins
│   │   │   │   └── PluginTester.tsx       # Plugin testing interface
│   │   │   │
│   │   │   ├── knowledge/                # Knowledge management components
│   │   │   │   ├── DataSourceUpload.tsx   # File upload interface
│   │   │   │   ├── WebCrawler.tsx         # Website crawling configuration
│   │   │   │   ├── NotionConnector.tsx    # Notion integration interface
│   │   │   │   ├── GoogleDocsConnector.tsx # Google Docs integration interface
│   │   │   │   ├── DirectPasteEditor.tsx  # Direct content paste interface
│   │   │   │   ├── DocumentProcessor.tsx  # Document processing interface
│   │   │   │   ├── KnowledgeBase.tsx      # Knowledge base overview
│   │   │   │   ├── AnnotationTool.tsx     # Data annotation interface
│   │   │   │   ├── ProcessingQueue.tsx    # Document processing queue
│   │   │   │   ├── SourceManager.tsx      # Data source management
│   │   │   │   └── VectorVisualization.tsx # Vector embeddings visualization
│   │   │   │
│   │   │   ├── analytics/                # Analytics components
│   │   │   │   ├── DashboardOverview.tsx  # Main analytics dashboard
│   │   │   │   ├── UsageChart.tsx         # Usage trend charts
│   │   │   │   ├── TokenUsageChart.tsx    # Token consumption charts
│   │   │   │   ├── BillingOverview.tsx    # Billing summary component
│   │   │   │   ├── ConversationAnalytics.tsx # Conversation insights
│   │   │   │   ├── PerformanceMetrics.tsx # System performance metrics
│   │   │   │   ├── ReportBuilder.tsx      # Custom report builder
│   │   │   │   ├── DataExporter.tsx       # Data export interface
│   │   │   │   └── AlertsPanel.tsx        # Monitoring alerts panel
│   │   │   │
│   │   │   ├── organization/             # Organization management components
│   │   │   │   ├── OrgSelector.tsx        # Organization switcher
│   │   │   │   ├── MemberManagement.tsx   # Team member management
│   │   │   │   ├── RoleEditor.tsx         # Role and permissions editor
│   │   │   │   ├── InviteModal.tsx        # Team invitation modal
│   │   │   │   ├── BillingSettings.tsx    # Billing configuration
│   │   │   │   ├── SecuritySettings.tsx   # Security configuration
│   │   │   │   ├── APIKeyManager.tsx      # API key management
│   │   │   │   ├── WebhookConfig.tsx      # Webhook configuration
│   │   │   │   ├── AuditLog.tsx           # Audit log viewer
│   │   │   │   └── IntegrationSettings.tsx # Platform integrations
│   │   │   │
│   │   │   ├── referrals/                # Referral system components
│   │   │   │   ├── ReferralDashboard.tsx  # Main referral dashboard
│   │   │   │   ├── ReferralLinkGenerator.tsx # Generate custom referral links
│   │   │   │   ├── ReferralInviteModal.tsx # Send email invitations
│   │   │   │   ├── RewardBalance.tsx       # USDC/USDT balance display
│   │   │   │   ├── RewardHistory.tsx       # Transaction history
│   │   │   │   ├── WithdrawModal.tsx       # USDC/USDT withdrawal interface
│   │   │   │   ├── ReferralStats.tsx       # Performance metrics
│   │   │   │   ├── ConversionChart.tsx     # Conversion analytics
│   │   │   │   ├── ReferralLeaderboard.tsx # Top referrers
│   │   │   │   ├── EarningsCalculator.tsx  # Potential earnings calculator
│   │   │   │   ├── ReferralBanner.tsx      # Promotional banner
│   │   │   │   ├── SocialShareButtons.tsx  # Social media sharing
│   │   │   │   └── ReferralLanding.tsx     # Landing page for referred users
│   │   │   │
│   │   │   ├── shared/                   # Shared/common components
│   │   │   │   ├── Header.tsx             # Main application header
│   │   │   │   ├── Sidebar.tsx            # Navigation sidebar
│   │   │   │   ├── WorkspaceSwitcher.tsx  # Workspace/org switcher
│   │   │   │   ├── BreadcrumbNav.tsx      # Breadcrumb navigation
│   │   │   │   ├── Loading.tsx            # Loading states
│   │   │   │   ├── ErrorBoundary.tsx      # Error handling
│   │   │   │   ├── EmptyState.tsx         # Empty state illustrations
│   │   │   │   ├── ConfirmModal.tsx       # Confirmation dialogs
│   │   │   │   ├── NotificationPanel.tsx  # In-app notifications
│   │   │   │   ├── SearchBar.tsx          # Global search component
│   │   │   │   ├── FilterPanel.tsx        # Filtering interface
│   │   │   │   ├── PaginationControls.tsx # Pagination component
│   │   │   │   ├── StatusIndicator.tsx    # Status badges and indicators
│   │   │   │   ├── CopyToClipboard.tsx    # Copy functionality
│   │   │   │   ├── DateRangePicker.tsx    # Date range selection
│   │   │   │   ├── FileUpload.tsx         # File upload component
│   │   │   │   ├── CodeEditor.tsx         # Code/JSON editor
│   │   │   │   ├── MarkdownRenderer.tsx   # Markdown display
│   │   │   │   └── TooltipInfo.tsx        # Information tooltips
│   │   ├── lib/                          # Utility functions
│   │   │   ├── auth.ts                   # Authentication utilities
│   │   │   ├── api.ts                    # API client configuration
│   │   │   ├── wallet.ts                 # Keplr wallet utilities
│   │   │   ├── secret-network.ts         # Secret Network client
│   │   │   ├── utils.ts                  # General utilities
│   │   │   ├── constants.ts              # Application constants
│   │   │   └── validators.ts             # Form validation schemas
│   │   ├── hooks/                        # Custom React hooks
│   │   │   ├── use-auth.ts               # Authentication hook
│   │   │   ├── use-wallet.ts             # Wallet connection hook
│   │   │   ├── use-organization.ts       # Organization management hook
│   │   │   ├── use-secret-network.ts     # Secret Network integration hook
│   │   │   ├── use-chatbot.ts            # Chatbot management hook
│   │   │   └── use-deployment.ts         # Deployment management hook
│   │   ├── store/                        # Zustand state management
│   │   │   ├── auth.ts                   # Authentication state
│   │   │   ├── wallet.ts                 # Wallet state
│   │   │   ├── organization.ts           # Organization state
│   │   │   ├── chatbot.ts                # Chatbot state
│   │   │   └── ui.ts                     # UI state (modals, etc.)
│   │   └── types/                        # TypeScript type definitions
│   │       ├── auth.ts                   # Authentication types
│   │       ├── chatbot.ts                # Chatbot types
│   │       ├── organization.ts           # Organization types
│   │       ├── secret-network.ts         # Blockchain types
│   │       ├── api.ts                    # API response types
│   │       └── global.d.ts               # Global type declarations
│   └── tests/
│       ├── __mocks__/                    # Test mocks
│       ├── components/                   # Component tests
│       ├── pages/                        # Page tests
│       ├── utils/                        # Utility function tests
│       └── setup.ts                      # Test setup configuration
│
├── backend/                              # Python Flask Backend API
│   ├── requirements.txt                  # Production dependencies
│   ├── requirements-dev.txt              # Development dependencies
│   ├── pyproject.toml                    # Python project configuration
│   ├── Dockerfile                        # Container configuration
│   ├── app.py                            # Main Flask application
│   ├── wsgi.py                           # WSGI entry point
│   ├── config/
│   │   ├── __init__.py
│   │   ├── development.py                # Development configuration
│   │   ├── production.py                 # Production configuration
│   │   └── testing.py                    # Testing configuration
│   ├── api/                              # API layer (Flask routes)
│   │   ├── __init__.py
│   │   ├── auth/                         # Authentication endpoints
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Login, register, refresh routes
│   │   │   └── decorators.py             # Auth decorators
│   │   ├── organizations/                # Organization management
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # CRUD operations for orgs
│   │   │   └── models.py                 # Pydantic models
│   │   ├── chatbots/                     # Chatbot management
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Chatbot CRUD operations
│   │   │   ├── models.py                 # Request/response models
│   │   │   └── schemas.py                # Validation schemas
│   │   ├── deployments/                  # Deployment management
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Deploy/manage endpoints
│   │   │   └── models.py                 # Deployment models
│   │   ├── chat/                         # Chat processing
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Chat endpoints
│   │   │   └── websocket.py              # WebSocket handlers
│   │   ├── billing/                      # Billing & payments
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Payment endpoints
│   │   │   └── secret_network.py         # Blockchain integration
│   │   ├── marketplace/                  # Plugin marketplace
│   │   │   ├── __init__.py
│   │   │   ├── routes.py                 # Plugin management
│   │   │   └── models.py                 # Plugin models
│   │   └── webhooks/                     # External platform webhooks
│   │       ├── __init__.py
│   │       ├── discord.py                # Discord webhook handler
│   │       ├── slack.py                  # Slack webhook handler
│   │       └── whatsapp.py               # WhatsApp webhook handler
│   ├── core/                             # Core business logic
│   │   ├── __init__.py
│   │   ├── auth/                         # Authentication logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Auth business logic
│   │   │   └── models.py                 # Auth domain models
│   │   ├── organizations/                # Organization logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Org business logic
│   │   │   ├── models.py                 # Org domain models
│   │   │   └── permissions.py            # Permission management
│   │   ├── chatbots/                     # Chatbot logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Chatbot business logic
│   │   │   ├── models.py                 # Chatbot domain models
│   │   │   └── training.py               # Training logic
│   │   ├── chat/                         # Chat processing logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Chat service
│   │   │   ├── processor.py              # Message processing
│   │   │   └── encryption.py             # Message encryption
│   │   ├── referrals/                    # Referral system logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Referral business logic
│   │   │   ├── models.py                 # Referral domain models
│   │   │   ├── reward_calculator.py      # Reward calculation logic
│   │   │   ├── code_generator.py         # Referral code generation
│   │   │   ├── tracking.py               # Conversion tracking
│   │   │   └── payment_processor.py      # USDC/USDT payments
│   │   ├── billing/                      # Billing logic
│   │   │   ├── __init__.py
│   │   │   ├── service.py                # Billing service
│   │   │   ├── secret_client.py          # Secret Network client
│   │   │   └── usage_tracker.py          # Usage tracking
│   │   └── integrations/                 # External integrations
│   │       ├── __init__.py
│   │       ├── secret_ai.py              # Secret AI integration
│   │       ├── keplr.py                  # Keplr wallet integration
│   │       ├── knowledge_sources/        # Knowledge base integrations
│   │       │   ├── __init__.py
│   │       │   ├── notion_client.py      # Notion API integration
│   │       │   ├── google_docs_client.py # Google Docs API integration
│   │       │   ├── direct_paste_processor.py # Direct content processing
│   │       │   └── base_knowledge_source.py # Base class for sources
│   │       └── platforms/                # Platform integrations
│   │           ├── __init__.py
│   │           ├── discord.py
│   │           ├── slack.py
│   │           └── whatsapp.py
│   ├── database/                         # Database layer
│   │   ├── __init__.py
│   │   ├── connection.py                 # Database connection
│   │   ├── migrations/                   # Database migrations
│   │   │   ├── alembic.ini
│   │   │   ├── env.py
│   │   │   └── versions/                 # Migration files
│   │   └── models/                       # SQLAlchemy ORM models
│   │       ├── __init__.py
│   │       ├── base.py                   # Base model class
│   │       ├── user.py                   # User model
│   │       ├── organization.py           # Organization model
│   │       ├── chatbot.py                # Chatbot model
│   │       ├── conversation.py           # Conversation model
│   │       ├── message.py                # Message model
│   │       ├── deployment.py             # Deployment model
│   │       ├── usage_log.py              # Usage tracking model
│   │       ├── plugin.py                 # Plugin model
│   │       ├── referral.py               # Referral model
│   │       ├── referral_code.py          # Referral code model
│   │       ├── referral_conversion.py    # Conversion tracking model
│   │       ├── reward.py                 # Reward transaction model
│   │       └── reward_withdrawal.py      # Withdrawal history model
│   ├── utils/                            # Utility functions
│   │   ├── __init__.py
│   │   ├── encryption.py                 # Encryption utilities
│   │   ├── validators.py                 # Data validation
│   │   ├── helpers.py                    # General helpers
│   │   └── constants.py                  # Application constants
│   ├── workers/                          # Background workers (Celery)
│   │   ├── __init__.py
│   │   ├── celery_app.py                 # Celery configuration
│   │   ├── training_worker.py            # AI training worker
│   │   ├── billing_worker.py             # Billing processing worker
│   │   └── analytics_worker.py           # Analytics worker
│   └── tests/
│       ├── conftest.py                   # Test configuration
│       ├── unit/                         # Unit tests
│       │   ├── test_auth.py
│       │   ├── test_chatbots.py
│       │   └── test_billing.py
│       ├── integration/                  # Integration tests
│       │   ├── test_api.py
│       │   └── test_secret_network.py
│       └── fixtures/                     # Test data fixtures
│           ├── users.py
│           └── organizations.py
│
├── ai-service/                           # AI Processing Service (FastAPI)
│   ├── requirements.txt                  # Python dependencies
│   ├── Dockerfile                        # Container configuration
│   ├── main.py                           # FastAPI application entry point
│   ├── config/
│   │   ├── __init__.py
│   │   └── settings.py                   # Application settings
│   ├── api/                              # API endpoints
│   │   ├── __init__.py
│   │   ├── chat.py                       # Chat processing endpoints
│   │   ├── training.py                   # Model training endpoints
│   │   └── health.py                     # Health check endpoints
│   ├── core/                             # Core AI logic
│   │   ├── __init__.py
│   │   ├── processor.py                  # Main AI processor
│   │   ├── secret_ai_client.py           # Secret AI integration
│   │   ├── tee_handler.py                # TEE operations
│   │   ├── encryption.py                 # Privacy encryption
│   │   └── context_manager.py            # Conversation context
│   ├── models/                           # Data models (Pydantic)
│   │   ├── __init__.py
│   │   ├── request.py                    # Request models
│   │   ├── response.py                   # Response models
│   │   └── training.py                   # Training models
│   ├── plugins/                          # Plugin interface
│   │   ├── __init__.py
│   │   ├── base.py                       # Base plugin class
│   │   └── secret_ai/                    # Secret AI plugin
│   │       ├── __init__.py
│   │       ├── plugin.py                 # Plugin implementation
│   │       ├── tee_processor.py          # TEE processing
│   │       └── manifest.json             # Plugin manifest
│   └── tests/
│       ├── test_processor.py             # AI processor tests
│       ├── test_secret_ai.py             # Secret AI tests
│       └── test_encryption.py            # Encryption tests
│
├── plugin-daemon/                        # Plugin Management Service
│   ├── requirements.txt                  # Python dependencies
│   ├── Dockerfile                        # Container configuration
│   ├── main.py                           # Plugin daemon main process
│   ├── core/
│   │   ├── __init__.py
│   │   ├── plugin_manager.py             # Plugin lifecycle management
│   │   ├── sandbox.py                    # Plugin sandboxing
│   │   ├── registry.py                   # Plugin registry
│   │   └── executor.py                   # Plugin execution engine
│   ├── plugins/                          # Installed plugins
│   │   ├── __init__.py
│   │   ├── base_plugin.py                # Base plugin interface
│   │   ├── ai_models/                    # AI model plugins
│   │   │   └── secret_ai/
│   │   │       ├── __init__.py
│   │   │       ├── plugin.py
│   │   │       └── config.json
│   │   ├── integrations/                 # Platform integration plugins
│   │   │   ├── discord/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── plugin.py
│   │   │   │   └── config.json
│   │   │   ├── slack/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── plugin.py
│   │   │   │   └── config.json
│   │   │   ├── whatsapp/
│   │   │   │   ├── __init__.py
│   │   │   │   ├── plugin.py
│   │   │   │   └── config.json
│   │   │   └── zapier/
│   │   │       ├── __init__.py
│   │   │       ├── plugin.py
│   │   │       └── config.json
│   │   └── utilities/                    # Utility plugins
│   │       ├── __init__.py
│   │       └── analytics/
│   │           ├── __init__.py
│   │           ├── plugin.py
│   │           └── config.json
│   ├── marketplace/
│   │   ├── __init__.py
│   │   ├── catalog.py                    # Plugin catalog management
│   │   ├── installer.py                  # Plugin installation
│   │   └── validator.py                  # Plugin validation
│   └── tests/
│       ├── test_manager.py               # Plugin manager tests
│       ├── test_sandbox.py               # Sandbox tests
│       └── test_plugins.py               # Plugin tests
│
├── gateway/                              # API Gateway Service
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── kong.yml                          # Kong configuration
│   ├── src/
│   │   ├── __init__.py
│   │   ├── plugins/
│   │   │   ├── __init__.py
│   │   │   ├── auth_plugin.py           # Keplr wallet auth
│   │   │   ├── rate_limit_plugin.py     # Per-org rate limiting
│   │   │   ├── usage_tracker.py         # SCRT billing tracker
│   │   │   └── tenant_router.py         # Multitenancy routing
│   │   ├── middleware/
│   │   │   ├── __init__.py
│   │   │   ├── cors.py                  # CORS handling
│   │   │   └── security.py              # Security headers
│   │   └── config/
│   │       ├── __init__.py
│   │       ├── routes.py                # API route definitions
│   │       └── policies.py              # Access policies
│   └── tests/
│       ├── __init__.py
│       ├── test_auth.py
│       ├── test_routing.py
│       └── test_billing.py
│
├── infrastructure/                       # Infrastructure as Code
│   ├── docker/                           # Docker configurations
│   │   ├── nginx/
│   │   │   ├── Dockerfile
│   │   │   └── nginx.conf                # Load balancer configuration
│   │   ├── postgres/
│   │   │   ├── Dockerfile
│   │   │   └── init.sql                  # Database initialization
│   │   └── redis/
│   │       ├── Dockerfile
│   │       └── redis.conf                # Cache configuration
│   ├── kubernetes/                       # Kubernetes manifests
│   │   ├── namespace.yaml                # Namespace definition
│   │   ├── configmap.yaml                # Configuration maps
│   │   ├── secrets.yaml                  # Secrets management
│   │   ├── deployments/                  # Application deployments
│   │   │   ├── frontend.yaml
│   │   │   ├── backend.yaml
│   │   │   ├── ai-service.yaml
│   │   │   └── plugin-daemon.yaml
│   │   ├── services/                     # Service definitions
│   │   │   ├── frontend-service.yaml
│   │   │   ├── backend-service.yaml
│   │   │   ├── ai-service-service.yaml
│   │   │   └── plugin-daemon-service.yaml
│   │   └── ingress/                      # Ingress configuration
│   │       └── privexbot-ingress.yaml
│   ├── terraform/                        # Infrastructure provisioning
│   │   ├── main.tf                       # Main configuration
│   │   ├── variables.tf                  # Variable definitions
│   │   ├── outputs.tf                    # Output definitions
│   │   └── modules/                      # Terraform modules
│   │       ├── vpc/                      # VPC module
│   │       │   ├── main.tf
│   │       │   ├── variables.tf
│   │       │   └── outputs.tf
│   │       ├── eks/                      # EKS cluster module
│   │       │   ├── main.tf
│   │       │   ├── variables.tf
│   │       │   └── outputs.tf
│   │       └── rds/                      # RDS database module
│   │           ├── main.tf
│   │           ├── variables.tf
│   │           └── outputs.tf
│   └── monitoring/                       # Monitoring configurations
│       ├── prometheus/
│       │   ├── prometheus.yml
│       │   └── rules.yml
│       ├── grafana/
│       │   ├── dashboards/
│       │   └── provisioning/
│       └── alertmanager/
│           └── alertmanager.yml
│
├── docs/                                 # Documentation
│   ├── README.md                         # Project overview
│   ├── ARCHITECTURE.md                   # Architecture documentation
│   ├── API.md                            # API documentation
│   ├── DEPLOYMENT.md                     # Deployment guide
│   ├── SECURITY.md                       # Security guidelines
│   ├── CONTRIBUTING.md                   # Contribution guidelines
│   ├── api/                              # API documentation
│   │   ├── openapi.yaml                  # OpenAPI specification
│   │   └── postman/                      # Postman collections
│   ├── guides/                           # User guides
│   │   ├── getting-started.md
│   │   ├── creating-chatbots.md
│   │   ├── deploying-bots.md
│   │   └── managing-billing.md
│   └── architecture/                     # Architecture diagrams
│       ├── system-overview.mmd
│       ├── data-flow.mmd
│       └── security-model.mmd
│
├── scripts/                              # Utility scripts
│   ├── setup.sh                          # Environment setup
│   ├── deploy.sh                         # Deployment script
│   ├── backup.sh                         # Database backup
│   ├── migrate.sh                        # Database migration
│   ├── test.sh                           # Test runner
│   └── generate-docs.sh                  # Documentation generation
│
└── tests/                                # End-to-end tests
    ├── e2e/                              # Playwright E2E tests
    │   ├── auth.spec.ts
    │   ├── chatbot-creation.spec.ts
    │   ├── deployment.spec.ts
    │   └── billing.spec.ts
    ├── integration/                      # Service integration tests
    │   ├── api-ai-service.test.py
    │   ├── plugin-daemon.test.py
    │   └── secret-network.test.py
    ├── load/                             # Load testing
    │   ├── chat-load.js
    │   └── api-load.js
    └── security/                         # Security tests
        ├── auth-security.test.py
        ├── data-encryption.test.py
     
```

### 🧱 Why This Structure? (For Beginners)

- **Frontend**: What users see and interact with
- **Backend**: The brain that processes requests and manages data.
- **AI Service**: A specialized service dedicated to AI processing
- **Plugin Daemon**: Manages add-on and workflow features
- **Infrastructure**: Handles deployment, networking, and configuration


---

## Frontend User Experience & Flow Architecture

### User Journey Overview

PrivexBot's frontend is designed around four main user types with distinct journeys:

1. **Individual Users (Free)**: Landing → Signup → Create Chatbot (Free Plan)
2. **Individual Users (Paid)**: Free User → Connect Wallet → Upgrade Plan → Premium Features
3. **Organization Users**: Individual User → Create Organization → Team Collaboration
4. **Public Visitors**: Explore → Templates/Demos → Signup → Individual User

### Core Navigation Structure

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Public Pages   │ -> │  Authentication │ -> │ Personal Space  │ -> │  Organization   │
│                 │    │                 │    │                 │    │   (Optional)    │
│ • Landing       │    │ • Sign In       │    │ • My Chatbots   │    │ • Team Space    │
│ • Explore       │    │ • Sign Up       │    │ • Studio        │    │ • Shared Bots   │
│ • Pricing       │    │ • Verify Email  │    │ • Marketplace   │    │ • Team Settings │
│ • Docs          │    │ • Connect Wallet│    │ • Billing       │    │ • Collaboration │
│ • Showcase      │    │   (Optional)    │    │ • Profile       │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Detailed User Flows

#### 1. Individual User Onboarding Flow (Simplified)

```mermaid
graph TD
    A[Landing Page] --> B{User Intent?}
    B -->|Explore| C[Browse Templates]
    B -->|Get Started| D[Sign Up]
    B -->|Learn More| E[Documentation]

    C --> F[Template Preview]
    F --> D

    D --> G{Auth Method?}
    G -->|Email| H[Email Signup]
    G -->|Keplr Wallet| I[Connect Keplr]

    H --> J[Email Verification]
    I --> K[Wallet Connected]
    J --> L[Personal Dashboard]
    K --> L

    L --> M[Welcome Tour]
    M --> N[Create First Chatbot - FREE]
    N --> O[Basic Studio Access]
    O --> P[Deploy with Limitations]
    P --> Q{Upgrade Needed?}
    Q -->|Yes| R[Connect Wallet & Upgrade]
    Q -->|No| S[Continue with Free Plan]

    R --> T[Premium Features Unlocked]
    S --> U[Free Plan Features]
```

#### 2. Organization Creation Flow (Optional)

```mermaid
graph TD
    A[Individual User Dashboard] --> B{Create Organization?}
    B -->|Yes| C[Create Organization Button]
    B -->|No| D[Continue Individual Use]

    C --> E[Organization Setup Form]
    E --> F[Invite Team Members]
    F --> G[Set Organization Plan]
    G --> H{Payment Required?}
    H -->|Yes| I[Connect Wallet Required]
    H -->|No| J[Free Organization Plan]

    I --> K[Payment with SCRT/SNIP-20]
    K --> L[Organization Created]
    J --> L

    L --> M[Send Email Invitations]
    M --> N[Team Dashboard]
    N --> O[Collaborative Features]

    D --> P[Personal Workspace]
    P --> Q[Individual Features Only]
```

#### 3. Payment & Upgrade Flow

```mermaid
graph TD
    A[Free Plan User] --> B{Upgrade Trigger?}
    B -->|Hit Limits| C[Usage Limit Notification]
    B -->|Want Features| D[Upgrade Button Clicked]
    B -->|Organization Invite| E[Join Organization]

    C --> F[Upgrade Prompt]
    D --> F

    F --> G{Wallet Connected?}
    G -->|No| H[Connect Keplr Wallet]
    G -->|Yes| I[Select Plan]

    H --> J[Wallet Connection Flow]
    J --> K[Wallet Connected Successfully]
    K --> I

    I --> L[Review Plan Features]
    L --> M[Payment Method Selection]
    M --> N[SCRT/SNIP-20/Crypto Payment]
    N --> O[Transaction Confirmation]
    O --> P[Plan Activated]
    P --> Q[Send Confirmation Email]
    Q --> R[Premium Features Unlocked]

    E --> S[Accept Invitation Email]
    S --> T[Join Organization]
    T --> U[Organization Features]
```

#### 4. Studio Workflow (Core Experience)

```mermaid
graph TB
    subgraph "Studio Entry Points"
        A[Create New Bot]
        B[Edit Existing Bot]
        C[Use Template]
    end

    subgraph "Studio Workspace"
        D[Design Canvas]
        E[Node Library]
        F[Property Panel]
        G[Preview Panel]
        H[Version Control]
    end

    subgraph "Configuration Tabs"
        I[Configure Bot]
        J[Knowledge Base]
        K[Chat Flow]
        L[Workflows]
        M[Agents]
        N[Test & Preview]
    end

    subgraph "Publishing Flow"
        O[Quality Checklist]
        P[Pre-publish Review]
        Q[Deploy Options]
        R[Go Live]
    end

    A --> D
    B --> D
    C --> D

    D --> E
    D --> F
    D --> G
    D --> H

    F --> I
    F --> J
    F --> K
    F --> L
    F --> M
    F --> N

    N --> O
    O --> P
    P --> Q
    Q --> R
```

#### 3. Marketplace Experience

```mermaid
graph LR
    A[Marketplace Home] --> B[Browse Plugins]
    A --> C[Featured Plugins]
    A --> D[My Installed]

    B --> E[Plugin Details]
    C --> E

    E --> F{Action?}
    F -->|Install| G[Installation Flow]
    F -->|Review| H[Plugin Reviews]
    F -->|Test| I[Plugin Tester]

    G --> J[Configure Plugin]
    J --> K[Activate Plugin]

    D --> L[Manage Installed]
    L --> M[Configure Existing]
    L --> N[Uninstall Plugin]

    O[Publish Plugin] --> P[Upload Plugin]
    P --> Q[Plugin Review]
    Q --> R[Submit for Approval]
```

### Referral Program Flow

```mermaid
graph TD
    A[Existing User] --> B[Generate Referral Link/Code]
    B --> C[Share via Email/Social/Direct]
    C --> D[New User Clicks Link]
    D --> E[Referral Code Applied to Signup]
    E --> F[New User Registers]
    F --> G[New User Uses Free Plan]
    G --> H{User Upgrades to Premium?}
    H -->|Yes| I[Payment Processed]
    H -->|No| J[Continue Tracking]
    I --> K[Referral Reward Triggered]
    K --> L[USDC/USDT Reward Credited]
    L --> M[Notification Sent]
    J --> N[7-day Follow-up Email]
    N --> H
```

🔑 Some Key Features Implemented

Staking System:

- Exactly 1 month free Starter access for any 3+ month staking
- 30-day countdown tracking
- One-time benefit enforcement
- Clear UI messaging

Notion Integration:

- Integration token authentication
- Page and database content extraction
- Workspace-wide sync option
- Rate-limited API calls

Google Docs Integration:

- OAuth2 authentication
- Document, folder, and shared drive support
- Rich text extraction from complex structures
- Drive API metadata integration

Direct Paste:

- Multi-format support (text/markdown/HTML)
- Content cleaning and validation
- Tagging system
- Batch processing interface
