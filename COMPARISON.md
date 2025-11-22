# CloudCannon vs Custom Build - Head-to-Head Comparison

**Decision Point:** Which approach for Kaptio Content Hub Ecosystem?  
**Date:** January 2025  
**Status:** Evaluating two finalists

---

## 🎯 Core Requirements (Must-Haves)

1. ✅ **Git-native** - Full version control, portable content
2. ✅ **Custom approval workflows** - Different rules per hub/content type  
3. ✅ **Non-technical editor** - Visual/WYSIWYG experience for content authors
4. ✅ **Link tracking** - Generate tracked URLs per prospect with engagement analytics
5. ✅ **Kai AI integration** - Embedded assistant in all hubs
6. ✅ **Sustainable knowledge** - System we understand and can maintain long-term

---

## 📊 Option A: CloudCannon

### Overview
- Mature commercial git-based CMS (since 2013)
- All-in-one platform (CMS + hosting + CDN)
- Enterprise-grade, very stable
- **Cost:** ~$100/month (Team plan for 4 sites)

### What's Native (Built-in)
✅ Excellent visual editor (best in class)  
✅ Git integration (GitHub, GitLab, Bitbucket)  
✅ Publishing workflows (draft → staging → production)  
✅ Team roles & permissions  
✅ Hosting + CDN included  
✅ Multiple SSG support  
✅ Media management  

### What Requires Workarounds
⚠️ **Custom approval matrix** - CloudCannon has basic approvals, but not per-content-type rules

**How we'd make it work:**
```
CloudCannon Workflow → Webhook on publish event → 
  Check our Supabase DB for approval rules → 
  Block if not enough approvals → 
  Admin portal shows approval UI
```

⚠️ **Link tracking** - No built-in prospect tracking

**How we'd make it work:**
```
Build separate link service:
  - Generate short URL (go.kaptio.com/abc123)
  - Store in Supabase with prospect metadata
  - Redirect to CloudCannon-hosted content
  - Track visits in our database
```

⚠️ **Kai integration** - No AI features

**How we'd make it work:**
```
Use CloudCannon's component system:
  - Add Kai widget via script injection
  - Kai runs as separate service
  - Loads on every page via custom component
```

### Architecture with CloudCannon

```
┌─────────────────────────────────────────┐
│     CloudCannon (Editor + Hosting)      │
│  • Visual editing                       │
│  • Git sync                             │
│  • Basic approvals                      │
│  • Hosting                              │
└─────────────────────────────────────────┘
                    ↓ webhooks
┌─────────────────────────────────────────┐
│    Our Custom Services (Supabase)       │
│  • Approval rules engine                │
│  • Link tracking database               │
│  • Kai AI service                       │
│  • Admin portal (approval UI)           │
└─────────────────────────────────────────┘
```

**Result:** Two systems to maintain, but CloudCannon handles the editing UX.

### Timeline
- **Week 1-2:** Set up CloudCannon, configure 4 sites
- **Week 3-6:** Build workaround services (approval tracker, link service, admin portal)
- **Week 7+:** Content creation begins

**Total: 6 weeks to fully functional** (2 weeks for basic, 6 weeks for all features)

---

## 📊 Option B: Custom Build

### Overview
- Purpose-built for Kaptio's exact needs
- Full control over features and UX
- Simple React + Supabase + GitHub API stack
- **Cost:** ~$20/month (infrastructure only)

### What's Native (Built-in)
✅ Custom approval rules engine (per content type)  
✅ Link tracking integrated  
✅ Kai AI natively embedded  
✅ Git operations via GitHub API  
✅ Unified admin portal (approvals + links + analytics)  
✅ Clean, simple architecture  
✅ Full knowledge ownership  

### What Requires Build Time
⚠️ **12 weeks to MVP** - Every feature must be built

**What we build:**
```
Weeks 1-3: Content editor (MDX + preview)
Weeks 4-6: Approval workflow + admin portal
Weeks 7-9: Hub static sites + deployment
Weeks 10-12: Link service + Kai + polish
```

### Architecture with Custom

```
┌─────────────────────────────────────────┐
│    Kaptio Content System (Custom)       │
│  • CMS Editor (React + MDX)             │
│  • Approval engine (Supabase)           │
│  • Link tracker (Supabase)              │
│  • Kai AI (embedded)                    │
│  • Admin portal (all-in-one)            │
│  • Git operations (GitHub API)          │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│         GitHub (Source of Truth)        │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│       Netlify (Static Site Hosting)     │
│  • Hub 1: marketing.kaptio.com          │
│  • Hub 2: docs.kaptio.com               │
│  • Hub 3: architecture.kaptio.com       │
│  • Hub 4: maturity.kaptio.com           │
└─────────────────────────────────────────┘
```

**Result:** Single integrated system, we understand every part.

### Timeline
- **Week 1-3:** CMS foundation (editor, GitHub integration)
- **Week 4-6:** Approval workflows
- **Week 7-9:** Hub infrastructure
- **Week 10-12:** Shared services (links, Kai, analytics)

**Total: 12 weeks to fully functional**

---

## ⚖️ Head-to-Head Comparison

| Factor | CloudCannon | Custom Build | Winner |
|--------|-------------|--------------|--------|
| **Editor UX** | ⭐⭐⭐⭐⭐ Best-in-class | ⭐⭐⭐⭐ Good | CloudCannon |
| **Time to Launch** | 2-6 weeks | 12 weeks | CloudCannon |
| **Approval Workflows** | ⚠️ Workaround needed | ✅ Native | Custom |
| **Link Tracking** | ⚠️ Separate system | ✅ Integrated | Custom |
| **Kai Integration** | ⚠️ Script injection | ✅ Native | Custom |
| **Knowledge Ownership** | ⚠️ Vendor docs | ✅ Full understanding | Custom |
| **Maintainability** | ⚠️ Limited by vendor | ✅ Complete control | Custom |
| **System Complexity** | 2 systems | 1 system | Custom |
| **Cost (5 years)** | ~$6,000 | ~$1,200 | Custom |
| **Maturity** | ✅ Very stable | ⚠️ We build it | CloudCannon |

---

## 🧠 The Knowledge Question

This is the **critical** factor:

### With CloudCannon
- **What team learns:** How to use CloudCannon
- **Knowledge dependency:** CloudCannon documentation, support, and roadmap
- **When issues arise:** Submit support ticket, wait for vendor
- **When features needed:** Request feature, wait for roadmap
- **Maintainability:** Dependent on vendor staying in business and maintaining product

### With Custom Build
- **What team learns:** How our system works (React, Supabase, GitHub API)
- **Knowledge dependency:** Our own documentation and codebase
- **When issues arise:** We can fix it ourselves (we wrote it)
- **When features needed:** We build it next sprint
- **Maintainability:** Fully sustainable as long as we maintain the codebase

**The question:** Do we want to invest in learning **their platform** or **our system**?

---

## 💡 How CloudCannon Workarounds Would Actually Work

### Approval Matrix Workaround

```typescript
// CloudCannon publishes content → Webhook fires
app.post('/webhooks/cloudcannon/publish', async (req) => {
  const { site, path } = req.body;
  
  // Look up content in our DB
  const content = await supabase
    .from('content_items')
    .select('*, submissions(*)')
    .eq('path', path)
    .single();
  
  // Check approval rules
  const rules = await getApprovalRules(site, content.type);
  const approvals = await getApprovals(content.submissions.id);
  
  if (approvals.length < rules.required_approvals) {
    // Not enough approvals - rollback!
    await cloudcannon.unpublish(site, path);
    await notify.error(`${path} published without approval`);
    return res.status(403).json({ error: 'Insufficient approvals' });
  }
  
  // Enough approvals - allow publish
  return res.status(200).json({ success: true });
});
```

**Reality:** This works, but it's reactive (rollback after publish) not preventive. Admin portal would need to show "ready to publish" status based on approvals.

### Link Tracking Workaround

```typescript
// Separate link service
app.get('/l/:code', async (req) => {
  const link = await supabase
    .from('tracked_links')
    .select('*')
    .eq('short_code', req.params.code)
    .single();
  
  // Track visit
  await supabase.from('link_visits').insert({
    link_id: link.id,
    ip: req.ip,
    user_agent: req.headers['user-agent'],
    referrer: req.headers.referer
  });
  
  // Redirect to CloudCannon-hosted content
  res.redirect(link.target_url);
});
```

**Reality:** This works fine. Link service would be separate from CloudCannon but functional.

### Kai Integration Workaround

```html
<!-- CloudCannon component: kai-widget.html -->
<script src="https://kai.kaptio.com/widget.js"></script>
<div id="kai-assistant" data-context="{{site}}/{{page}}"></div>
```

**Reality:** Works. Kai loads on every page, can access content context. Not as tight as native, but functional.

---

## 🎯 Recommendation

### If Speed is Critical (Launch in 1 month)
→ **Choose CloudCannon**
- Accept workarounds for approvals and tracking
- Get content creation started immediately
- Can always migrate to custom later if CloudCannon becomes limiting

### If Sustainable Knowledge is Priority (Launch in 3 months)
→ **Choose Custom Build**
- Invest in building expertise in our own system
- Full integration from day 1
- Long-term maintainability and ownership
- No vendor dependency

---

## 📝 Key Decision Makers

**Who should weigh in:**
- Product team (feature requirements)
- Content team (editor UX needs)
- Engineering team (build effort estimate)
- Leadership (strategic direction)

**Decision point:** Do we optimize for **time-to-market** or **long-term sustainability**?

---

**Last Updated:** 2025-01-20  
**Status:** Two viable options identified, decision pending

