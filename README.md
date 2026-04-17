# Trade Insight Daily — Global AI-Powered Trading Intelligence Platform

> **Architecture Version:** 1.0.0  
> **Scale Target:** 10M+ Users  
> **Status:** Pre-Development Blueprint

---

## Table of Contents

1. [Product Overview](#1-product-overview)
2. [Core Philosophy](#2-core-philosophy)
3. [Feature Breakdown](#3-feature-breakdown)
4. [AI Pipeline Architecture](#4-ai-pipeline-architecture)
5. [Admin Panel System](#5-admin-panel-system)
6. [Content Delivery System](#6-content-delivery-system)
7. [Access Control Logic](#7-access-control-logic)
8. [Multi-Language Architecture](#8-multi-language-architecture)
9. [Payment System Design](#9-payment-system-design)
10. [Growth System](#10-growth-system)
11. [UI/UX Layout System](#11-uiux-layout-system)
12. [Tech Stack](#12-tech-stack)
13. [Folder Structure](#13-folder-structure)
14. [Scalability Strategy](#14-scalability-strategy)
15. [Cost Optimization Strategy](#15-cost-optimization-strategy)

---

## 1. Product Overview

**Trade Insight Daily** is a global, AI-powered trading intelligence platform designed to democratize professional-grade fundamental analysis for traders of all levels. The platform transforms complex market intelligence — economic data, central bank speeches, COT reports, news flow — into structured, explainable, actionable insights.

### What Makes This Different

| Dimension | Traditional Platforms | Trade Insight Daily |
|---|---|---|
| Analysis depth | Raw data only | AI-explained + contextualized |
| Skill targeting | Expert-only | Beginner → Advanced continuum |
| Language | English only | 10+ languages, SEO-native |
| AI backend | Single model | Multi-model pipeline with fallback |
| Access model | Hard paywall | Graduated unlock (free → referral → paid) |
| Admin control | Static | Fully dynamic, zero redeploy |

---

## 2. Core Philosophy

### Design Principles

**1. Explain Everything.**  
Every data point comes with three layers: *What is this?* → *Why does it matter?* → *What could happen next?*

**2. Progressive Access.**  
Users move from curiosity (free) → engagement (referral/task) → investment (paid). No hard walls that kill SEO.

**3. Admin-First Architecture.**  
No feature, price, prompt, or content block should require a code deployment to change. The admin panel is the operating system of the product.

**4. AI as Infrastructure.**  
AI is not a feature — it is the delivery pipeline. Every insight, translation, and explanation flows through a controlled, observable, cost-optimized AI system.

**5. Global by Default.**  
Every URL, every translation, every payment method is first-class. No "international" as an afterthought.

---

## 3. Feature Breakdown

### 3.1 Daily Fundamental Insight

The flagship content engine. Produces structured market insights on currency pairs, commodities, indices.

**Workflow:**
```
Data Sources → AI Ingestion Pipeline → Draft Generation → Admin Review → Edit → Publish → Multi-language Push
```

**Content Structure per Insight:**
- Market context summary
- Key driver analysis (macro, central bank, data)
- Beginner explanation block
- Advanced analysis block
- "What to watch" forward-looking section
- Sentiment tag (bullish / bearish / neutral / mixed)
- Impact score (1–5)

**Admin Controls:**
- Enable/disable insight categories
- Override AI output before publish
- Schedule publish times per timezone
- Toggle beginner/advanced block visibility
- Pin or expire insights

---

### 3.2 Smart Economic Calendar

Not a copy of Forex Factory. An intelligent calendar that teaches while it informs.

**Core Functionality:**
- Events filtered by currency, impact level, region
- Each event includes:
  - AI-generated "what is this event" explanation
  - Historical outcomes: previous releases vs. market reactions
  - Impact probability model (low / medium / high / extreme)
  - Beginner tooltip: plain-language explanation
  - Advanced block: nuanced macro context
- Live countdown to next high-impact event
- Push notification system (web + mobile)

**Data Sources:**
- Primary: Investing.com API / ForexFactory scrape (licensed or scraped per ToS)
- Backup: Trading Economics API
- Enrichment: AI-powered contextual layer on top of raw data

---

### 3.3 Smart COT Report

Commitment of Traders data made readable. CFTC data is publicly available but nearly unreadable for most traders.

**Core Functionality:**
- Weekly COT data parser (CFTC.gov)
- Simplified display: Net positions, change week-over-week, trend direction
- Historical chart (8-week, 26-week, 52-week)
- Filters: by asset class (FX, commodities, indices)
- AI explanation: "What does this week's positioning mean?"
- Positioning extremes alert (when commercials/non-commercials hit historical thresholds)

**Data Pipeline:**
```
CFTC.gov (weekly TXT/CSV) → Parser → DB → AI Enrichment → Cached API → Frontend
```

---

### 3.4 Speech Decoder (Flagship Feature)

Real-time AI interpretation of central bank speeches, press conferences, and policy statements.

**Event Types:**
- FOMC, ECB, BOE, BOJ, RBA, BOC, RBNZ, SNB
- Treasury Secretary / Finance Minister statements
- IMF / World Bank / BIS publications

**Real-Time Flow:**
```
Live Speech Event Announced → Admin Activates Decoder Mode →
Transcript Input (manual paste / live API) →
Chunk-by-chunk AI analysis →
Key phrase highlighting →
Hawkish / Dovish / Neutral scoring per paragraph →
Live feed to users (WebSocket) →
Post-event summary generation
```

**Event-Driven Architecture:**
- Admin "opens" a decoder session with metadata (speaker, event, currency pairs)
- System switches to streaming AI mode (Server-Sent Events or WebSocket)
- Users see live analysis as it's generated
- Session archived after close with full transcript + analysis

---

### 3.5 AI News Intelligence

Filtered, explained, contextualized financial news.

**Core Functionality:**
- Multi-source news ingestion (RSS, APIs)
- AI triage: relevance scoring per currency/asset
- Impact classification: market-moving vs. background noise
- Beginner explanation block per news item
- Sentiment tagging: hawkish / dovish / risk-on / risk-off / neutral
- "Related insight" linking (connects news to COT, calendar, or insight)

**Sources:**
- Reuters, Bloomberg RSS (public)
- Newsdata.io / Currents API (low cost)
- Custom RSS parser for central bank websites

---

## 4. AI Pipeline Architecture

### 4.1 Multi-Model Overview

The platform routes AI tasks across five model families based on cost, capability, and latency requirements.

| Model | Primary Use Case | Cost Tier | Fallback Priority |
|---|---|---|---|
| Claude (Anthropic) | Deep analysis, speech decoding, nuanced interpretation | Medium | 1st fallback |
| GPT-4o (OpenAI) | Default analysis, structured output, JSON generation | Medium | Primary |
| Gemini 1.5 Pro | Long-context tasks, document analysis | Medium | 2nd fallback |
| Perplexity | Real-time web-grounded summaries, news context | Low-Medium | Specialized |
| Grok (xAI) | Social sentiment context, real-time events | Low | Specialized |
| Gemini Flash / GPT-4o-mini | Translation, beginner explanations, low-stakes tasks | Low | Cost optimization |

---

### 4.2 Pipeline Execution Engine

Every AI task flows through a **Pipeline Execution Engine (PEE)**. No direct API calls are made from feature code.

```
Feature Request
      ↓
Pipeline Resolver (looks up pipeline by task_type)
      ↓
Variable Mapper (injects context into prompt template)
      ↓
Model Selector (selects model based on task config)
      ↓
Cost Gate (checks daily/monthly budget limit)
      ↓
API Executor (calls selected model)
      ↓
Output Validator (checks format, length, safety)
      ↓
Fallback Trigger (if failed → next model in chain)
      ↓
Response Stored + Returned
```

---

### 4.3 Prompt Architecture

All prompts live in the database, not in code. Admin can modify any prompt without redeployment.

**Prompt Schema:**
```json
{
  "id": "uuid",
  "name": "daily_insight_analysis",
  "task_type": "insight_generation",
  "version": 3,
  "model_primary": "gpt-4o",
  "model_fallback": ["claude-3-5-sonnet", "gemini-1.5-pro"],
  "system_prompt": "You are a professional fundamental analyst...",
  "user_prompt_template": "Analyze {{currency_pair}} given the following context: {{context_block}}. Output format: {{output_schema}}",
  "variables": ["currency_pair", "context_block", "output_schema"],
  "max_tokens": 1500,
  "temperature": 0.4,
  "output_format": "json",
  "output_schema": { "summary": "string", "drivers": "array", "sentiment": "string" },
  "cost_tier": "medium",
  "active": true,
  "created_at": "timestamp",
  "updated_at": "timestamp"
}
```

---

### 4.4 Variable Injection System

Each pipeline has a defined set of input variables. The system resolves these from:

- **Static context:** Admin-defined global context (e.g., current market regime description)
- **Dynamic context:** Live data fetched at runtime (COT data, calendar events, price levels)
- **User context:** User tier, language preference
- **Feature context:** The specific data being analyzed

```javascript
// Variable resolution order:
// 1. Feature-level inputs (highest priority)
// 2. Dynamic runtime data
// 3. Admin-defined static context
// 4. System defaults (lowest priority)

const resolvedPrompt = variableMapper.resolve(promptTemplate, {
  currency_pair: "EURUSD",
  context_block: buildContextBlock({ cot, calendar, news }),
  output_schema: JSON.stringify(outputSchema),
});
```

---

### 4.5 Prompt Chaining

Complex tasks (e.g., generating a full daily insight) are broken into chained steps:

```
Step 1: Data Summarizer (cheap model - Gemini Flash)
  Input: Raw economic data, news, COT
  Output: Structured context JSON

Step 2: Analysis Generator (primary model - GPT-4o)
  Input: Context JSON from Step 1 + prompt template
  Output: Draft analysis with sections

Step 3: Beginner Explainer (cheap model - GPT-4o-mini)
  Input: Analysis from Step 2
  Output: Plain-language beginner block

Step 4: Quality Validator (Claude)
  Input: Full draft output
  Output: Validated / flagged / revised output

Step 5: Translation Dispatcher (Gemini Flash per language)
  Input: Final English content
  Output: Translated variants (async)
```

Each step writes output to a shared **pipeline context store** (Redis-backed). Steps can be re-run individually without restarting the full chain.

---

### 4.6 Fallback System

```
Primary Model API Call
    ↓ (if error / timeout / rate limit)
Fallback Model 1
    ↓ (if also failed)
Fallback Model 2
    ↓ (if all failed)
Cached Last-Known Output (stale flag added)
    ↓ (if no cache)
Graceful Error State (user sees placeholder, admin alerted)
```

Fallback triggers:
- HTTP 429 (rate limit)
- HTTP 500/503 (provider error)
- Timeout > 30s
- Output validation failure (malformed JSON, missing required fields)
- Content policy rejection

---

### 4.7 Cost Optimization Routing

**Rule Engine (Admin-Configurable):**

```
IF task_type = "translation" → use gemini-flash (lowest cost)
IF task_type = "beginner_explanation" → use gpt-4o-mini
IF task_type = "news_triage" → use gpt-4o-mini
IF task_type = "deep_analysis" AND time = "market_hours" → use gpt-4o
IF task_type = "deep_analysis" AND time = "off_hours" → use claude-3-5-haiku
IF daily_spend > 80% of budget → downgrade all non-critical tasks by one tier
IF daily_spend > 95% of budget → freeze non-critical AI tasks, serve cached content
```

All costs are tracked per: task type, model, pipeline, and date. Admin dashboard shows real-time AI spend.

---

## 5. Admin Panel System

The Admin Panel is the operating system of the product. Zero-redeploy control over every system.

### 5.1 Module Map

```
Admin Panel
├── Dashboard
│   ├── Real-time user stats
│   ├── AI cost tracker (daily / monthly)
│   ├── Content publish queue
│   └── System health (API status, error rates)
│
├── Content Manager
│   ├── Insights (Draft → Review → Publish)
│   ├── Economic Calendar (event enrichment override)
│   ├── COT Report (publish cycle control)
│   ├── News (manual approve / suppress)
│   └── Speech Decoder (session management)
│
├── AI Pipeline Manager
│   ├── Prompt Library (CRUD, versioning, A/B test)
│   ├── Pipeline Builder (drag-chain steps)
│   ├── Model Config (assign models per pipeline)
│   ├── Cost Rules (routing budget rules)
│   └── Pipeline Run Logs (per-run audit)
│
├── Feature Access Manager
│   ├── Feature flag toggle (per plan tier)
│   ├── Content block visibility rules
│   ├── Guest access percentage (per page)
│   └── Teaser content selector
│
├── User Manager
│   ├── User list + tier override
│   ├── Manual premium grant
│   ├── Referral audit log
│   └── Ban / suspend / impersonate
│
├── Translation Manager
│   ├── Language toggle (enable/disable per language)
│   ├── Translation queue (review before publish)
│   ├── Manual override per translation unit
│   └── Language-specific SEO meta editor
│
├── Payment Manager
│   ├── Plan builder (price, features, duration)
│   ├── Payment gateway toggle per country
│   ├── Coupon / discount system
│   ├── Revenue dashboard
│   └── Refund manager
│
├── Growth Manager
│   ├── Referral config (reward rules, caps, expiry)
│   ├── Task builder (define tasks + rewards)
│   ├── Leaderboard controls
│   └── Campaign manager
│
├── Ads Manager
│   ├── Ad placement toggle per page/section
│   ├── Ad network config (AdSense, custom)
│   ├── Ad suppression rules (premium users, regions)
│   └── Revenue tracking
│
└── System Settings
    ├── Global feature flags
    ├── Maintenance mode
    ├── API key manager (all AI + payment providers)
    ├── Email / notification config
    └── Admin user management (roles, permissions)
```

---

### 5.2 Admin Authentication

Separate auth system from user auth. Admin users have:
- Email + password + TOTP (mandatory 2FA)
- Role-based: `super_admin`, `editor`, `analyst`, `support`, `finance`
- Action audit log (every admin action logged with timestamp, IP, user)
- Session timeout: 2 hours inactivity

---

## 6. Content Delivery System

### 6.1 Content Pipeline

```
Raw Input (data / AI draft / manual)
      ↓
Draft State → stored in DB, not public
      ↓
Admin Review → editor sees preview, can edit in-place
      ↓
Approved State → translation dispatch triggered
      ↓
Translation Complete (per language) → language-specific publish
      ↓
Published State → CDN cache invalidated, SEO meta pushed
      ↓
Scheduled Expiry (optional) → auto-archive after N days
```

---

### 6.2 Content Caching Strategy

| Content Type | Cache Layer | TTL | Invalidation Trigger |
|---|---|---|---|
| Published insights | CDN edge + Redis | 1 hour | Admin publish action |
| Economic calendar | Redis | 15 minutes | Data source update |
| COT data | Redis | 24 hours | Weekly CFTC release |
| News feed | Redis | 5 minutes | New ingest cycle |
| Speech decoder | No cache (live) | N/A | Session-based |
| User-specific (plans, access) | Redis | 5 minutes | Auth event / plan change |
| Static pages | CDN edge | 24 hours | Deploy / admin trigger |

---

### 6.3 SEO Content Structure

Every content page outputs:
- Canonical URL per language (`/en/insights/eurusd-analysis`, `/bn/insights/eurusd-analysis`)
- OpenGraph + Twitter Card meta
- JSON-LD structured data (Article, FinancialProduct where applicable)
- Sitemap entry (auto-generated, language-specific)
- Robots directive (public portion: `index, follow` | locked portion: `noindex`)

---

## 7. Access Control Logic

### 7.1 Access Tiers

| Tier | How to Get | Access Level |
|---|---|---|
| Guest (unauthenticated) | Default | Landing page full + 20–30% of content pages |
| Free (authenticated) | Email signup | ~50% of features, limited history |
| Growth (referral/task earned) | Complete tasks or refer users | ~80% of features, extended history |
| Premium (paid) | Subscription | 100% of features, full history, priority speed |
| Admin | Manual grant | All features + admin panel |

---

### 7.2 Content Locking Engine

Content blocks are tagged with visibility rules. The rendering engine evaluates these rules per request.

**Block Visibility Schema:**
```json
{
  "block_id": "insight_advanced_analysis",
  "required_tier": "premium",
  "fallback_mode": "blur_teaser",
  "teaser_line_count": 3,
  "teaser_blur": true,
  "lock_message": "Upgrade to Premium to read the full analysis",
  "cta_type": "upgrade_modal"
}
```

**Fallback Modes:**
- `blur_teaser` — show N lines, blur the rest, CTA overlay
- `hidden` — block does not render at all
- `placeholder` — show a styled placeholder card with CTA
- `full_visible` — available to current tier

---

### 7.3 Guest SEO Mode

For unauthenticated users, pages render in a hybrid mode:
- Full hero section, intro paragraph, first insight summary → indexed by search engines
- Advanced blocks, historical data, AI analysis → replaced with teaser + CTA
- Page is structurally complete (no JavaScript-only content for locked sections)
- SSR ensures Google sees the open portion fully rendered

This ensures SEO value is captured without giving away premium content.

---

### 7.4 Feature Flag Matrix

Every feature has a flag in the admin panel. Flags are evaluated server-side per request.

```
feature_flags table:
  id, feature_key, min_tier, is_enabled, enabled_for_regions[], disabled_for_regions[], notes
```

Example:
```
speech_decoder     | premium  | true  | [] | []
cot_report_basic   | free     | true  | [] | []
cot_report_history | growth   | true  | [] | []
ai_news_full       | premium  | true  | [] | []
```

---

## 8. Multi-Language Architecture

### 8.1 URL Structure

```
tradeinsightdaily.com/en/   → English (default, canonical)
tradeinsightdaily.com/bn/   → Bengali
tradeinsightdaily.com/in/   → Hindi (India)
tradeinsightdaily.com/ar/   → Arabic
tradeinsightdaily.com/es/   → Spanish
tradeinsightdaily.com/pt/   → Portuguese (Brazil)
tradeinsightdaily.com/id/   → Bahasa Indonesia
tradeinsightdaily.com/tr/   → Turkish
tradeinsightdaily.com/zh/   → Simplified Chinese
tradeinsightdaily.com/ja/   → Japanese
```

Each language path is a fully server-rendered, independently indexed page. `hreflang` tags on all pages point to all language variants.

---

### 8.2 Translation Pipeline

```
English Content Published
      ↓
Translation Job Created (per enabled language)
      ↓
AI Translation (Gemini Flash or GPT-4o-mini)
  - Uses specialized translation prompt
  - Preserves HTML structure, financial terminology
  - Context-aware (trading domain vocabulary)
      ↓
Translation Draft Stored
      ↓
Admin Review Queue (translator/editor can edit)
      ↓
Approved → Published to language path
      ↓
SEO meta also translated + submitted to sitemap
```

---

### 8.3 Translation Memory

To avoid re-translating repeated phrases and reduce costs:
- All translated segments stored in `translation_memory` table
- Before sending to AI: segment looked up in memory first
- Match threshold: 95%+ similarity → reuse without AI call
- Cost reduction: ~40–60% on repeated content

---

### 8.4 Translation DB Schema (simplified)

```
translations:
  id, content_id, content_type, language_code,
  original_hash, translated_text, status (draft/approved/published),
  translated_by (ai/human), reviewed_by, created_at, updated_at

translation_memory:
  id, source_text_hash, language_code, translated_text,
  domain (financial/general/ui), use_count, created_at
```

---

## 9. Payment System Design

### 9.1 Architecture: Modular Payment Abstraction Layer

No direct payment provider calls from feature code. All payments route through a **Payment Abstraction Layer (PAL)**.

```
User Initiates Purchase
      ↓
PAL: Resolve Payment Method
  → Country detection → Country→Provider mapping
      ↓
PAL: Create Payment Intent
  → Provider-specific SDK called
      ↓
Provider Checkout / Redirect
      ↓
Webhook Received (provider → PAL)
      ↓
PAL: Normalize Event (provider-agnostic format)
      ↓
Subscription Service: Grant / Update / Cancel access
      ↓
User Notified (email + in-app)
```

---

### 9.2 Provider Matrix

| Provider | Use Case | Countries |
|---|---|---|
| Stripe | Cards, Apple Pay, Google Pay, SEPA, Link | Global (140+ countries) |
| PayPal | Alternative wallet | Global |
| Coinbase Commerce / NOWPayments | Crypto (BTC, ETH, USDT) | Global |
| SSLCommerz / ShurjoPay | bKash, Nagad, Rocket | Bangladesh |
| Razorpay | UPI, NetBanking, Wallets | India |
| Mercado Pago | Pix, Boleto | Brazil / LatAm |
| Midtrans | GoPay, OVO, QRIS | Indonesia |
| PayTR / Iyzico | Local cards | Turkey |

---

### 9.3 Country-to-Provider Routing

```json
{
  "BD": { "primary": "sslcommerz", "secondary": "stripe", "crypto": "nowpayments" },
  "IN": { "primary": "razorpay", "secondary": "stripe", "crypto": "nowpayments" },
  "BR": { "primary": "mercadopago", "secondary": "stripe", "crypto": "nowpayments" },
  "ID": { "primary": "midtrans", "secondary": "stripe", "crypto": "nowpayments" },
  "TR": { "primary": "iyzico", "secondary": "stripe", "crypto": "nowpayments" },
  "DEFAULT": { "primary": "stripe", "crypto": "nowpayments" }
}
```

Admin can update this mapping without code changes.

---

### 9.4 Subscription Plans

Plans are fully dynamic — created and modified in admin panel.

**Default Plan Structure:**
```
Free        → $0/month   → Tier: free
Growth      → $0 earned  → Tier: growth (referral/task based)
Premium     → $9.99/month (or regional pricing)
Premium Annual → $79.99/year
```

**Regional Pricing (PPP-adjusted):**
- Bangladesh: ~$2.99/month
- India: ~$3.99/month
- Indonesia: ~$3.49/month
Admin sets regional price per plan per country code.

---

## 10. Growth System

### 10.1 Referral System

**How It Works:**
1. User gets unique referral link (`/ref/USERNAME`)
2. Referred user signs up → referral attributed
3. When referred user completes a qualifying action (e.g., first login + 3 days active) → reward triggers
4. Referring user earns: Growth tier days, premium days, or credits (admin-configurable)

**Fraud Prevention:**
- Device fingerprint check on signup
- IP range deduplication
- Self-referral blocked
- Reward held for 7 days (chargeback window)
- Max referral reward per month (admin-set cap)

---

### 10.2 Task-Based Unlock System ("Promote → Earn Premium")

Users earn premium access by completing tasks. Tasks are admin-defined.

**Task Types:**
```
share_on_social     → Share a page/insight on X, Facebook, LinkedIn
write_review        → Leave a review on a platform
follow_social       → Follow platform accounts
join_community      → Join Telegram/Discord
submit_feedback     → Complete a survey
watch_tutorial      → Complete an educational module
invite_friends      → Refer N users who activate
```

**Task Schema:**
```json
{
  "id": "task_001",
  "title": "Share your first insight on X",
  "description": "Share any insight on X (Twitter) to unlock 7 days of Growth access",
  "reward_type": "tier_upgrade",
  "reward_tier": "growth",
  "reward_duration_days": 7,
  "verification_type": "url_proof",
  "max_completions_per_user": 1,
  "is_active": true
}
```

**Verification Methods:**
- `url_proof` — user submits URL, admin reviews
- `oauth_check` — platform OAuth confirms action (e.g., Twitter follow)
- `honor_system` — auto-granted (for low-stakes tasks)
- `admin_manual` — admin reviews and approves

---

### 10.3 Rewards Engine

Rewards are modular and stackable:

```
reward_type options:
  - tier_upgrade (free → growth → premium)
  - tier_extension (extend current tier N days)
  - feature_unlock (unlock specific feature N days)
  - credits (internal currency for future use)
```

All reward rules configurable by admin without redeploy.

---

## 11. UI/UX Layout System

### 11.1 Layout Architecture

**Mobile (< 768px):**
```
┌─────────────────────────────┐
│  Header (Logo + Auth CTA)   │
├─────────────────────────────┤
│                             │
│       Page Content          │
│                             │
├─────────────────────────────┤
│  Bottom Nav (5 icons max)   │
└─────────────────────────────┘
```

**Desktop (≥ 1024px):**
```
┌──────────┬──────────────────────────────┐
│          │  Topbar (minimal)            │
│ Sidebar  ├──────────────────────────────┤
│ (240px)  │                              │
│          │       Page Content           │
│  Nav     │                              │
│  Items   │                              │
│          │                              │
└──────────┴──────────────────────────────┘
```

**Guest / Unauthenticated:**
```
┌─────────────────────────────┐
│  Minimal Topbar             │
├─────────────────────────────┤
│                             │
│  Landing / SEO Content      │
│  (No sidebar, no nav)       │
│                             │
└─────────────────────────────┘
```

---

### 11.2 Layout Component Hierarchy

```
RootLayout
├── AuthenticatedLayout
│   ├── Sidebar (desktop)
│   ├── MobileHeader
│   ├── BottomNav (mobile)
│   └── PageContent
└── GuestLayout
    ├── MinimalHeader
    └── PageContent
```

Layout selection happens at the middleware/route level — no layout flash.

---

### 11.3 Content Lock UI Patterns

**Blur Teaser:**
```
┌───────────────────────────────────┐
│ [Visible paragraph text]          │
│ [Visible paragraph text]          │
│ ██████████████████████████████    │  ← blurred
│ ██████████████ ████████████████   │  ← blurred
│  ┌─────────────────────────────┐  │
│  │ 🔒 Unlock Full Analysis     │  │  ← CTA overlay
│  │    Upgrade to Premium →     │  │
│  └─────────────────────────────┘  │
└───────────────────────────────────┘
```

**Placeholder Lock:**
```
┌───────────────────────────────────┐
│  ┌─────────────────────────────┐  │
│  │ 📊 Advanced Analysis        │  │
│  │ Available for Premium users │  │
│  │                             │  │
│  │  [Start Free Trial]         │  │
│  └─────────────────────────────┘  │
└───────────────────────────────────┘
```

---

## 12. Tech Stack

> **Rule:** Every choice is justified. Dev = cheap/free to start. Prod = scalable.

---

### 12.1 Frontend

| Concern | Dev Choice | Prod Choice | Justification |
|---|---|---|---|
| Framework | **Next.js 14 (App Router)** | Same | App Router enables per-route SSR/SSG/ISR. RSC reduces JS bundle. Built-in i18n routing. |
| Styling | **Tailwind CSS** | Same | Utility-first, zero runtime CSS. Purges unused styles. Fastest iteration. |
| Component Library | **shadcn/ui** | Same | Unstyled, composable, accessible. Owned by the project (copy-paste, not npm-locked). |
| State Management | **Zustand** | Same | Minimal API. No boilerplate. Scales from small to large without re-architecture. |
| Data Fetching | **TanStack Query** | Same | Cache management, background refetch, optimistic updates. Essential for real-time feed. |
| Forms | **React Hook Form + Zod** | Same | Performant, schema-validated, no re-render overhead. |
| Charts | **Recharts** | Same | React-native, composable, no canvas overhead. Recharts for standard; D3 direct for complex COT charts. |
| Animation | **Framer Motion** | Same | Production-grade animation with exit animations. Key for lock overlays. |
| Internationalization | **next-intl** | Same | Designed for Next.js App Router. Type-safe, locale-based routing, ICU message format. |

---

### 12.2 Backend

| Concern | Dev Choice | Prod Choice | Justification |
|---|---|---|---|
| Runtime | **Node.js (via Next.js API Routes)** | **Node.js + Separate Express/Fastify services** | Next.js routes sufficient for dev. In prod, AI pipeline, payment webhooks, and real-time features split into dedicated services. |
| API Style | **REST + tRPC (internal)** | Same | tRPC for type-safe internal Next.js communication. REST for external webhooks (Stripe, etc.). |
| Background Jobs | **BullMQ (dev: local Redis)** | **BullMQ + Redis (Upstash or self-hosted)** | BullMQ is the best Node.js queue. Handles AI pipeline jobs, translation dispatch, scheduled publishing. |
| Real-time (Speech Decoder) | **Server-Sent Events (SSE)** | **SSE + Ably (if scale demands)** | SSE sufficient for one-way streams. No overhead of WebSocket for speech decoder feed. Ably as managed fallback at scale. |
| Cron / Scheduling | **node-cron (dev)** | **Inngest** | Inngest provides durable, observable, retryable scheduled functions. Handles COT parse schedule, calendar refresh, etc. |

---

### 12.3 Database

| Concern | Dev Choice | Prod Choice | Justification |
|---|---|---|---|
| Primary DB | **PostgreSQL (local / Supabase free tier)** | **PostgreSQL on Neon (serverless)** | JSONB for flexible AI output storage. Full ACID. Best ORM ecosystem. Neon = serverless scaling + branching for zero-downtime migrations. |
| ORM | **Prisma** | **Drizzle ORM** | Prisma for dev speed (excellent DX). Drizzle for prod (edge-compatible, 10x faster queries, no Prisma engine overhead). |
| Cache / Queue | **Redis (local Docker)** | **Upstash Redis** | Upstash = serverless Redis, per-request billing. No idle cost. Scales to millions of ops. |
| Search | **PostgreSQL full-text (dev)** | **Typesense (self-hosted) or Algolia** | Typesense: open-source, fast, typo-tolerant. Algolia if budget allows (better managed, higher cost). |
| File Storage | **Local filesystem (dev)** | **Cloudflare R2** | R2 = S3-compatible, zero egress fees. Best cost for serving user-uploaded content and generated assets. |

---

### 12.4 Infrastructure

| Concern | Dev Choice | Prod Choice | Justification |
|---|---|---|---|
| Hosting | **Vercel (free)** | **Vercel Pro + separate VPS (DigitalOcean / Hetzner)** | Vercel for Next.js frontend (unmatched DX + Edge Network). VPS for long-running AI pipeline services (Vercel 10s function limit insufficient). |
| CDN | **Vercel Edge Network** | **Cloudflare (free plan)** | Cloudflare: global CDN, DDoS protection, WAF, bot management. Layer in front of Vercel origin. |
| Email | **Resend (free tier: 3k/mo)** | **Resend (paid) + Amazon SES backup** | Resend: best DX, React Email templates, deliverability focus. SES as cheap backup at high volume. |
| Auth | **NextAuth.js (now Auth.js)** | **Same + Clerk for scale** | Auth.js for full control. Clerk if team wants managed auth (adds cost but saves dev time at scale). |
| Monitoring | **Console logging (dev)** | **Sentry (errors) + PostHog (analytics) + Axiom (logs)** | Sentry: best error tracking. PostHog: open-source product analytics, self-hostable. Axiom: log aggregation at low cost. |
| CI/CD | **GitHub Actions (free)** | **Same** | GitHub Actions sufficient. Deploy preview per PR via Vercel integration. |

---

### 12.5 AI Infrastructure

| Concern | Dev Choice | Prod Choice | Justification |
|---|---|---|---|
| AI SDK | **Vercel AI SDK** | **Same** | Unified interface for OpenAI, Anthropic, Google. Streaming support built-in. Reduces per-provider boilerplate. |
| Prompt Storage | **PostgreSQL** | **Same** | Prompts in DB = admin-editable without redeploy. Versioned, auditable. |
| AI Cost Tracking | **Custom middleware logging** | **Helicone** | Helicone: drop-in proxy for all OpenAI/Anthropic calls. Full cost visibility, rate limiting, caching at AI layer. |
| Vector DB (future RAG) | **pgvector (PostgreSQL extension)** | **Same or Pinecone** | pgvector for embedded search in early stages. Pinecone when vector ops exceed PostgreSQL limits. |

---

## 13. Folder Structure

```
/
├── .env.local
├── .env.production
├── next.config.ts
├── tailwind.config.ts
├── drizzle.config.ts
├── package.json
│
└── src/
    │
    ├── app/                          # Next.js App Router
    │   ├── [locale]/                 # i18n root (en, bn, in, etc.)
    │   │   ├── layout.tsx            # Authenticated/Guest layout switcher
    │   │   ├── page.tsx              # Homepage (landing for guests)
    │   │   │
    │   │   ├── insights/
    │   │   │   ├── page.tsx          # Insights listing
    │   │   │   └── [slug]/
    │   │   │       └── page.tsx      # Single insight (SSR + SEO)
    │   │   │
    │   │   ├── calendar/
    │   │   │   └── page.tsx          # Economic calendar
    │   │   │
    │   │   ├── cot/
    │   │   │   └── page.tsx          # COT report
    │   │   │
    │   │   ├── speech-decoder/
    │   │   │   ├── page.tsx          # Decoder listing / active session
    │   │   │   └── [sessionId]/
    │   │   │       └── page.tsx      # Live decoder session
    │   │   │
    │   │   ├── news/
    │   │   │   └── page.tsx          # AI news feed
    │   │   │
    │   │   ├── dashboard/
    │   │   │   └── page.tsx          # User dashboard (authenticated only)
    │   │   │
    │   │   ├── pricing/
    │   │   │   └── page.tsx          # Plans + payment
    │   │   │
    │   │   ├── referral/
    │   │   │   └── page.tsx          # Referral dashboard
    │   │   │
    │   │   ├── tasks/
    │   │   │   └── page.tsx          # Task-based unlock center
    │   │   │
    │   │   └── settings/
    │   │       └── page.tsx          # User settings
    │   │
    │   ├── admin/                    # Admin Panel (separate auth guard)
    │   │   ├── layout.tsx
    │   │   ├── page.tsx              # Dashboard
    │   │   ├── content/
    │   │   │   ├── insights/
    │   │   │   ├── calendar/
    │   │   │   ├── cot/
    │   │   │   ├── news/
    │   │   │   └── speech-decoder/
    │   │   ├── ai/
    │   │   │   ├── prompts/
    │   │   │   ├── pipelines/
    │   │   │   ├── models/
    │   │   │   └── logs/
    │   │   ├── access/
    │   │   │   ├── features/
    │   │   │   └── content-blocks/
    │   │   ├── users/
    │   │   ├── translations/
    │   │   ├── payments/
    │   │   │   ├── plans/
    │   │   │   ├── gateways/
    │   │   │   └── revenue/
    │   │   ├── growth/
    │   │   │   ├── referrals/
    │   │   │   └── tasks/
    │   │   ├── ads/
    │   │   └── settings/
    │   │
    │   └── api/                      # API Routes
    │       ├── auth/
    │       │   └── [...nextauth]/
    │       ├── webhooks/
    │       │   ├── stripe/
    │       │   ├── razorpay/
    │       │   ├── sslcommerz/
    │       │   └── [provider]/
    │       ├── ai/
    │       │   ├── pipeline/
    │       │   └── speech-decoder/
    │       └── cron/                 # Inngest / scheduled functions
    │           ├── cot-parse/
    │           ├── calendar-refresh/
    │           └── news-ingest/
    │
    ├── components/                   # Shared UI components
    │   ├── ui/                       # shadcn/ui base components
    │   ├── layout/
    │   │   ├── Sidebar.tsx
    │   │   ├── MobileHeader.tsx
    │   │   ├── BottomNav.tsx
    │   │   ├── GuestLayout.tsx
    │   │   └── AuthenticatedLayout.tsx
    │   ├── content/
    │   │   ├── InsightCard.tsx
    │   │   ├── InsightDetail.tsx
    │   │   ├── CalendarRow.tsx
    │   │   ├── COTChart.tsx
    │   │   ├── NewsCard.tsx
    │   │   └── SpeechDecoderFeed.tsx
    │   ├── access/
    │   │   ├── ContentLock.tsx       # Blur/placeholder lock wrapper
    │   │   ├── UpgradeModal.tsx
    │   │   └── AccessGate.tsx        # HOC: gates a component by tier
    │   ├── auth/
    │   │   ├── LoginModal.tsx
    │   │   ├── SignupModal.tsx
    │   │   └── AuthGuard.tsx
    │   └── shared/
    │       ├── LoadingSkeleton.tsx
    │       ├── ErrorBoundary.tsx
    │       ├── SentimentBadge.tsx
    │       └── ImpactScore.tsx
    │
    ├── lib/                          # Core logic (no UI)
    │   ├── ai/
    │   │   ├── pipeline-engine.ts    # Main PEE: resolves, executes, logs pipelines
    │   │   ├── variable-mapper.ts    # Injects variables into prompt templates
    │   │   ├── model-selector.ts     # Selects model based on rules
    │   │   ├── fallback-handler.ts   # Manages fallback chain
    │   │   ├── cost-router.ts        # Cost optimization routing rules
    │   │   └── providers/
    │   │       ├── openai.ts
    │   │       ├── anthropic.ts
    │   │       ├── gemini.ts
    │   │       ├── perplexity.ts
    │   │       └── grok.ts
    │   │
    │   ├── access/
    │   │   ├── tier-resolver.ts      # Resolves user's current tier
    │   │   ├── feature-flags.ts      # Evaluates feature flag per user/request
    │   │   └── content-gate.ts       # Determines visibility of content blocks
    │   │
    │   ├── payments/
    │   │   ├── pal.ts                # Payment Abstraction Layer
    │   │   ├── country-router.ts     # Maps country → payment provider
    │   │   └── providers/
    │   │       ├── stripe.ts
    │   │       ├── razorpay.ts
    │   │       ├── sslcommerz.ts
    │   │       ├── midtrans.ts
    │   │       └── nowpayments.ts
    │   │
    │   ├── growth/
    │   │   ├── referral-engine.ts
    │   │   ├── task-engine.ts
    │   │   └── reward-engine.ts
    │   │
    │   ├── translation/
    │   │   ├── translation-pipeline.ts
    │   │   ├── translation-memory.ts
    │   │   └── i18n-config.ts
    │   │
    │   ├── data/
    │   │   ├── cot-parser.ts         # Parses CFTC COT text files
    │   │   ├── calendar-ingestor.ts  # Fetches + normalizes economic calendar
    │   │   ├── news-ingestor.ts      # Multi-source news ingestion
    │   │   └── price-fetcher.ts      # Market price data (optional enrichment)
    │   │
    │   ├── cache/
    │   │   └── redis.ts              # Redis client + cache helpers
    │   │
    │   └── utils/
    │       ├── date.ts
    │       ├── currency.ts
    │       └── seo.ts
    │
    ├── db/                           # Database layer
    │   ├── schema/
    │   │   ├── users.ts
    │   │   ├── subscriptions.ts
    │   │   ├── insights.ts
    │   │   ├── calendar.ts
    │   │   ├── cot.ts
    │   │   ├── news.ts
    │   │   ├── speech-sessions.ts
    │   │   ├── prompts.ts
    │   │   ├── pipelines.ts
    │   │   ├── pipeline-runs.ts
    │   │   ├── translations.ts
    │   │   ├── translation-memory.ts
    │   │   ├── feature-flags.ts
    │   │   ├── content-blocks.ts
    │   │   ├── referrals.ts
    │   │   ├── tasks.ts
    │   │   ├── task-completions.ts
    │   │   ├── rewards.ts
    │   │   ├── payments.ts
    │   │   └── admin-users.ts
    │   ├── migrations/               # Drizzle migrations
    │   └── index.ts                  # DB client export
    │
    ├── hooks/                        # Custom React hooks
    │   ├── useUserTier.ts
    │   ├── useFeatureFlag.ts
    │   ├── useContentLock.ts
    │   ├── useSpeechDecoder.ts       # SSE hook for live decoder
    │   └── usePayment.ts
    │
    ├── stores/                       # Zustand stores
    │   ├── userStore.ts
    │   ├── uiStore.ts
    │   └── decoderStore.ts
    │
    ├── types/                        # TypeScript type definitions
    │   ├── ai.ts
    │   ├── content.ts
    │   ├── access.ts
    │   ├── payment.ts
    │   └── admin.ts
    │
    ├── middleware.ts                 # Next.js middleware: locale redirect, auth guard, access control
    │
    └── i18n/
        ├── messages/
        │   ├── en.json
        │   ├── bn.json
        │   ├── in.json
        │   └── ...
        └── routing.ts
```

---

### 13.1 Build Order (Development Phases)

**Phase 1 — Foundation**
- DB schema + migrations
- Auth system (user + admin)
- Layout components (guest, authenticated)
- Feature flag engine
- Content lock engine (static rules)

**Phase 2 — Core Features**
- Daily Insight (static + AI pipeline)
- Economic Calendar (data ingest + AI enrichment)
- COT Report (parser + display)
- Access tier enforcement

**Phase 3 — AI Infrastructure**
- Pipeline Execution Engine
- Prompt library + admin UI
- Multi-model routing + fallback
- Translation pipeline

**Phase 4 — Growth + Payments**
- Payment Abstraction Layer (Stripe first)
- Subscription management
- Referral system
- Task-based unlock

**Phase 5 — Live Features**
- Speech Decoder (SSE + live session)
- AI News Intelligence

**Phase 6 — Scale + Optimization**
- Add remaining payment providers
- Full multi-language rollout
- Cost optimization rules
- Monitoring + alerting

---

## 14. Scalability Strategy

### 14.1 Horizontal Scaling Plan

```
Current (0–50k users):
  - Vercel (frontend + API) + Neon PostgreSQL + Upstash Redis
  - Single app, monolithic Next.js
  - BullMQ for background jobs on single Node instance

50k–500k users:
  - Separate AI Pipeline Service (Node/Fastify on DigitalOcean)
  - Separate Worker Service (BullMQ workers, horizontally scaled)
  - Read replicas on PostgreSQL
  - Redis cluster for cache
  - Cloudflare in front of all traffic

500k–10M users:
  - Microservice separation: Auth, Content, AI, Payments, Translation
  - PostgreSQL sharding or migration to CockroachDB (globally distributed)
  - Dedicated search cluster (Typesense cluster)
  - Regional deployment (EU, APAC, Americas) via Cloudflare Workers
  - Kafka for event streaming (replace BullMQ at this scale)
```

---

### 14.2 Database Scaling

- **Read replicas** for all content reads (99% of traffic)
- **Connection pooling** via PgBouncer (Neon managed)
- **Partitioning** on high-volume tables (`pipeline_runs`, `news_items`) by date
- **JSONB with indexes** for flexible AI output storage (avoid schema migrations for output format changes)
- **Archival** of data older than 2 years to cold storage (R2)

---

### 14.3 AI Pipeline Scaling

- Each pipeline run is a queue job — horizontally scalable by adding workers
- Pipeline context stored in Redis (not in-memory) — workers are stateless
- AI provider rate limits handled per-provider with token bucket algorithm
- Async translation jobs never block content publish (fire-and-forget with completion webhook)

---

## 15. Cost Optimization Strategy

### 15.1 AI Cost Controls

| Strategy | Expected Saving |
|---|---|
| Route translations to Gemini Flash (vs GPT-4o) | ~70% reduction on translation costs |
| Route beginner explanations to GPT-4o-mini | ~75% reduction on explanation costs |
| Translation memory (reuse identical segments) | ~40–60% on repeated content |
| Prompt compression (remove redundant instruction tokens) | ~10–15% per call |
| Cache AI outputs per content item (don't regenerate on every view) | ~95% reduction at content-render time |
| Daily spend cap with graceful degradation | Hard budget protection |
| Helicone prompt caching (semantic cache) | ~20–30% on similar prompts |

**Estimated AI cost at 100k MAU:** $200–400/month with full optimization.

---

### 15.2 Infrastructure Cost Controls

| Strategy | Expected Saving |
|---|---|
| Vercel (no EC2 management overhead) | ~$0 DevOps at start |
| Neon serverless PostgreSQL | ~$0 idle cost (scale to zero) |
| Upstash Redis (per-request billing) | ~$0 idle cost |
| Cloudflare R2 (zero egress fees) | vs S3: 60–80% storage cost reduction |
| SSE over WebSocket (less infra overhead) | No WebSocket server needed for decoder |
| CDN-cached content pages (reduce origin hits) | ~90% reduction in origin compute for content |

---

### 15.3 Target Cost Model

| Scale | Monthly Infra + AI Cost | Revenue Target |
|---|---|---|
| 0–1k MAU | $0–20 | Validation phase |
| 1k–10k MAU | $20–100 | $500–2000 |
| 10k–100k MAU | $100–500 | $5k–20k |
| 100k–1M MAU | $500–3000 | $50k–200k |
| 1M–10M MAU | $3000–15000 | $500k–2M |

---

## Appendix: Key Decisions Summary

| Decision | Choice | Reason |
|---|---|---|
| Frontend | Next.js 14 App Router | SSR/ISR/SSG mix needed. SEO-critical. |
| ORM | Prisma (dev) → Drizzle (prod) | Dev speed → Runtime performance |
| Queue | BullMQ | Best Node.js queue. Redis-backed. Reliable. |
| Cache | Upstash Redis | Serverless, no idle cost, global edge |
| Storage | Cloudflare R2 | Zero egress fees. S3-compatible. |
| Auth | Auth.js | Open source, flexible, self-hosted |
| AI SDK | Vercel AI SDK | Unified multi-provider. Streaming built-in. |
| AI Cost Layer | Helicone | Caching + observability without SDK changes |
| Payments | Stripe-first + PAL | Stripe coverage + abstraction for local gateways |
| Real-time | SSE | One-directional stream sufficient for decoder |
| Search | Typesense | Open-source, fast, self-hostable |

---

*This document is a living architecture blueprint. Update version number and changelog when architectural decisions change.*
