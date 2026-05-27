---
name: pptx-maker
description: Generate downloadable PowerPoint presentations (.pptx) with structured JSON. Use when asked to "make a PPT", "create slides", "做PPT", "做幻灯片", or "制作演示文稿".
metadata:
  author: multica-local
  version: "1.0.0"
  argument-hint: <topic or description>
---

# PPT Maker Skill

You generate PowerPoint presentations. Output is a structured JSON artifact that renders as an interactive slide preview with a one-click `.pptx` download.

## ⚠️ Critical: Output format

**Always** wrap your output in a `pptx` artifact code fence. Never output HTML, CSS, or plain markdown for presentations.

````
```pptx artifact title="<presentation title>"
{
  "title": "Presentation title",
  "theme": "light",
  "slides": [...]
}
```
````

## Schema

```
{
  "title": string,
  "theme": "light" | "dark" | "blue",
  "slides": Slide[]
}
```

### Slide layouts

**Title slide** — opening slide with large centered title:
```json
{ "layout": "title", "title": "string", "subtitle": "string (optional)" }
```

**Content slide** — title + bullet list:
```json
{ "layout": "content", "title": "string", "bullets": ["point 1", "point 2"] }
```
Or with free text instead of bullets:
```json
{ "layout": "content", "title": "string", "text": "paragraph text" }
```

**Two-column slide** — side-by-side comparison:
```json
{
  "layout": "two-column",
  "title": "string",
  "left":  { "heading": "optional", "bullets": ["..."] },
  "right": { "heading": "optional", "bullets": ["..."] }
}
```

**Blank slide** — free-form text:
```json
{ "layout": "blank", "title": "optional", "text": "optional" }
```

## Theme guide

| Theme | Best for |
|-------|----------|
| `"light"` | General use, business, academic |
| `"dark"` | Tech, startup, modern brand |
| `"blue"` | Formal, enterprise, government |

## Presentation principles

1. **Open with `title` layout** — large title + subtitle.
2. **One idea per slide** — if a slide has more than 5 bullets, split it into two.
3. **Bullets are short phrases** (3–8 words), not sentences.
4. **Use `two-column` for comparisons** — before/after, pros/cons, feature vs benefit.
5. **Close with a clear next step** — question, decision, or call to action.
6. **8–15 slides** is the sweet spot unless specified otherwise.

## Full example

````
```pptx artifact title="心理类型简介"
{
  "title": "心理类型简介",
  "theme": "light",
  "slides": [
    {
      "layout": "title",
      "title": "心理类型简介",
      "subtitle": "了解自己，理解他人"
    },
    {
      "layout": "content",
      "title": "什么是心理类型？",
      "bullets": [
        "心理类型描述人们感知世界和做决策的偏好模式",
        "最广为人知的框架：MBTI（迈尔斯-布里格斯类型指标）",
        "16种类型，由4个维度组合而成",
        "类型不是标签，而是理解自我的工具"
      ]
    },
    {
      "layout": "two-column",
      "title": "四个核心维度",
      "left": {
        "heading": "能量来源 & 信息获取",
        "bullets": ["外向 (E) vs 内向 (I)", "实感 (S) vs 直觉 (N)"]
      },
      "right": {
        "heading": "决策方式 & 生活态度",
        "bullets": ["思考 (T) vs 情感 (F)", "判断 (J) vs 感知 (P)"]
      }
    },
    {
      "layout": "content",
      "title": "为什么心理类型有用？",
      "bullets": [
        "提升自我认知：了解自己的优势和盲点",
        "改善沟通：理解他人为何做出不同选择",
        "团队协作：发挥每种类型的独特价值",
        "职业规划：找到与天性契合的工作方向"
      ]
    },
    {
      "layout": "blank",
      "title": "下一步",
      "text": "进行你的心理类型测评，开始认识真实的自己。"
    }
  ]
}
```
````
