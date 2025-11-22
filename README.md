# Kaptio Content Hub Ecosystem

**Status:** POC Phase  
**Ragnar:** Building simple gallery site (this week)  
**Halldor:** Exploring long-term options & integration plan  
**Decision:** CloudCannon vs Custom after POC proven

---

## 🚀 POC: Simple Gallery Site

**Launch:** This week  
**Purpose:** Support sales team immediately with beautiful, trackable pre-sales content

### What We're Building

A simple, static HTML gallery site at `marketing.kaptio.com`:
- Gallery/index page listing all pre-sales content
- Individual pages for each piece (showcases, one-pagers, case studies)
- Kaptio Design System styling
- Manual link tracking initially
- Git-based (can add content quickly)

### Why This Approach

1. **Immediate Value:** Sales team empowered TODAY, not in 6-12 weeks
2. **No Dependencies:** While Halldor explores CloudCannon, team has working solution
3. **Proves Concept:** Tests if magazine-style content works for sales workflow
4. **Easy Migration:** Static content easily moves to CloudCannon or custom system later

### How We Add Content (POC)

1. Create HTML file (or markdown → HTML)
2. Kai assists with writing (via Cursor, internal only)
3. Manual review/approval (email/Slack)
4. Git commit + push
5. Auto-deploy to Netlify (< 5 minutes)

**Timeline:** 1-2 days to build, live by end of week.

---

## 📋 Overview

Unified git-native content infrastructure serving 4 specialized hubs:

1. **Marketing Hub** - Product showcases and pre-sales collateral
2. **User Guides Hub** - End-user and admin documentation
3. **Architecture Hub** - Technical documentation and extension guides
4. **Maturity Model Hub** - Thought leadership and capability growth

---

## ⚠️ Important: Kai AI Reality Check

**Current Status:** Kai is an extremely powerful AI assistant with full access to Kaptio systems and customer data.

**Security & Privacy Concerns:**
- ❌ **No guardrails** - Kai has unrestricted access to all data
- ❌ **Privacy risk** - Could expose sensitive customer information
- ❌ **Security risk** - Too powerful to expose to customers/prospects
- ❌ **Not customer-facing ready** - Cannot be embedded in hubs until we implement proper data isolation and protection

**How We Use Kai (For Now):**
- ✅ **Internal content generation only** - Team members use Kai via Cursor to create first drafts
- ✅ **No customer interaction** - Kai never directly interacts with prospects or customers
- ✅ **Content creation assistant** - Not a chat widget, not embedded in hubs

**Future State:**
- Once we build proper security controls, data isolation, and customer data protection mechanisms, THEN we can consider embedding Kai in hubs
- This is a separate, significant engineering effort not part of this content hub project

---

## 🎯 Implementation Options Analysis

We evaluated multiple git-native CMS solutions. Here's how they compare against our requirements:

### Evaluated Solutions

| Feature | CloudCannon | Decap CMS | Tina CMS | Keystatic | **Custom** |
|---------|-------------|-----------|----------|-----------|------------|
| Git-Native | ✅ | ✅ | ✅ | ✅ | ✅ |
| Built-in Approval | ✅ Publishing | ⚠️ Basic | ❌ | ❌ | ✅ Custom Rules |
| Approval Matrix (2+ approvers) | ⚠️ Team Plans | ❌ | ❌ | ❌ | ✅ |
| Different Rules per Content Type | ⚠️ Limited | ❌ | ❌ | ❌ | ✅ |
| Link Tracking & Analytics | ❌ | ❌ | ❌ | ❌ | ✅ |
| Kai AI Integration | ❌ | ❌ | ❌ | ❌ | ✅ |
| Visual Editor UX | ✅ Excellent | ⚠️ Basic | ✅ Excellent | ✅ Good | ✅ Tailored |
| Cost | $45/mo+ | Free | $29/mo+ | Free | Dev Time Only |
| Maturity | ✅ Very Stable | ✅ Stable | ✅ Mature | ⚠️ New | ✅ We Control |

### CloudCannon: The Closest Match

**CloudCannon** is the most mature and feature-rich option we evaluated. It's a commercial, enterprise-grade git-based CMS that's been around since 2013.

**What CloudCannon Does Well:**
- ✅ Excellent visual editor (best-in-class UX)
- ✅ Built-in publishing workflows (staging → production)
- ✅ Team collaboration with roles & permissions
- ✅ Supports many SSGs (Jekyll, Hugo, Eleventy, etc.)
- ✅ Includes hosting (all-in-one solution)
- ✅ Very stable, mature product

**Why It's Still Not Enough:**
- ❌ **Approval rules:** Limited to basic team workflows, can't customize per content type
- ❌ **No link tracking:** Can't generate tracked URLs per prospect
- ❌ **No AI integration:** No way to embed Kai natively
- ❌ **Cost:** $45-99/mo per site × 4 hubs = $180-396/mo recurring
- ❌ **Vendor lock-in:** Tied to their hosting & platform
- ❌ **Feature requests:** At mercy of their roadmap

**Verdict:** CloudCannon could work for Hubs 2-4 (documentation) if we compromised on approval workflows. But Hub 1 (Marketing) absolutely needs prospect tracking and custom approval matrices. Rather than split our stack (CloudCannon for docs + custom for marketing), building one unified system gives us consistency and full control.

### Deal Breakers (All Solutions)

- ❌ **No custom approval matrices** - Need different rules per hub/content type
- ❌ **No audit trail we control** - Need complete approval tracking
- ❌ **Limited to vendor roadmap** - Can't add features as needed
- ❌ **Can't integrate with Kai** - Need native AI assistant integration
- ❌ **No prospect link tracking** - Critical for Hub 1 (Marketing)

### Two Finalists

After initial analysis, **Decap**, **Tina**, and **Keystatic** are eliminated due to lack of approval workflows. 

The decision is between:

#### **Option A: CloudCannon** (Mature Commercial Platform)
- ✅ Best-in-class editor UX
- ✅ Immediate availability
- ✅ All-in-one (CMS + hosting)
- ⚠️ Requires workarounds for custom approvals and link tracking
- ⚠️ Vendor dependency for knowledge and features
- 💰 ~$100/month (~$6K over 5 years)

#### **Option B: Custom Build** (Purpose-Built Solution)
- ✅ Full control and knowledge ownership
- ✅ Integrated approval/tracking/Kai from day 1
- ✅ Simple, maintainable codebase
- ⚠️ 12 weeks to build
- ⚠️ We maintain it
- 💰 ~$20/month (~$1.2K over 5 years)

### Decision Criteria

The key factor is **sustainable, maintainable knowledge**:
- CloudCannon = Learn their platform, rely on vendor
- Custom = Own our architecture, full understanding

Cost is secondary. The real question: Do we value speed (2 weeks) or long-term knowledge ownership (12 weeks)?

---

## 🏗️ Architecture

```
kaptio-hub/
├── packages/
│   ├── cms-ui/              # Custom content editor
│   │   ├── components/
│   │   │   ├── Editor.tsx         # MDX editor
│   │   │   ├── MediaUpload.tsx    # Cloudinary upload
│   │   │   ├── Preview.tsx        # Live preview
│   │   │   └── MetadataForm.tsx   # Frontmatter editor
│   │   └── pages/
│   │       ├── dashboard.tsx
│   │       ├── edit/[id].tsx
│   │       └── new.tsx
│   │
│   ├── admin-portal/        # Approval & management
│   │   ├── pages/
│   │   │   ├── dashboard.tsx
│   │   │   ├── review-queue.tsx   # Approval UI
│   │   │   ├── links.tsx          # Link generator
│   │   │   └── analytics.tsx      # Engagement metrics
│   │   └── lib/
│   │       ├── approval-engine.ts
│   │       └── db.ts              # Supabase client
│   │
│   ├── design-system/       # Shared Kaptio components
│   └── shared-services/     # Link tracking, analytics
│
├── content/                 # Actual content (Git)
│   ├── marketing/
│   ├── user-guides/
│   ├── architecture/
│   └── maturity-model/
│
└── hubs/                    # Static site generators
    ├── marketing-hub/       # Vite + React
    ├── user-guides-hub/     # Vite + React
    ├── architecture-hub/    # Vite + React
    └── maturity-model-hub/  # Vite + React
```

---

## 🛠️ Tech Stack

### Frontend
- **Framework:** React 18 + TypeScript
- **Styling:** Tailwind CSS (Kaptio Design System)
- **Editor:** MDXEditor (markdown with React components)
- **Routing:** React Router

### Backend
- **Database:** Supabase (PostgreSQL + Auth)
- **Git Operations:** GitHub API (Octokit)
- **Serverless:** Netlify Functions
- **Media:** Cloudinary

### Infrastructure
- **Version Control:** Git (source of truth)
- **CI/CD:** GitHub Actions
- **Hosting:** Netlify
- **Monorepo:** Turborepo

### Integrations
- **Analytics:** Plausible (privacy-first)
- **Search:** Pagefind (static site search)
- **AI:** Kai Assistant (Claude API)
- **Link Tracking:** Custom (Supabase + short URL service)

---

## 📊 Database Schema

```sql
-- content_items: Track all content
CREATE TABLE content_items (
  id UUID PRIMARY KEY,
  hub TEXT NOT NULL,
  type TEXT NOT NULL,
  path TEXT NOT NULL UNIQUE,
  title TEXT NOT NULL,
  status TEXT NOT NULL DEFAULT 'draft',
  git_branch TEXT,
  pr_number INTEGER,
  author_id UUID REFERENCES auth.users(id),
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- submissions: Track review workflow
CREATE TABLE submissions (
  id UUID PRIMARY KEY,
  content_item_id UUID REFERENCES content_items(id),
  pr_number INTEGER NOT NULL,
  preview_url TEXT,
  status TEXT NOT NULL DEFAULT 'pending',
  submitted_by UUID REFERENCES auth.users(id),
  required_approvals INTEGER NOT NULL DEFAULT 1
);

-- approvals: Track who approved what
CREATE TABLE approvals (
  id UUID PRIMARY KEY,
  submission_id UUID REFERENCES submissions(id),
  approver_id UUID REFERENCES auth.users(id),
  approved BOOLEAN NOT NULL,
  comment TEXT,
  approved_at TIMESTAMPTZ DEFAULT NOW()
);

-- approval_rules: Define who can approve what
CREATE TABLE approval_rules (
  id UUID PRIMARY KEY,
  hub TEXT NOT NULL,
  content_type TEXT NOT NULL,
  required_approvals INTEGER NOT NULL DEFAULT 1,
  approver_roles TEXT[] NOT NULL
);

-- tracked_links: Link tracking for prospects
CREATE TABLE tracked_links (
  id UUID PRIMARY KEY,
  short_code TEXT NOT NULL UNIQUE,
  target_url TEXT NOT NULL,
  content_item_id UUID REFERENCES content_items(id),
  prospect_name TEXT,
  campaign TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  expires_at TIMESTAMPTZ
);

-- link_visits: Track engagement
CREATE TABLE link_visits (
  id UUID PRIMARY KEY,
  link_id UUID REFERENCES tracked_links(id),
  visited_at TIMESTAMPTZ DEFAULT NOW(),
  ip_address TEXT,
  user_agent TEXT,
  referrer TEXT
);
```

---

## 🚀 Implementation Roadmap

### Phase 1: CMS Foundation (Weeks 1-3)
- Set up monorepo with Turborepo
- Create Kaptio Design System package
- Build content editor with MDX support
- Implement GitHub API integration
- Set up Supabase project + schema
- Basic save draft functionality

**Deliverable:** Non-technical users can write content, save drafts

### Phase 2: Approval Workflow (Weeks 4-6)
- Submit for review (PR creation)
- Admin portal: Review queue
- Custom approval rules engine
- Approval matrix with multiple reviewers
- Email notifications
- Auto-merge on approval

**Deliverable:** Full review/approval workflow working

### Phase 3: Hub Infrastructure (Weeks 7-9)
- Build Hub 1 (Marketing) static site
- Build Hub 2 (User Guides) static site
- Set up Netlify deployment pipelines
- Configure preview deployments
- Media upload integration (Cloudinary)
- Live preview in editor

**Deliverable:** Two hubs live with content from CMS

### Phase 4: Shared Services & Launch (Weeks 10-12)
- Link generator with tracking
- Analytics integration (Plausible)
- Kai AI assistant integration
- Build Hubs 3 & 4
- Polish UI/UX across all systems
- User training & documentation

**Deliverable:** Full system operational, all 4 hubs live

---

## 🎨 User Workflows

### Content Author Workflow

1. **Login** → CMS dashboard
2. **New Content** → Select hub + content type
3. **Write** → MDX editor with live preview
4. **Add Media** → Drag-drop to Cloudinary
5. **Save Draft** → Auto-commit to Git branch
6. **Submit for Review** → Creates PR, notifies reviewers
7. **Track Status** → See approval progress in dashboard

### Reviewer Workflow

1. **Login** → Admin portal
2. **Review Queue** → See pending submissions
3. **Preview** → Click to see staged content
4. **Review** → Check content in browser + PR diff
5. **Approve/Reject** → One-click approval
6. **Auto-Publish** → System merges PR when enough approvals

### Sales/Marketing Workflow

1. **Login** → Admin portal
2. **Link Generator** → Select content + prospect
3. **Generate** → Get tracked short URL
4. **Share** → Send to prospect
5. **Track** → Monitor engagement in real-time
6. **Analyze** → See which content resonates

---

## 📝 Content Format

All content stored as **MDX** (Markdown + JSX):

```mdx
---
title: "Kaptio Connect Showcase"
hub: "marketing"
type: "showcase"
date: 2025-01-20
author: "John Doe"
tags: ["integration", "showcase", "api"]
---

# Kaptio Connect

Powerful integration platform for travel technology.

## Key Features

<FeatureGrid>
  <Feature title="Real-time Sync" icon="sync">
    Bi-directional data flow between systems
  </Feature>
  <Feature title="Secure" icon="lock">
    Enterprise-grade security and compliance
  </Feature>
</FeatureGrid>

## Architecture

<DiagramComponent src="/diagrams/connect-architecture.svg" />

[Learn more about extending Kaptio →](/architecture/extension-guide)
```

**Benefits:**
- ✅ Human-readable (Git diffs make sense)
- ✅ AI-friendly (LLMs understand markdown)
- ✅ Portable (can export to any system)
- ✅ Powerful (React components in content)

---

## 🔗 Cross-Hub Linking

Maturity Model Hub links to relevant content:

```mdx
## Level 3: Standardized Operations

You've documented your processes. Now let's optimize them.

**Recommended Resources:**
- [Booking Wizard Configuration Guide](/user-guides/booking-wizard) (Hub 2)
- [Custom Field Architecture](/architecture/custom-fields) (Hub 3)
- [Success Story: Railbookers](/marketing/case-studies/railbookers) (Hub 1)
```

---

## 📈 Success Metrics

- **Content Production Speed:** 10x faster (AI-assisted writing)
- **Time to Deploy:** < 5 minutes (Git push → live)
- **Cross-Hub Reusability:** 100% (shared components)
- **Prospect Engagement:** Per-link tracking
- **Content Quality:** Review workflow ensures accuracy

---

## 🔐 Security & Permissions

### User Roles

- **Author:** Can create/edit content, submit for review
- **Reviewer:** Can approve content in their hub
- **Admin:** Can approve any content, manage users, generate links
- **Viewer:** Read-only access to content

### Approval Rules Example

```yaml
marketing-showcase:
  required_approvals: 2
  approvers:
    - product-team
    - marketing-team
  
user-guide:
  required_approvals: 1
  approvers:
    - docs-team
    
architecture-doc:
  required_approvals: 2
  approvers:
    - engineering-team
    - solutions-team
```

---

## 🎯 Key Decisions

1. **Custom CMS over Tina/Decap** - Full control, exact requirements
2. **Supabase over Firebase** - Better PostgreSQL, simpler auth
3. **Turborepo over pnpm workspaces** - Better caching, faster builds
4. **Cloudinary over Git LFS** - Better performance, transformations
5. **Plausible over Google Analytics** - Privacy-first, simple
6. **MDX over plain Markdown** - React components in content

---

## 📚 Reference

- **Pitch Document:** [PITCH.html](./PITCH.html)
- **Live Examples:**
  - [Kaptio Connect Showcase](https://kaptio-connect-showcase.netlify.app/)
  - [Transfer Architecture Guide](https://kaptio-transfer-architecture.netlify.app/)
  - [Booking Wizard Guide](https://kaptio-booking-wizard-guide.netlify.app/)
- **Design System:** `/quanta-docs-duvine/KAPTIO_DESIGN_SYSTEM.md`

---

## 🚀 Next Steps

### Immediate (This Week)
1. ✅ Define vision and requirements (DONE)
2. ✅ Evaluate CMS options (DONE)
3. ✅ Identify POC strategy (DONE - simple gallery)
4. 🔄 **Build POC gallery site**
5. 🔄 **Deploy POC to marketing.kaptio.com**

### Parallel Track (Next 2-4 Weeks)
- Halldor: Explore CloudCannon setup & templates
- Team: Use POC gallery, add content as needed
- Decision point: CloudCannon vs Custom after POC proven

### Post-POC (Week 5+)
**If CloudCannon:**
- Migrate POC content to CloudCannon
- Set up approval/tracking services
- 6 weeks to full workflow

**If Custom Build:**
- Start building custom CMS
- 12 weeks to full system

---

**Last Updated:** 2025-01-22  
**Status:** POC gallery to be built this week, long-term decision pending


