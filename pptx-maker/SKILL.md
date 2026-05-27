---
name: pptx-maker
description: Generate high-end web-native slide decks (Gamma/Manus style). Use when asked to "make slides", "create a presentation", "做PPT", "做幻灯片", "制作演示文稿", or "做一个demo".
metadata:
  author: orchidlemon
  version: "2.0.0"
  argument-hint: <topic or description>
---

# Slides Maker — Reveal Runtime

You generate **web-native slide decks** rendered directly in the browser (Gamma / Manus style) — not PowerPoint files. Output is a JSON schema that drives a high-end React slides renderer with smooth transitions and modern design.

---

## Output format (REQUIRED)

Always wrap output in a `pptx artifact` code fence. Never output HTML, markdown, or .pptx files.

```pptx artifact title="<presentation title>"
{
  "title": "...",
  "theme": "dark",
  "slides": [...]
}
```

---

## Schema

```
{
  "title": string,
  "theme": "dark" | "light" | "brand",
  "slides": Slide[]
}
```

### Theme

| Theme   | When to use                        | Background    |
|---------|------------------------------------|---------------|
| "dark"  | Tech, AI, startup — DEFAULT        | #0B0F14 navy  |
| "light" | Business, academic, report         | #FAFAFA white |
| "brand" | Product launch, keynote            | Gradient      |

---

## Slide Layouts

### hero — Opening impact slide

```json
{
  "layout": "hero",
  "badge": "v2.0",
  "title": "Multi-Agent Collaboration",
  "subtitle": "Memory-driven orchestration at scale",
  "note": "Internal demo · May 2026"
}
```

Fields: badge (optional pill label), title (max 8 words), subtitle (max 15 words), note (small footnote)

---

### content — Title + cards or bullets

Card grid (for features/capabilities):
```json
{
  "layout": "content",
  "title": "Core Capabilities",
  "subtitle": "What makes it different",
  "items": [
    { "icon": "cpu",    "title": "Fast",    "desc": "Sub-100ms latency" },
    { "icon": "shield", "title": "Secure",  "desc": "End-to-end encrypted" },
    { "icon": "zap",    "title": "Scalable","desc": "10k concurrent agents" }
  ]
}
```

Bullet list (for steps/explanations):
```json
{
  "layout": "content",
  "title": "How It Works",
  "bullets": [
    "Agent receives task from workspace",
    "Retrieves relevant memory chunks",
    "Executes with tool access"
  ]
}
```

Available icon values: cpu, shield, zap, brain, rocket, globe, code, chart, users, lock, check, star, target, layers, box, git

---

### comparison — Before vs After

```json
{
  "layout": "comparison",
  "title": "Before vs After",
  "left": {
    "label": "Traditional Approach",
    "sentiment": "negative",
    "points": ["Manual task routing", "No memory", "Single-agent bottleneck"]
  },
  "right": {
    "label": "With Multi-Agent",
    "sentiment": "positive",
    "points": ["Auto parallel routing", "Persistent memory", "Infinite scale"]
  }
}
```

sentiment: "positive" (green) | "negative" (red) | "neutral" (default)

---

### metrics — Big numbers

```json
{
  "layout": "metrics",
  "title": "Results After 30 Days",
  "subtitle": "Production deployment across 3 accounts",
  "metrics": [
    { "value": "47%",   "label": "Faster task completion", "trend": "up" },
    { "value": "3.2x",  "label": "Throughput increase",    "trend": "up" },
    { "value": "$2.4M", "label": "Cost saved annually",    "trend": "up" }
  ]
}
```

trend: "up" (green arrow) | "down" (red arrow) | "neutral" (no indicator)

---

### timeline — Roadmap / phases

```json
{
  "layout": "timeline",
  "title": "Product Roadmap",
  "events": [
    { "marker": "Q1 2025", "title": "Foundation",  "desc": "Core runtime",   "done": true  },
    { "marker": "Q2 2025", "title": "Memory",      "desc": "Persistent ctx", "done": true  },
    { "marker": "Q3 2025", "title": "Multi-Agent", "desc": "Orchestration",  "done": false }
  ]
}
```

---

### two-column — Side by side

```json
{
  "layout": "two-column",
  "title": "Architecture",
  "left":  { "heading": "Frontend", "bullets": ["React", "WebSocket", "Artifacts"] },
  "right": { "heading": "Backend",  "bullets": ["Go API", "PostgreSQL", "Daemon"] }
}
```

---

### quote — Pull quote / testimonial

```json
{
  "layout": "quote",
  "quote": "The best interface is no interface. The agent should just know.",
  "author": "Sam Chen",
  "role": "CTO, Acme Corp"
}
```

---

### cta — Closing call to action

```json
{
  "layout": "cta",
  "title": "Ready to get started?",
  "subtitle": "Join 500+ teams already using multi-agent workflows",
  "action": "Start free trial →"
}
```

---

## Composition Rules

1. Always start with "hero" — punchy title, one supporting line
2. One idea per slide — more than 4 bullets → split into two slides
3. Use "metrics" for proof — numbers beat words every time
4. Use "comparison" for selling — show the pain, then the solution
5. End with "cta" — one clear next step
6. Sweet spot: 6–12 slides
7. Titles are takeaways, not topics: "Revenue grew 47%" not "Revenue"
8. Dark theme by default

---

## Full Example

```pptx artifact title="AI Agent Platform Demo"
{
  "title": "AI Agent Platform Demo",
  "theme": "dark",
  "slides": [
    {
      "layout": "hero",
      "badge": "Internal Demo",
      "title": "AI Agents as Real Teammates",
      "subtitle": "Assign issues, review PRs, and ship features autonomously",
      "note": "Multica Platform · May 2026"
    },
    {
      "layout": "content",
      "title": "The Problem",
      "bullets": [
        "AI tools are isolated with no memory or collaboration",
        "Every task starts from scratch",
        "Developers spend 40% of time on coordination"
      ]
    },
    {
      "layout": "comparison",
      "title": "Old Way vs New Way",
      "left": {
        "label": "Without Agents",
        "sentiment": "negative",
        "points": ["Manual routing", "Lost context", "One tool at a time"]
      },
      "right": {
        "label": "With Multica",
        "sentiment": "positive",
        "points": ["Auto-assigned", "Memory graph", "Multi-agent parallel"]
      }
    },
    {
      "layout": "content",
      "title": "Core Capabilities",
      "items": [
        { "icon": "brain",  "title": "Memory",       "desc": "Agents remember across sessions" },
        { "icon": "users",  "title": "Collaboration", "desc": "Multiple agents, one task" },
        { "icon": "code",   "title": "Code Actions",  "desc": "Write, review, deploy" },
        { "icon": "shield", "title": "Guardrails",    "desc": "Human-in-the-loop approvals" }
      ]
    },
    {
      "layout": "metrics",
      "title": "Early Results",
      "subtitle": "30-day pilot across 5 engineering teams",
      "metrics": [
        { "value": "3x",  "label": "Faster issue resolution", "trend": "up" },
        { "value": "68%", "label": "Less context switching",  "trend": "up" },
        { "value": "12h", "label": "Saved per dev per week",  "trend": "up" }
      ]
    },
    {
      "layout": "cta",
      "title": "Let us build the future of work together",
      "subtitle": "Request access to the private beta",
      "action": "Get early access →"
    }
  ]
}
```
