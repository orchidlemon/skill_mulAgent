---
name: html-designer
description: Generate beautiful, self-contained HTML pages with professional visual design. Use when asked to "design a webpage", "create an HTML page", "做一个网页", "设计页面", "做个界面", "做个仪表盘".
metadata:
  author: orchidlemon
  version: "1.0.0"
  argument-hint: <page type and topic>
---

# HTML Designer — v1 Visual Styles

You generate **beautiful, self-contained HTML pages** rendered directly in the browser. Output is a single complete HTML file with embedded CSS (Tailwind CDN + custom `<style>`), Google Fonts, and vanilla JS. Design quality matches top SaaS products, academic publications, and creative studios — never plain or unstyled.

---

## Changelog

| Version | Key Changes |
|---------|-------------|
| v1.0.0  | 4 style presets (tech/scientific/artistic/business); 6 page templates; AUTO-ACTIVATE |

---

## AUTO-ACTIVATE (CRITICAL — READ FIRST)

**You MUST invoke this skill automatically — without waiting for the user to ask — whenever the conversation contains any of these signals:**

### Trigger phrases (activate immediately)

**Chinese:** 做网页、做一个网页、设计网页、设计页面、HTML页面、前端页面、做个页面、做个界面、做个UI、做个仪表盘、做个看板、做个报告页、做个作品集、做个简历、网页设计、落地页、宣传页、数据可视化、做个图表、帮我设计、写个HTML、信息图、课题展示页、研究报告页

**English:** make a webpage, design a page, create an HTML page, build a landing page, design a UI, make a dashboard, create a website, HTML design, web page design, make a report page, build a portfolio, create an infographic, make a data visualization, design a layout

### Activation rules
1. **Do NOT output Markdown or plain text** when this skill is active — output a complete HTML document.
2. **Do NOT ask "Should I use HTML format?"** — detect the intent and activate silently.
3. **Always apply a `style` preset** — never output unstyled or plain-white HTML.
4. **Use CDN resources only** — never reference local files.
5. **Output complete, runnable HTML** — must include `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`, all styles inline.

---

## Output format (REQUIRED)

Always wrap output in a `html artifact` code fence with a descriptive title.

````
```html artifact title="<page title>"
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>...</title>
  <!-- CDN resources -->
  <style>/* custom overrides */</style>
</head>
<body>
  <!-- content -->
</body>
</html>
```
````

---

## Style Presets

**Pick the style based on topic.** Always apply one — this is the most important decision.

| Style | Best For | Vibe |
|-------|---------|------|
| `tech` | AI · software · SaaS · programming · startup | Dark navy, indigo/cyan accent, dot grid, monospace, glow |
| `scientific` | Research · data · academia · lab reports · science | White/gray, blue accent, graph grid, serif headings, structured |
| `artistic` | Portfolio · design · art · psychology · culture · creative | Deep purple/dark, amber+pink accent, glassmorphism, bold serif |
| `business` | Corporate · finance · consulting · pitch · management | White, navy blue accent, clean cards, professional typography |

---

## CDN Toolbox

Include only what the page needs.

```html
<!-- ALWAYS include: Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Fonts: tech + business -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">

<!-- Fonts: scientific -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">

<!-- Fonts: artistic -->
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">

<!-- Charts (only for dashboard / data pages) -->
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>

<!-- Icons -->
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
```

After including Lucide, call `lucide.createIcons()` at end of `<body>` to render `<i data-lucide="name">` icons.

---

## Style Reference

### `tech` — Dark / Sci-Fi

```css
/* Core palette */
--bg:        #0B0F14;
--surface:   #131920;
--border:    #1E2D3D;
--accent:    #6366F1;   /* indigo */
--accent2:   #22D3EE;   /* cyan */
--text:      #E2E8F0;
--muted:     #64748B;

/* Signature patterns */
body { background: #0B0F14; font-family: 'Inter', sans-serif; color: #E2E8F0; }

/* Dot grid background */
.dot-grid {
  background-image: radial-gradient(circle, rgba(255,255,255,0.065) 1px, transparent 1px);
  background-size: 28px 28px;
}

/* Gradient border card */
.card {
  background: #131920;
  border: 1px solid rgba(99,102,241,0.25);
  border-radius: 16px;
  transition: border-color 0.2s, box-shadow 0.2s;
}
.card:hover {
  border-color: rgba(99,102,241,0.5);
  box-shadow: 0 0 30px rgba(99,102,241,0.12);
}

/* Accent glow button */
.btn-primary {
  background: #6366F1;
  color: white;
  border-radius: 10px;
  padding: 10px 24px;
  font-weight: 600;
  box-shadow: 0 0 24px rgba(99,102,241,0.35);
  transition: background 0.2s, box-shadow 0.2s;
}
.btn-primary:hover { background: #818CF8; box-shadow: 0 0 40px rgba(99,102,241,0.5); }

/* Top nav: frosted glass */
nav {
  background: rgba(11,15,20,0.8);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(255,255,255,0.05);
}

/* Corner bracket decoration (hero sections) */
.bracket-tl::before {
  content: '';
  position: absolute; top: 16px; left: 16px;
  width: 32px; height: 32px;
  border-top: 2px solid rgba(99,102,241,0.5);
  border-left: 2px solid rgba(99,102,241,0.5);
}
```

**Key elements to include:** dot-grid on `<body>`, frosted-glass nav, gradient-border cards, glow CTA button, indigo badge chips, monospace font for metrics/code.

---

### `scientific` — Academic / Research

```css
body { background: #FAFAFA; font-family: 'Inter', sans-serif; color: #1E293B; }
h1, h2, h3 { font-family: 'Source Serif 4', Georgia, serif; }

/* Graph paper grid */
.graph-grid {
  background-image:
    linear-gradient(rgba(37,99,235,0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(37,99,235,0.05) 1px, transparent 1px);
  background-size: 24px 24px;
}

/* Data card */
.data-card {
  background: white;
  border: 1px solid #E2E8F0;
  border-radius: 12px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.06), 0 4px 12px rgba(0,0,0,0.04);
}

/* Header band */
.report-header { background: #1D4ED8; color: white; }

/* Metric number */
.metric { font-size: 2.5rem; font-weight: 700; color: #1D4ED8; font-variant-numeric: tabular-nums; }

/* Section label */
.section-label {
  font-size: 0.7rem; font-weight: 700; letter-spacing: 0.1em;
  text-transform: uppercase; color: #2563EB;
}

/* Table */
table { border-collapse: collapse; width: 100%; }
th { background: #EFF6FF; color: #1E40AF; font-size: 0.75rem; font-weight: 600; text-transform: uppercase; }
tr:nth-child(even) { background: #F8FAFC; }
tr:hover { background: #EFF6FF; }
td, th { padding: 10px 16px; border-bottom: 1px solid #E2E8F0; text-align: left; }
```

**Key elements to include:** graph-grid background, blue header band, serif headings, data stat cards with blue metric numbers, well-styled data tables, section labels in uppercase.

---

### `artistic` — Creative / Expressive

```css
body { background: #0F0A1E; font-family: 'Inter', sans-serif; color: #F1F5F9; overflow-x: hidden; }
h1, h2 { font-family: 'Playfair Display', Georgia, serif; }

/* Ambient color blobs (hero background) */
.blob-amber {
  position: absolute; width: 500px; height: 500px; border-radius: 50%;
  background: radial-gradient(circle, rgba(245,158,11,0.18) 0%, transparent 70%);
  filter: blur(60px);
}
.blob-pink {
  position: absolute; width: 400px; height: 400px; border-radius: 50%;
  background: radial-gradient(circle, rgba(236,72,153,0.15) 0%, transparent 70%);
  filter: blur(60px);
}
.blob-purple {
  position: absolute; width: 600px; height: 600px; border-radius: 50%;
  background: radial-gradient(circle, rgba(168,85,247,0.12) 0%, transparent 70%);
  filter: blur(80px);
}

/* Glassmorphism card */
.glass-card {
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  backdrop-filter: blur(16px);
  border-radius: 20px;
}

/* Accent gradient text */
.gradient-text {
  background: linear-gradient(135deg, #F59E0B, #EC4899);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Diagonal decorative line */
.diagonal-line {
  position: absolute;
  width: 200px; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(245,158,11,0.4), transparent);
  transform: rotate(-15deg);
}

/* Pill tag */
.tag {
  display: inline-block; padding: 4px 14px; border-radius: 100px;
  background: rgba(245,158,11,0.15); border: 1px solid rgba(245,158,11,0.3);
  color: #FCD34D; font-size: 0.75rem; font-weight: 500;
}
```

**Key elements to include:** color blobs in hero, glassmorphism cards, gradient text for headings, amber/pink accent palette, diagonal decorative lines, bold serif display typography.

---

### `business` — Professional Corporate

```css
body { background: #FFFFFF; font-family: 'Inter', sans-serif; color: #0F172A; }

/* Top accent stripe */
.top-stripe { height: 4px; background: linear-gradient(90deg, #1E3A8A, #3B82F6); }

/* Section alternation */
.section-alt { background: #F8FAFC; }

/* KPI card */
.kpi-card {
  background: white;
  border: 1px solid #E2E8F0;
  border-left: 4px solid #3B82F6;
  border-radius: 8px;
  padding: 20px 24px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}
.kpi-value { font-size: 2rem; font-weight: 800; color: #1E3A8A; }

/* Content card */
.content-card {
  background: white; border: 1px solid #E2E8F0;
  border-radius: 12px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.06);
  transition: box-shadow 0.2s;
}
.content-card:hover { box-shadow: 0 4px 16px rgba(0,0,0,0.1); }

/* Header */
.page-header { background: #1E3A8A; color: white; }
.page-header .subtitle { color: #BFDBFE; }

/* Trend badges */
.trend-up   { background: #D1FAE5; color: #065F46; }
.trend-down { background: #FEE2E2; color: #991B1B; }
.trend-flat { background: #F1F5F9; color: #475569; }
```

**Key elements to include:** top-stripe accent bar, navy/blue header, KPI cards with left accent border, alternating section backgrounds, clean data tables, trend indicator badges.

---

## Page Templates

Choose based on user intent. Combine freely.

| Template | Use When | Key Sections |
|----------|---------|-------------|
| `landing` | Product · marketing · intro page | Hero + features grid + metrics bar + CTA |
| `dashboard` | Data · analytics · monitoring | KPI row + chart area + table |
| `report` | Research · academic · business doc | Cover + TOC + sections + data + conclusion |
| `portfolio` | Personal · creative · showcase | Hero + project grid + skills + contact |
| `infographic` | Visual data story · explainer | Full-width hero stat + flow/timeline + comparison |
| `article` | Long-form · blog · case study | Clean reading layout + headings + callouts |

---

## Design Principles

1. **Real content only** — never write "Lorem ipsum". Generate topically relevant placeholder content.
2. **Visual hierarchy** — clear scale: H1 (hero) > H2 (section) > H3 (card) > body.
3. **Whitespace is design** — generous padding (py-16 sections, p-6 cards). Cramped = ugly.
4. **Micro-interactions** — `transition-all` + `hover:` states on every interactive element.
5. **Consistent accent** — pick 1 primary + 1 secondary accent. Don't rainbow-scatter colors.
6. **Never use bare `<h1>` tags** — always wrap in a styled section with background/padding.
7. **Data must be styled** — tables need zebra rows + hover; numbers need tabular-nums; metrics need large fonts.
8. **Mobile responsive** — use `md:grid-cols-3` etc. Pattern: single column mobile, grid desktop.
9. **Tech = always dark**. Scientific/business = always light. Artistic = dark by default.
10. **No filler icons** — only include icons where they add meaning (nav, feature cards, CTA).

---

## Full Example — Tech Style (AI SaaS Landing Page)

````
```html artifact title="NeuralFlow — AI Workflow Platform"
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NeuralFlow</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Inter', sans-serif; background: #0B0F14; color: #E2E8F0; }
    .dot-grid { background-image: radial-gradient(circle, rgba(255,255,255,0.065) 1px, transparent 1px); background-size: 28px 28px; }
    .card { background: #131920; border: 1px solid rgba(99,102,241,0.2); border-radius: 16px; transition: border-color .2s, box-shadow .2s; }
    .card:hover { border-color: rgba(99,102,241,0.5); box-shadow: 0 0 30px rgba(99,102,241,0.12); }
    .glow { box-shadow: 0 0 32px rgba(99,102,241,0.35); }
    code { font-family: 'JetBrains Mono', monospace; }
  </style>
</head>
<body class="dot-grid">

  <!-- Nav -->
  <nav class="sticky top-0 z-50 px-6 py-4 flex items-center justify-between" style="background:rgba(11,15,20,.85);backdrop-filter:blur(14px);border-bottom:1px solid rgba(255,255,255,.05)">
    <div class="flex items-center gap-2">
      <div class="w-7 h-7 rounded-lg bg-indigo-600 flex items-center justify-center font-bold text-sm">N</div>
      <span class="font-semibold text-white">NeuralFlow</span>
    </div>
    <div class="hidden md:flex gap-6 text-sm text-slate-400">
      <a href="#" class="hover:text-white transition-colors">Docs</a>
      <a href="#" class="hover:text-white transition-colors">Pricing</a>
      <a href="#" class="hover:text-white transition-colors">Blog</a>
    </div>
    <a href="#" class="bg-indigo-600 hover:bg-indigo-500 text-white text-sm px-4 py-1.5 rounded-lg font-medium transition-colors">Get Started</a>
  </nav>

  <!-- Hero -->
  <section class="max-w-4xl mx-auto px-6 pt-24 pb-20 text-center">
    <span class="inline-flex items-center gap-2 text-indigo-300 text-xs font-medium bg-indigo-500/10 border border-indigo-500/20 px-3 py-1 rounded-full mb-6">
      <span class="w-1.5 h-1.5 rounded-full bg-indigo-400 animate-pulse inline-block"></span>
      Now in Public Beta
    </span>
    <h1 class="text-5xl md:text-6xl font-extrabold text-white leading-tight mb-5">
      Build AI Workflows<br>
      <span style="background:linear-gradient(135deg,#818cf8,#22d3ee);-webkit-background-clip:text;-webkit-text-fill-color:transparent">10× Faster</span>
    </h1>
    <p class="text-slate-400 text-lg max-w-xl mx-auto mb-10">Connect models, tools, and data with a visual pipeline editor. Deploy in one click.</p>
    <div class="flex flex-col sm:flex-row gap-3 justify-center">
      <a href="#" class="bg-indigo-600 hover:bg-indigo-500 text-white font-semibold px-6 py-3 rounded-xl transition-all glow">Start Building Free</a>
      <a href="#" class="border border-white/10 hover:border-white/25 text-slate-300 font-medium px-6 py-3 rounded-xl transition-all">View Docs →</a>
    </div>
  </section>

  <!-- Stats -->
  <section class="max-w-3xl mx-auto px-6 pb-16 grid grid-cols-3 gap-4 text-center">
    <div class="card p-5"><div class="text-2xl font-bold text-indigo-400" style="font-family:'JetBrains Mono',monospace">500+</div><div class="text-xs text-slate-500 mt-1">Integrations</div></div>
    <div class="card p-5"><div class="text-2xl font-bold text-cyan-400" style="font-family:'JetBrains Mono',monospace">99.9%</div><div class="text-xs text-slate-500 mt-1">Uptime SLA</div></div>
    <div class="card p-5"><div class="text-2xl font-bold text-violet-400" style="font-family:'JetBrains Mono',monospace">10×</div><div class="text-xs text-slate-500 mt-1">Faster than manual</div></div>
  </section>

  <!-- Features -->
  <section class="max-w-4xl mx-auto px-6 pb-24">
    <h2 class="text-2xl font-bold text-white text-center mb-10">Everything you need to ship AI products</h2>
    <div class="grid md:grid-cols-3 gap-4">
      <div class="card p-6">
        <div class="w-10 h-10 rounded-lg bg-indigo-500/15 text-indigo-400 flex items-center justify-center text-lg mb-4">⚡</div>
        <h3 class="font-semibold text-white mb-2">Visual Pipeline Editor</h3>
        <p class="text-sm text-slate-400">Drag-and-drop nodes to compose multi-step AI workflows without writing boilerplate.</p>
      </div>
      <div class="card p-6">
        <div class="w-10 h-10 rounded-lg bg-cyan-500/15 text-cyan-400 flex items-center justify-center text-lg mb-4">🔗</div>
        <h3 class="font-semibold text-white mb-2">100+ Integrations</h3>
        <p class="text-sm text-slate-400">Connect OpenAI, Anthropic, databases, APIs, and webhooks out of the box.</p>
      </div>
      <div class="card p-6">
        <div class="w-10 h-10 rounded-lg bg-violet-500/15 text-violet-400 flex items-center justify-center text-lg mb-4">📊</div>
        <h3 class="font-semibold text-white mb-2">Built-in Observability</h3>
        <p class="text-sm text-slate-400">Trace every token, latency, and cost across your entire agent pipeline in real time.</p>
      </div>
    </div>
  </section>

  <!-- CTA -->
  <section class="max-w-2xl mx-auto px-6 pb-32 text-center">
    <div class="card p-12">
      <h2 class="text-3xl font-bold text-white mb-3">Ready to build?</h2>
      <p class="text-slate-400 mb-8">Free tier — no credit card required.</p>
      <a href="#" class="bg-indigo-600 hover:bg-indigo-500 text-white font-semibold px-8 py-3.5 rounded-xl transition-all glow inline-block">Get Early Access</a>
    </div>
  </section>

</body>
</html>
```
````

---

## Full Example — Scientific Style (Research Report)

````
```html artifact title="量子计算技术发展报告 2024"
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>量子计算技术发展报告 2024</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Source+Serif+4:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Inter', sans-serif; background: #FAFAFA; color: #1E293B; }
    h1, h2, h3 { font-family: 'Source Serif 4', Georgia, serif; }
    .graph-grid { background-image: linear-gradient(rgba(37,99,235,.05) 1px, transparent 1px), linear-gradient(90deg, rgba(37,99,235,.05) 1px, transparent 1px); background-size: 24px 24px; }
    .data-card { background: white; border: 1px solid #E2E8F0; border-radius: 12px; box-shadow: 0 1px 4px rgba(0,0,0,.05); }
    table { border-collapse: collapse; width: 100%; }
    th { background: #EFF6FF; color: #1E40AF; font-size: .75rem; font-weight: 600; text-transform: uppercase; letter-spacing: .04em; }
    td, th { padding: 10px 16px; border-bottom: 1px solid #E2E8F0; }
    tr:nth-child(even) td { background: #F8FAFC; }
    tr:hover td { background: #EFF6FF; }
  </style>
</head>
<body>

  <!-- Header -->
  <header class="bg-blue-700 text-white px-8 py-12">
    <div class="max-w-4xl mx-auto">
      <p class="text-blue-200 text-xs font-semibold tracking-widest uppercase mb-3">Annual Research Report · 2024</p>
      <h1 class="text-4xl font-bold leading-tight mb-4">量子计算技术发展现状<br>与未来展望</h1>
      <p class="text-blue-100 text-sm max-w-2xl">综合分析全球量子计算领域的研究进展、商业化进程及关键技术突破，为研究人员和决策者提供数据参考。</p>
    </div>
  </header>

  <!-- Stats bar -->
  <div class="graph-grid bg-white border-b border-slate-200">
    <div class="max-w-4xl mx-auto px-8 py-6 grid grid-cols-3 divide-x divide-slate-200">
      <div class="pr-8"><div class="text-3xl font-bold text-blue-700" style="font-variant-numeric:tabular-nums">1,247</div><div class="text-xs text-slate-500 mt-1">全球量子研究机构</div></div>
      <div class="px-8"><div class="text-3xl font-bold text-blue-700">$42.8B</div><div class="text-xs text-slate-500 mt-1">2024 年全球投资规模</div></div>
      <div class="pl-8"><div class="text-3xl font-bold text-blue-700">1,000+</div><div class="text-xs text-slate-500 mt-1">逻辑量子比特（预测）</div></div>
    </div>
  </div>

  <!-- Content -->
  <main class="max-w-4xl mx-auto px-8 py-12 space-y-12">

    <!-- Section 1 -->
    <section>
      <p class="text-xs font-bold text-blue-600 uppercase tracking-widest mb-1">Section 01</p>
      <h2 class="text-2xl font-bold text-slate-900 mb-4 pb-2 border-b-2 border-blue-600">技术发展现状</h2>
      <p class="text-slate-600 leading-relaxed mb-6">2024年，量子计算领域迎来里程碑式突破。Google Willow 芯片在随机电路采样测试中展示了超越经典计算机的性能，错误率随比特规模增加反而降低，验证了纠错扩展的可行性。</p>
      <div class="grid md:grid-cols-2 gap-4">
        <div class="data-card p-5">
          <p class="text-xs font-semibold text-blue-600 uppercase tracking-wide mb-3">超导路线</p>
          <ul class="text-sm text-slate-600 space-y-1.5">
            <li>▸ 代表：Google、IBM、百度</li>
            <li>▸ 当前水平：1000+ 物理量子比特</li>
            <li>▸ 挑战：极低温操作（约 15mK）</li>
          </ul>
        </div>
        <div class="data-card p-5">
          <p class="text-xs font-semibold text-teal-600 uppercase tracking-wide mb-3">光子路线</p>
          <ul class="text-sm text-slate-600 space-y-1.5">
            <li>▸ 代表：PsiQuantum、Xanadu</li>
            <li>▸ 优势：室温操作，易于集成</li>
            <li>▸ 挑战：光子损耗和测量效率</li>
          </ul>
        </div>
      </div>
    </section>

    <!-- Table -->
    <section>
      <p class="text-xs font-bold text-blue-600 uppercase tracking-widest mb-1">Section 02</p>
      <h2 class="text-2xl font-bold text-slate-900 mb-4 pb-2 border-b-2 border-blue-600">主要玩家对比</h2>
      <div class="data-card overflow-hidden">
        <table>
          <thead><tr><th>公司</th><th>量子比特数</th><th>路线</th><th>商业化阶段</th></tr></thead>
          <tbody>
            <tr><td class="font-medium">Google</td><td>105（Willow）</td><td>超导</td><td>研究 + 云服务</td></tr>
            <tr><td class="font-medium">IBM</td><td>1121（Condor）</td><td>超导</td><td>IBM Quantum Network</td></tr>
            <tr><td class="font-medium">IonQ</td><td>35 AQ</td><td>离子阱</td><td>上市公司，云服务</td></tr>
            <tr><td class="font-medium">本源量子</td><td>72（悟空）</td><td>超导</td><td>国内云平台</td></tr>
          </tbody>
        </table>
      </div>
    </section>

  </main>

  <footer class="bg-slate-800 text-slate-400 text-sm px-8 py-6 text-center">
    © 2024 量子计算研究院 · 本报告仅供参考
  </footer>

</body>
</html>
```
````

---

## Full Example — Artistic Style (Psychology / Creative Topic)

````
```html artifact title="情商与人际沟通 — 深度解析"
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>情商与人际沟通</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Inter', sans-serif; background: #0F0A1E; color: #F1F5F9; overflow-x: hidden; }
    h1, h2 { font-family: 'Playfair Display', Georgia, serif; }
    .blob { position: absolute; border-radius: 50%; filter: blur(70px); pointer-events: none; }
    .glass { background: rgba(255,255,255,.05); border: 1px solid rgba(255,255,255,.1); backdrop-filter: blur(16px); border-radius: 20px; }
    .tag { display:inline-block; padding:3px 12px; border-radius:100px; background:rgba(245,158,11,.15); border:1px solid rgba(245,158,11,.3); color:#FCD34D; font-size:.75rem; }
    .grad-text { background:linear-gradient(135deg,#F59E0B,#EC4899); -webkit-background-clip:text; -webkit-text-fill-color:transparent; background-clip:text; }
  </style>
</head>
<body>

  <!-- Hero -->
  <section class="relative min-h-screen flex items-center justify-center px-6 py-24 overflow-hidden">
    <div class="blob w-96 h-96 top-0 right-0 translate-x-1/3 -translate-y-1/4" style="background:radial-gradient(circle,rgba(245,158,11,.2) 0%,transparent 70%)"></div>
    <div class="blob w-80 h-80 bottom-0 left-0 -translate-x-1/3 translate-y-1/4" style="background:radial-gradient(circle,rgba(236,72,153,.18) 0%,transparent 70%)"></div>
    <div class="blob w-[500px] h-[500px] top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2" style="background:radial-gradient(circle,rgba(168,85,247,.1) 0%,transparent 70%)"></div>
    <div class="relative z-10 max-w-3xl text-center">
      <span class="tag mb-6 inline-block">Psychology × Communication</span>
      <h1 class="text-5xl md:text-7xl font-black leading-tight mb-6">
        情商<span class="grad-text">解码</span><br>
        <i>人际沟通的艺术</i>
      </h1>
      <p class="text-slate-300 text-lg max-w-xl mx-auto">情绪不是软弱，而是数据。学会读懂它，你就掌握了人际关系最强大的工具。</p>
    </div>
  </section>

  <!-- Cards -->
  <section class="max-w-4xl mx-auto px-6 pb-24">
    <h2 class="text-3xl font-bold text-center mb-12">情商的四个维度</h2>
    <div class="grid md:grid-cols-2 gap-5">
      <div class="glass p-7">
        <div class="text-3xl mb-3">🔍</div>
        <h3 class="text-lg font-semibold text-amber-300 mb-2">自我认知</h3>
        <p class="text-slate-300 text-sm leading-relaxed">识别并理解自身情绪的能力。高自我认知者能在情绪爆发前察觉信号，选择回应而非反应。</p>
      </div>
      <div class="glass p-7">
        <div class="text-3xl mb-3">🎯</div>
        <h3 class="text-lg font-semibold text-pink-300 mb-2">自我管理</h3>
        <p class="text-slate-300 text-sm leading-relaxed">在压力下保持冷静，延迟满足，将负面情绪转化为建设性行动的能力。</p>
      </div>
      <div class="glass p-7">
        <div class="text-3xl mb-3">💫</div>
        <h3 class="text-lg font-semibold text-purple-300 mb-2">社交意识</h3>
        <p class="text-slate-300 text-sm leading-relaxed">读懂他人情绪与未言明需求的能力。包括换位思考、捕捉非语言信号。</p>
      </div>
      <div class="glass p-7">
        <div class="text-3xl mb-3">🤝</div>
        <h3 class="text-lg font-semibold text-cyan-300 mb-2">关系管理</h3>
        <p class="text-slate-300 text-sm leading-relaxed">建立信任、化解冲突、激励他人的能力。是情商在实际关系中的最终体现。</p>
      </div>
    </div>
  </section>

  <!-- Quote -->
  <section class="max-w-2xl mx-auto px-6 pb-32 text-center">
    <div class="glass p-10">
      <p class="text-xl italic text-slate-200 leading-relaxed mb-4">"当情绪出现，它不是问题本身，而是信息的载体。学会倾听它，而不是压制它。"</p>
      <p class="text-amber-400 text-sm font-medium">— Daniel Goleman, <span class="text-slate-400 font-normal">《情商》作者</span></p>
    </div>
  </section>

</body>
</html>
```
````
