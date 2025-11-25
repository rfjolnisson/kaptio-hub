# CloudCannon CMS - Detailed Analysis

**Evaluated:** 2025-01-20  
**Version:** Current (2024/2025)  
**Website:** https://cloudcannon.com  
**Verdict:** ❌ Does not meet core requirements

---

## 📋 Overview

CloudCannon is a mature, commercial git-based CMS that's been in the market since 2013. It's one of the most polished and feature-rich options in the git-native CMS space.

**Target Audience:**
- Agencies managing multiple client sites
- Enterprise teams needing collaboration features
- Teams wanting an all-in-one solution (CMS + hosting)

**Positioning:**
- Enterprise-grade git-based CMS
- "Visual editing for static sites"
- All-in-one: CMS + hosting + build pipeline

---

## ✅ What CloudCannon Does Well

### 1. **Excellent Visual Editor**
- **Best-in-class UX** among git-native CMS options
- True WYSIWYG editing (edit directly on the page)
- Multiple editing interfaces:
  - Visual Editor (inline editing)
  - Content Editor (structured forms)
  - Source Editor (raw markdown/code)
- Live preview as you type
- Component-based editing (for React, Vue, etc.)

### 2. **Publishing Workflows**
- Built-in staging and production branches
- Branch-based publishing (draft → staging → production)
- Review process before publishing
- Team collaboration features
- Role-based permissions (Editor, Developer, Admin)

### 3. **Static Site Generator Support**
- Supports many SSGs:
  - Jekyll (native support)
  - Hugo
  - Eleventy
  - Next.js
  - Gatsby
  - SvelteKit
  - And more
- Automatic builds on Git push
- Build hooks and webhooks

### 4. **Hosting Included**
- Built-in global CDN
- Automatic SSL certificates
- Custom domains
- Forms (with submissions)
- Redirects and rewrites
- Password protection

### 5. **Git Integration**
- GitHub, GitLab, Bitbucket support
- Two-way sync (CMS ↔ Git)
- Merge conflict handling
- Full Git history preserved

### 6. **Team Features**
- User roles and permissions
- Activity logs
- Comments on content
- Scheduled publishing
- Draft/review workflows

### 7. **Developer Experience**
- Local development sync
- Configuration via YAML files
- Custom build commands
- Environment variables
- Staging environments

---

## ❌ Why It Doesn't Meet Our Requirements

### 1. **Approval Workflows - Limited**

**What CloudCannon Offers:**
- Basic publishing workflow (draft → review → publish)
- Requires "Team" plan ($99/mo+) for review features
- Single approval step (not multi-stage)

**What We Need:**
```yaml
# Our requirement: Custom approval matrix per content type
marketing-showcase:
  required_approvals: 2
  approvers: [product-team, marketing-team]
  
user-guide:
  required_approvals: 1
  approvers: [docs-team]

architecture-doc:
  required_approvals: 2
  approvers: [engineering-team, solutions-team]
```

**Gap:** CloudCannon's workflow is site-wide, not per content-type. Can't configure "2 approvals for showcases, 1 for user guides."

---

### 2. **No Link Tracking**

**What We Need:**
- Generate unique tracked URLs per prospect
- Track: page views, time on page, content downloaded
- Link expiry dates
- Campaign tagging
- Integration with CRM

**What CloudCannon Offers:**
- ❌ None of this
- Basic forms (but no link tracking)
- No analytics beyond standard web analytics

**Workaround:** Would need to build entirely separate system for link tracking, defeating the purpose of integrated platform.

---

### 3. **No AI Integration**

**What We Need:**
- Kai assistant embedded in all hubs
- Context-aware help
- Content generation assistance
- Search with natural language

**What CloudCannon Offers:**
- ❌ No AI features
- ❌ No API for embedding custom assistants
- ❌ No chatbot/assistant framework

**Gap:** CloudCannon is a traditional CMS with no AI/LLM integration path.

---

### 4. **Cost Structure**

**CloudCannon Pricing (2024):**

| Plan | Price/Month | Features | Suitable For |
|------|-------------|----------|--------------|
| **Lite** | $45 | 1 site, basic features | Small sites |
| **Team** | $99 | 3 sites, workflows, roles | Small teams |
| **Enterprise** | Custom | Unlimited sites, SSO | Large orgs |

**Our Scenario:**
- 4 hubs = 4 separate sites
- Need team features (workflows, roles)
- **Cost:** $99/mo (if 3 sites included) + $45/mo for 4th site = **~$144/mo**
- OR: $45 × 4 = **$180/mo** on Lite plan (no workflow features)
- OR: Negotiate enterprise pricing (likely $300-500/mo)

**Annual Cost:** $1,728 - $6,000/year

**Custom CMS Cost:**
- Development time: 12 weeks (~$0 if we build ourselves)
- Infrastructure: ~$20/mo (Netlify + Supabase + Cloudinary free tiers)
- **Annual Cost:** ~$240/year

**ROI:** Custom CMS pays for itself in 2-3 months.

---

### 5. **Vendor Lock-in**

**CloudCannon Lock-in:**
- Hosting tied to their platform
- Configuration files (CloudCannon-specific YAML)
- Editor configuration (CloudCannon schemas)
- Build pipeline on their infrastructure

**Migration Path:**
- Content in Git (portable ✅)
- But: CloudCannon config files need rewriting
- But: Workflows and permissions need rebuilding
- But: Hosting needs new setup

**Risk:** If CloudCannon changes pricing, gets acquired, or shuts down, we're stuck migrating.

---

### 6. **Feature Requests**

**Need New Features?**
- Submit to CloudCannon roadmap
- Wait for them to prioritize
- No ETA guarantees
- May never get built

**Example:**
- "We need per-content-type approval rules"
- CloudCannon response: "Thanks for the feedback, we'll consider it"
- Reality: 12-24 months if ever

**With Custom:**
- Need a feature? Build it next sprint.
- Full control over roadmap.

---

## 🤔 Could We Use CloudCannon for Some Hubs?

### Hybrid Approach Analysis

**Scenario:** Use CloudCannon for Hubs 2-4 (documentation), custom for Hub 1 (marketing)

**Pros:**
- CloudCannon's visual editor is great for docs
- Built-in hosting simplifies deployment
- Team can start creating content immediately

**Cons:**
- **Split stack complexity:** Two systems to maintain
- **Inconsistent UX:** Different editing experience per hub
- **Duplicate work:** Build approval system twice (CloudCannon + custom)
- **Cost:** Still $99/mo for CloudCannon + dev time for custom Hub 1
- **Training:** Team needs to learn two different systems

**Verdict:** ❌ Not worth it. Unified custom system is simpler, cheaper, and more maintainable.

---

## 📊 CloudCannon vs Custom CMS

| Criterion | CloudCannon | Custom CMS | Winner |
|-----------|-------------|------------|--------|
| **Visual Editor** | ✅ Excellent | ✅ Good (MDX editor) | CloudCannon |
| **Approval Workflows** | ⚠️ Basic | ✅ Custom per content type | Custom |
| **Link Tracking** | ❌ None | ✅ Built-in | Custom |
| **AI Integration** | ❌ None | ✅ Kai native | Custom |
| **Cost (Annual)** | $1,728-6,000 | ~$240 | Custom |
| **Flexibility** | ⚠️ Limited to roadmap | ✅ Full control | Custom |
| **Vendor Lock-in** | ⚠️ Some | ✅ None | Custom |
| **Time to Launch** | ✅ Immediate | ⚠️ 12 weeks | CloudCannon |
| **Maturity** | ✅ Very stable | ⚠️ We build it | CloudCannon |
| **SSG Support** | ✅ Many | ✅ Any | Tie |

**Score:** Custom CMS wins 7-3

---

## 🎯 Final Verdict

### Why Not CloudCannon?

1. **Deal Breakers:**
   - ❌ No custom approval matrices per content type
   - ❌ No prospect link tracking (critical for Hub 1)
   - ❌ No AI integration path

2. **Nice-to-Haves We'd Lose:**
   - Excellent visual editor (can build decent alternative)
   - Immediate availability (12 weeks not a blocker)

3. **Costs:**
   - $1,728-6,000/year vs $240/year
   - ROI on custom: 2-3 months

4. **Strategic:**
   - Vendor lock-in risk
   - Limited to their roadmap
   - Can't iterate quickly

### Why Custom Wins

1. **Core Requirements Met:**
   - ✅ Custom approval matrices
   - ✅ Link tracking integrated
   - ✅ Kai AI native

2. **Cost:**
   - 90% cheaper annually

3. **Control:**
   - Own our destiny
   - Add features anytime
   - No vendor dependency

4. **AI-Friendly:**
   - Clean patterns for Cursor
   - Can iterate with AI assistance
   - Future-proof for AI features

---

## 🔗 References

- **CloudCannon Website:** https://cloudcannon.com
- **CloudCannon Docs:** https://cloudcannon.com/documentation/
- **CloudCannon Pricing:** https://cloudcannon.com/pricing/
- **CloudCannon Blog:** https://cloudcannon.com/blog/

---

## 📝 Notes for Discussion

**If Asked "Why Not CloudCannon?":**

> "CloudCannon is actually the best commercial option we evaluated—excellent visual editor, mature platform, good workflows. But it has three critical gaps:
> 
> 1. **Approval workflows are site-wide, not per-content-type.** We need marketing showcases to require 2 approvals (product + marketing), but user guides only need 1 (docs team). CloudCannon can't do this.
> 
> 2. **No link tracking.** We need to generate tracked URLs for prospects and monitor engagement. CloudCannon has no concept of this—we'd have to build it separately anyway.
> 
> 3. **No AI integration.** We want Kai embedded natively. CloudCannon has no AI features or API for this.
> 
> Given we'd need to build custom systems for tracking and approval rules anyway, and we'd pay $1,700+/year, building our own unified system for ~$240/year makes more sense. Plus, we own it and can iterate quickly."

---

**Last Updated:** 2025-01-20  
**Next Review:** If CloudCannon announces custom workflows or AI features







