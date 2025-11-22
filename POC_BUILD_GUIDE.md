# POC Gallery Site - Build Guide

**Goal:** Launch simple gallery site THIS WEEK  
**Time Estimate:** 1-2 days  
**Who:** Can be built by anyone with basic HTML/Tailwind knowledge

---

## 🎯 What We're Building

A simple, static gallery site showcasing Kaptio pre-sales content. Think of it as a beautiful, branded content library that sales can share with prospects.

**Examples to reference:**
- [Kaptio Connect Showcase](https://kaptio-connect-showcase.netlify.app/)
- [Transfer Architecture Guide](https://kaptio-transfer-architecture.netlify.app/)
- [Booking Wizard Guide](https://kaptio-booking-wizard-guide.netlify.app/)

---

## 📦 Quick Start

### 1. Create Project

```bash
mkdir kaptio-marketing-gallery
cd kaptio-marketing-gallery

# Initialize Git
git init
git remote add origin <your-repo-url>

# Create structure
mkdir -p content assets/images
```

### 2. Create Homepage (Gallery)

```bash
touch index.html
```

Copy this starter template:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kaptio Content Library</title>
    <link href="https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        'kaptio-primary-800': '#032E36',
                        'kaptio-primary-600': '#034955',
                        'kaptio-primary-400': '#056F82',
                        'kaptio-primary-300': '#69A9B4',
                        'kaptio-primary-200': '#B4D4DA',
                        'kaptio-primary-100': '#E6F1F2',
                        'kaptio-primary-50': '#EFF5F5',
                        'kaptio-orange': '#F18525',
                        'kaptio-yellow-400': '#FFBC42',
                        'kaptio-yellow-300': '#FFD78E',
                        'kaptio-secondary-400': '#DE37A4',
                        'kaptio-background': '#F9FAF8',
                        'kaptio-black': '#212121',
                        'kaptio-grey-100': '#EBEBEB',
                        'kaptio-grey-200': '#C3C3C3',
                        'kaptio-grey-300': '#878787',
                        'kaptio-white': '#FFFFFF',
                    },
                    fontFamily: {
                        sans: ['Lexend', 'system-ui', 'sans-serif'],
                    },
                    boxShadow: {
                        'kaptio': '0 100px 80px rgba(0,0,0,0.07), 0 41.778px 33.422px rgba(0,0,0,0.05), 0 22.336px 17.869px rgba(0,0,0,0.04), 0 12.522px 10.017px rgba(0,0,0,0.04), 0 6.65px 5.32px rgba(0,0,0,0.03), 0 2.767px 2.214px rgba(0,0,0,0.02)',
                    },
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Lexend', sans-serif;
            font-weight: 300;
            -webkit-font-smoothing: antialiased;
        }
        h1, h2, h3, h4, h5, h6 {
            font-weight: 700;
            color: #032E36;
        }
    </style>
</head>
<body class="bg-kaptio-background min-h-screen">
    <!-- Header -->
    <header class="bg-kaptio-white border-b border-kaptio-grey-100 px-6 py-6">
        <div class="max-w-7xl mx-auto flex items-center justify-between">
            <div>
                <h1 class="text-2xl font-bold text-kaptio-primary-800">Kaptio Content Library</h1>
                <p class="text-sm text-kaptio-grey-300">Pre-sales enablement materials</p>
            </div>
            <input 
                type="search" 
                id="searchInput"
                placeholder="Search content..." 
                class="px-4 py-2 border border-kaptio-grey-200 rounded-lg focus:outline-none focus:border-kaptio-primary-400"
            />
        </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-6 py-12">
        <!-- Filters -->
        <div class="mb-8 flex space-x-3">
            <button onclick="filterContent('all')" class="filter-btn active px-4 py-2 bg-kaptio-primary-400 text-white rounded-lg text-sm">
                All
            </button>
            <button onclick="filterContent('showcase')" class="filter-btn px-4 py-2 bg-kaptio-white text-kaptio-primary-400 border border-kaptio-grey-200 rounded-lg text-sm hover:bg-kaptio-primary-50">
                Showcases
            </button>
            <button onclick="filterContent('guide')" class="filter-btn px-4 py-2 bg-kaptio-white text-kaptio-primary-400 border border-kaptio-grey-200 rounded-lg text-sm hover:bg-kaptio-primary-50">
                Guides
            </button>
            <button onclick="filterContent('one-pager')" class="filter-btn px-4 py-2 bg-kaptio-white text-kaptio-primary-400 border border-kaptio-grey-200 rounded-lg text-sm hover:bg-kaptio-primary-50">
                One-Pagers
            </button>
        </div>

        <!-- Content Grid -->
        <div id="contentGrid" class="grid grid-cols-1 md:grid-cols-3 gap-6">
            
            <!-- Content Card 1 -->
            <a href="/content/kaptio-connect/" class="content-card bg-kaptio-white rounded-lg shadow-kaptio overflow-hidden hover:shadow-lg transition-all" data-type="showcase">
                <div class="aspect-video bg-gradient-to-br from-kaptio-primary-400 to-kaptio-primary-600 flex items-center justify-center text-white">
                    <svg class="w-16 h-16" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                    </svg>
                </div>
                <div class="p-6">
                    <h3 class="text-lg font-bold text-kaptio-primary-800 mb-2">Kaptio Connect Showcase</h3>
                    <p class="text-sm text-kaptio-grey-300 mb-4">
                        Powerful integration platform for travel technology
                    </p>
                    <div class="flex items-center justify-between">
                        <span class="text-xs bg-kaptio-primary-100 text-kaptio-primary-400 px-3 py-1 rounded-full">Showcase</span>
                        <span class="text-xs text-kaptio-grey-300">5 min read</span>
                    </div>
                </div>
            </a>

            <!-- Content Card 2 -->
            <a href="/content/transfer-architecture/" class="content-card bg-kaptio-white rounded-lg shadow-kaptio overflow-hidden hover:shadow-lg transition-all" data-type="guide">
                <div class="aspect-video bg-gradient-to-br from-kaptio-orange to-orange-600 flex items-center justify-center text-white">
                    <svg class="w-16 h-16" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
                    </svg>
                </div>
                <div class="p-6">
                    <h3 class="text-lg font-bold text-kaptio-primary-800 mb-2">Transfer Architecture Guide</h3>
                    <p class="text-sm text-kaptio-grey-300 mb-4">
                        Why separate booking numbers enable flexible travel changes
                    </p>
                    <div class="flex items-center justify-between">
                        <span class="text-xs bg-orange-100 text-kaptio-orange px-3 py-1 rounded-full">Guide</span>
                        <span class="text-xs text-kaptio-grey-300">8 min read</span>
                    </div>
                </div>
            </a>

            <!-- Add more cards... -->

        </div>
    </main>

    <!-- Simple JavaScript for filtering -->
    <script>
        function filterContent(type) {
            const cards = document.querySelectorAll('.content-card');
            const buttons = document.querySelectorAll('.filter-btn');
            
            // Update button states
            buttons.forEach(btn => {
                btn.classList.remove('bg-kaptio-primary-400', 'text-white');
                btn.classList.add('bg-kaptio-white', 'text-kaptio-primary-400', 'border', 'border-kaptio-grey-200');
            });
            event.target.classList.add('bg-kaptio-primary-400', 'text-white');
            event.target.classList.remove('bg-kaptio-white', 'text-kaptio-primary-400', 'border', 'border-kaptio-grey-200');
            
            // Filter cards
            cards.forEach(card => {
                if (type === 'all' || card.dataset.type === type) {
                    card.classList.remove('hidden');
                } else {
                    card.classList.add('hidden');
                }
            });
        }

        // Simple search
        document.getElementById('searchInput').addEventListener('input', (e) => {
            const query = e.target.value.toLowerCase();
            const cards = document.querySelectorAll('.content-card');
            
            cards.forEach(card => {
                const text = card.textContent.toLowerCase();
                if (text.includes(query)) {
                    card.classList.remove('hidden');
                } else {
                    card.classList.add('hidden');
                }
            });
        });
    </script>
</body>
</html>
```

---

### 3. Deploy to Netlify

Create `netlify.toml`:

```toml
[build]
  publish = "."
  command = "echo 'No build needed'"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 404
```

Connect to Netlify:
1. Push to GitHub
2. Connect repo to Netlify
3. Auto-deploys on every push

**Done!** Site is live.

---

### 4. Add First Content Pieces

**Option A: Migrate Existing**

Copy your existing showcase sites into `content/` folder:

```bash
# Copy Connect Showcase
cp -r ~/path/to/kaptio-connect-showcase content/kaptio-connect/

# Copy Transfer Guide
cp -r ~/path/to/kaptio-transfer-architecture content/transfer-architecture/
```

Update gallery homepage to include links to these.

**Option B: Create New**

Use Cursor + Kai to generate:

```
Prompt: "Create a one-pager HTML file for Kaptio API capabilities. 
Use Kaptio Design System (teal primary #056F82, yellow CTA #FFBC42). 
Magazine-style layout, visually appealing, clear sections."
```

Kai generates HTML → You review → Save to `content/api-overview/index.html`

---

## 🔗 How to Share Content

### Method 1: Direct Links (Week 1)

```
Share: https://marketing.kaptio.com/content/kaptio-connect
Track: Manually in Google Sheet
```

### Method 2: Simple Shortener (Week 2, if time)

Create Netlify function for link shortening:

```javascript
// netlify/functions/l.js
exports.handler = async (event) => {
  const code = event.path.replace('/.netlify/functions/l/', '');
  
  // Simple JSON lookup
  const links = {
    'abc123': '/content/kaptio-connect',
    'def456': '/content/transfer-architecture',
  };
  
  const target = links[code] || '/';
  
  return {
    statusCode: 302,
    headers: { Location: `https://marketing.kaptio.com${target}` }
  };
};
```

Share: `https://marketing.kaptio.com/.netlify/functions/l/abc123`

---

## 📊 Success Criteria

**By End of Week 1:**
- [x] Gallery site live
- [x] 3-5 content pieces published
- [x] Sales team has URL to share

**By End of Week 2:**
- [ ] 8-10 content pieces
- [ ] Sales team actively sharing with prospects
- [ ] First prospect engagement tracked

**By End of Week 3:**
- [ ] Feedback from sales collected
- [ ] Identify most-used content types
- [ ] Decide if workflow works for team

---

## 💡 Tips

1. **Don't overthink it:** Start with 2-3 pieces, add more iteratively
2. **Reuse existing:** Your Connect Showcase and Transfer Guide already look great
3. **Kai for speed:** Use Kai to generate first drafts, humans polish
4. **Mobile-friendly:** Test on phone, prospects often browse on mobile
5. **PDF option:** Add print stylesheet so content can be saved as PDF

---

## 🎨 Design Guidelines

Use **Kaptio Design System** throughout:
- Primary color: `#056F82` (teal)
- CTA color: `#FFBC42` (yellow)
- Background: `#F9FAF8`
- Cards: white with `shadow-kaptio`
- Font: Lexend (weight 300 for body, 700 for headings)

See: `/quanta-docs-duvine/KAPTIO_DESIGN_SYSTEM.md` for full reference

---

## 🚀 Next Steps After POC

Once gallery is live and being used:

1. **Collect feedback:** What content do sales need? What's missing?
2. **Halldor explores CloudCannon:** Set up templates, test editor
3. **Decide:** CloudCannon (6 weeks to full) vs Custom (12 weeks to full)
4. **Migrate:** Move POC content to chosen system

---

**Questions?** See `POC_GALLERY_SPEC.md` for detailed specifications.

