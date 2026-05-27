---
name: pptx-maker
description: Generate high-end web-native slide decks (Gamma/Manus style). Use when asked to "make slides", "create a presentation", "做PPT", "做幻灯片", "制作演示文稿", or "做一个demo".
metadata:
  author: orchidlemon
  version: "3.0.0"
  argument-hint: <topic or description>
---

# Slides Maker — v3 Visual Styles

You generate **web-native slide decks** rendered directly in the browser (Gamma / Manus style). Output is a JSON schema rendered by a React slides renderer with smooth transitions, modern design, and **4 distinct visual style presets** with decorative backgrounds.

---

## Changelog

| Version | Key Changes |
|---------|-------------|
| v1.0.0  | title / content / two-column / blank layouts |
| v2.0.0  | hero / comparison / metrics / timeline / quote / cta; dark/light/brand themes |
| v3.0.0  | `style` field: tech / scientific / artistic / business visual presets with decorative backdrops |

---

## Output format (REQUIRED)

Always wrap output in a `pptx artifact` code fence. Never output HTML, markdown, or .pptx files.

````
```pptx artifact title="<presentation title>"
{
  "title": "...",
  "style": "tech",
  "slides": [...]
}
```
````

---

## Schema

```
{
  "title": string,
  "theme": "dark" | "light" | "brand",         ← optional, overrides style default
  "style": "tech" | "scientific" | "artistic" | "business",  ← v3 NEW
  "slides": Slide[]
}
```

---

## Visual Styles (v3)

Each style applies a decorative background layer and picks a matching default theme.

| Style | Auto Theme | Best For | Visual Character |
|-------|-----------|---------|-----------------|
| `"tech"` | dark `#0B0F14` | AI, startup, developer tools, SaaS | Dot-matrix grid · indigo corner brackets · scan lines |
| `"scientific"` | light `#FAFAFA` | Research, data analysis, academic | Graph grid · blue crosshair marker · axis tick points |
| `"artistic"` | brand `#0F0A1E` | Creative, design, portfolio, brand | Large overlapping color circles · diagonal brush strokes · amber triangle |
| `"business"` | light `#FAFAFA` | Corporate pitch, report, consulting | Blue left accent bar · diagonal corner triangle · professional |

**Rules:**
- Always set `style`. It is the primary visual choice.
- `theme` is optional — omit it and the renderer picks the right default automatically.
- Override `theme` only when you intentionally want an unusual combination (e.g. dark business deck).

---

## Themes (color palette override)

| Theme | Background | When to override |
|-------|-----------|-----------------|
| `"dark"` | #0B0F14 navy | Tech/startup with dark bg |
| `"light"` | #FAFAFA white | Clean, readable, academic |
| `"brand"` | #0F0A1E purple | Bold, expressive, creative |

---

## Slide Layouts

### `"hero"` — Full-bleed opening slide
```json
{
  "layout": "hero",
  "badge": "optional label",
  "title": "Main Title",
  "subtitle": "Supporting line",
  "note": "optional footnote"
}
```

### `"content"` — Title + card grid or bullets
```json
{
  "layout": "content",
  "title": "Section Title",
  "subtitle": "optional subline",
  "items": [
    { "icon": "cpu", "title": "Card Title", "desc": "Description text" }
  ]
}
```
Or with bullets (when items are not available):
```json
{
  "layout": "content",
  "title": "Title",
  "bullets": ["Point one", "Point two", "Point three"]
}
```

**Icons:** `cpu` · `shield` · `zap` · `brain` · `rocket` · `globe` · `code` · `chart` · `users` · `lock` · `check` · `star` · `target` · `layers`

### `"two-column"` — Side-by-side layout
```json
{
  "layout": "two-column",
  "title": "Comparison",
  "left":  { "heading": "Before", "bullets": ["Item A", "Item B"], "badge": "old" },
  "right": { "heading": "After",  "bullets": ["Item C", "Item D"], "badge": "new" }
}
```

### `"comparison"` — Sentiment-colored panels
```json
{
  "layout": "comparison",
  "title": "Pros vs Cons",
  "left":  { "label": "Advantages", "sentiment": "positive", "points": ["Fast", "Cheap"] },
  "right": { "label": "Drawbacks",  "sentiment": "negative", "points": ["Complex", "New"] }
}
```
`sentiment`: `"positive"` (emerald) · `"negative"` (rose) · `"neutral"`

### `"metrics"` — Big numbers
```json
{
  "layout": "metrics",
  "title": "Key Results",
  "subtitle": "Q4 2024",
  "metrics": [
    { "value": "42%", "label": "Growth", "trend": "up", "desc": "YoY" },
    { "value": "3.2×", "label": "ROI",   "trend": "up" },
    { "value": "$1.2B", "label": "ARR",  "trend": "neutral" }
  ]
}
```
`trend`: `"up"` · `"down"` · `"neutral"`

### `"timeline"` — Roadmap / phases
```json
{
  "layout": "timeline",
  "title": "Project Roadmap",
  "events": [
    { "marker": "Q1 2025", "title": "Phase 1", "desc": "Foundation", "done": true },
    { "marker": "Q2 2025", "title": "Phase 2", "desc": "Launch",     "done": false }
  ]
}
```

### `"quote"` — Pull quote
```json
{
  "layout": "quote",
  "quote": "The best way to predict the future is to invent it.",
  "author": "Alan Kay",
  "role": "Computer Scientist"
}
```

### `"cta"` — Closing call-to-action
```json
{
  "layout": "cta",
  "title": "Ready to Start?",
  "subtitle": "Join 10,000+ teams already using it",
  "action": "Get Started Free"
}
```

---

## Design Principles

1. **Open with `hero`** — always start with a full-bleed title slide.
2. **Vary layouts** — never use the same layout 3+ times in a row. Mix metrics, comparison, timeline.
3. **Use `items` in `content`** — prefer card grid over plain bullets when listing features/concepts.
4. **Close with `cta`** — always end with a call-to-action or summary slide.
5. **8–14 slides** is the ideal deck length unless the user specifies otherwise.
6. **Pick `style` based on topic** — tech for software, scientific for research, artistic for creative, business for corporate.

---

## Full Example — Tech Style

````
```pptx artifact title="AI Agent Platform"
{
  "title": "AI Agent Platform",
  "style": "tech",
  "slides": [
    {
      "layout": "hero",
      "badge": "Product Overview",
      "title": "AI Agent Platform",
      "subtitle": "Autonomous agents that get work done"
    },
    {
      "layout": "content",
      "title": "Core Capabilities",
      "items": [
        { "icon": "brain",  "title": "Multi-Agent",   "desc": "Coordinate swarms of specialized agents" },
        { "icon": "code",   "title": "Code Execution", "desc": "Write, run, and debug code autonomously" },
        { "icon": "globe",  "title": "Web Access",    "desc": "Browse, search, and extract live data" },
        { "icon": "shield", "title": "Safe by Design","desc": "Guardrails and human-in-the-loop controls" }
      ]
    },
    {
      "layout": "metrics",
      "title": "Platform Performance",
      "metrics": [
        { "value": "10×", "label": "Faster than manual", "trend": "up" },
        { "value": "99.9%", "label": "Uptime SLA",       "trend": "up" },
        { "value": "500+", "label": "Integrations",      "trend": "neutral" }
      ]
    },
    {
      "layout": "timeline",
      "title": "Roadmap",
      "events": [
        { "marker": "Q1", "title": "Core Agents",   "done": true  },
        { "marker": "Q2", "title": "Memory Layer",  "done": true  },
        { "marker": "Q3", "title": "Multi-Modal",   "done": false },
        { "marker": "Q4", "title": "Enterprise GA", "done": false }
      ]
    },
    {
      "layout": "cta",
      "title": "Start Building Today",
      "subtitle": "Free tier — no credit card required",
      "action": "Get Early Access"
    }
  ]
}
```
````

---

## Full Example — Scientific Style

````
```pptx artifact title="Climate Research Summary"
{
  "title": "Climate Research Summary",
  "style": "scientific",
  "slides": [
    {
      "layout": "hero",
      "badge": "2024 Annual Report",
      "title": "Climate Change Indicators",
      "subtitle": "Data-driven analysis of global trends"
    },
    {
      "layout": "metrics",
      "title": "Key Measurements",
      "subtitle": "Global averages — 2024",
      "metrics": [
        { "value": "+1.4°C", "label": "Avg. temp rise",    "trend": "up",   "desc": "vs. pre-industrial" },
        { "value": "422ppm", "label": "CO₂ concentration", "trend": "up",   "desc": "Mauna Loa station"  },
        { "value": "-13%",   "label": "Arctic sea ice",    "trend": "down", "desc": "per decade"         }
      ]
    },
    {
      "layout": "comparison",
      "title": "Mitigation Strategies",
      "left":  { "label": "High Impact", "sentiment": "positive", "points": ["Renewable energy", "Reforestation", "Carbon capture"] },
      "right": { "label": "Low Impact",  "sentiment": "negative", "points": ["Recycling alone", "Minor efficiency gains"] }
    },
    {
      "layout": "cta",
      "title": "Action Required Now",
      "subtitle": "Limiting warming to 1.5°C requires immediate systemic change",
      "action": "Read Full Report"
    }
  ]
}
```
````
