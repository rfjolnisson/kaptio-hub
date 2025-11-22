# POC: Simple Gallery Site - Specification

**Launch Target:** End of this week  
**Purpose:** Support sales team immediately with pre-sales content  
**URL:** marketing.kaptio.com (or similar)

---

## 🎯 Goals

1. **Empower Sales:** Give sales team beautiful, accurate content to share with prospects
2. **Fast Launch:** Live in 1-2 days, not weeks/months
3. **Prove Workflow:** Test if magazine-style content works for sales process
4. **No Blockers:** Don't wait for CloudCannon or custom CMS to be ready

---

## 📋 What We Build

### Homepage (Gallery/Index)

Simple grid layout showing all available content:

```
┌─────────────────────────────────────────────────┐
│          Kaptio Pre-Sales Content               │
│                                                 │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │ Kaptio     │  │ Transfer   │  │ Booking    ││
│  │ Connect    │  │ Architecture│  │ Wizard     ││
│  │ Showcase   │  │ Guide      │  │ Overview   ││
│  └────────────┘  └────────────┘  └────────────┘│
│                                                 │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐│
│  │ ROI        │  │ Case Study:│  │ API        ││
│  │ Calculator │  │ Railbookers│  │ One-Pager  ││
│  └────────────┘  └────────────┘  └────────────┘│
└─────────────────────────────────────────────────┘
```

**Features:**
- Card-based grid layout
- Each card: Title, brief description, thumbnail
- Click → goes to full content page
- Filter by type (showcase, guide, case study, etc.)
- Search (simple JavaScript filter)

### Content Pages

Individual pages for each content piece:
- Full Kaptio Design System styling
- Can be magazine-style (like Connect Showcase)
- Can be guide-style (like Transfer Architecture)
- Can be simple one-pagers
- Each page self-contained

### Technology

```
Simple stack:
- HTML files (or markdown → HTML via simple build)
- Tailwind CSS + Kaptio Design System
- No framework needed (or minimal Vite if we want components)
- Deploy to Netlify
- Git for version control
```

---

## 📁 Project Structure

```
marketing-gallery/
├── index.html              # Gallery homepage
├── content/
│   ├── kaptio-connect/
│   │   └── index.html      # Existing Connect Showcase
│   ├── transfer-architecture/
│   │   └── index.html      # Existing Transfer Guide
│   ├── booking-wizard-overview/
│   │   └── index.html      # New content
│   └── ... more content pieces
├── assets/
│   ├── css/
│   │   └── styles.css      # Kaptio Design System
│   └── images/
└── netlify.toml            # Build config
```

---

## 🚀 How We Add New Content

### Option A: Pure HTML (Simplest)

```html
<!-- content/new-piece/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Content Title - Kaptio</title>
    <link href="/assets/css/styles.css" rel="stylesheet">
</head>
<body class="bg-kaptio-background">
    <!-- Use Kaptio Design System classes -->
    <div class="max-w-7xl mx-auto px-6 py-16">
        <h1 class="text-4xl font-bold text-kaptio-primary-800 mb-8">
            Content Title
        </h1>
        <!-- Content here -->
    </div>
</body>
</html>
```

**Workflow:**
1. Create new folder in `content/`
2. Create `index.html` with content
3. Add entry to gallery homepage
4. Git commit + push
5. Netlify auto-deploys

### Option B: Markdown → HTML (Slightly Better)

```markdown
<!-- content/new-piece/content.md -->
---
title: "Content Title"
description: "Brief description"
type: "showcase"
thumbnail: "/assets/images/thumb.png"
---

# Content Title

Your markdown content here...
```

**Simple build script:**
```javascript
// build.js - Convert markdown to HTML with template
const fs = require('fs');
const marked = require('marked');

// Read markdown, convert to HTML, wrap in Kaptio template
// Generate gallery index from all markdown files
```

---

## 🔗 Link Tracking (POC Version)

### Manual Tracking (Week 1)

Simple Google Sheet or Notion database:
- Sales person creates entry: Prospect name, Content URL, Date shared
- Send them: `https://marketing.kaptio.com/content/kaptio-connect`
- Manually track follow-ups

### Simple Tracker (Week 2-3)

Build tiny link shortener:

```typescript
// Netlify function: /.netlify/functions/track.ts
export async function handler(event) {
  const { code } = event.queryStringParameters;
  
  // Look up in simple JSON file or Supabase
  const link = links[code]; // e.g., { url: '/content/connect', prospect: 'Acme Corp' }
  
  // Log visit (append to file or insert to Supabase)
  await logVisit(code);
  
  // Redirect
  return {
    statusCode: 302,
    headers: { Location: link.url }
  };
}
```

Generate links manually or via simple admin page.

---

## 📊 Success Metrics (POC)

### Week 1-2
- [ ] Gallery site live
- [ ] 3-5 content pieces published
- [ ] Sales team trained on how to share links
- [ ] At least 3 prospects view content

### Week 3-4
- [ ] 10+ content pieces
- [ ] Basic link tracking operational
- [ ] Sales team feedback collected
- [ ] Decide: Does this workflow work?

**If YES → Proceed with CloudCannon or Custom**  
**If NO → Adjust and iterate on POC**

---

## 🎨 Design Example (Gallery Homepage)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Kaptio Marketing Content</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Kaptio Design System config -->
</head>
<body class="bg-kaptio-background">
    <header class="bg-kaptio-white border-b border-kaptio-grey-100 px-6 py-6">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <div>
                <h1 class="text-2xl font-bold text-kaptio-primary-800">Kaptio Content Library</h1>
                <p class="text-sm text-kaptio-grey-300">Pre-sales enablement materials</p>
            </div>
            <input 
                type="search" 
                placeholder="Search content..." 
                class="px-4 py-2 border border-kaptio-grey-200 rounded-lg"
            />
        </div>
    </header>

    <main class="max-w-7xl mx-auto px-6 py-12">
        <!-- Filters -->
        <div class="mb-8 flex space-x-4">
            <button class="px-4 py-2 bg-kaptio-primary-400 text-white rounded-lg">All</button>
            <button class="px-4 py-2 bg-kaptio-white text-kaptio-primary-400 rounded-lg">Showcases</button>
            <button class="px-4 py-2 bg-kaptio-white text-kaptio-primary-400 rounded-lg">Guides</button>
            <button class="px-4 py-2 bg-kaptio-white text-kaptio-primary-400 rounded-lg">One-Pagers</button>
        </div>

        <!-- Content Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <!-- Card -->
            <a href="/content/kaptio-connect" class="bg-kaptio-white rounded-lg shadow-kaptio p-6 hover:shadow-lg transition-shadow">
                <div class="aspect-video bg-kaptio-primary-100 rounded-lg mb-4"></div>
                <h3 class="text-lg font-bold text-kaptio-primary-800 mb-2">Kaptio Connect Showcase</h3>
                <p class="text-sm text-kaptio-grey-300 mb-3">
                    Integration platform for travel technology
                </p>
                <span class="text-xs bg-kaptio-primary-100 text-kaptio-primary-400 px-3 py-1 rounded-full">Showcase</span>
            </a>

            <!-- More cards... -->
        </div>
    </main>
</body>
</html>
```

---

## 💭 Why This POC Makes Sense

1. **No Waiting:** Sales team gets content immediately, doesn't wait 6-12 weeks
2. **De-risks Decision:** Proves the concept before committing to CloudCannon or custom
3. **Parallel Work:** Halldor can explore CloudCannon while team uses gallery
4. **Easy Migration:** Static content moves easily to any system later
5. **Real Feedback:** Learn what sales team actually needs before building full system

---

## 📝 Content to Include (Initial)

1. ✅ **Kaptio Connect Showcase** (already exists - migrate)
2. ✅ **Transfer Architecture Guide** (already exists - migrate)
3. ✅ **Booking Wizard Overview** (quick version from existing guide)
4. 🔄 **ROI Calculator** (simple interactive page)
5. 🔄 **Kaptio vs Alternatives** (comparison sheet)
6. 🔄 **Case Study: Railbookers** (customer success story)
7. 🔄 **API One-Pager** (technical overview)
8. 🔄 **Integration Capabilities** (what Kaptio can connect to)

**Target:** 8-10 pieces for POC launch

---

**Status:** Ready to build  
**Next Action:** Create project structure and build gallery homepage

