# skill_mulAgent

Multica AI 助手的 Skills 与系统提示词集合。

## 目录结构

```
skill_mulAgent/
├── pptx-maker/          # 幻灯片生成 skill（Gamma/Manus 风格）
│   └── SKILL.md
├── html-designer/       # 网页设计 skill（4 种视觉风格）
│   └── SKILL.md
├── system-prompts/      # 智能体系统提示词
│   └── multica-assistant.md
└── archive/             # 历史版本存档
    └── pptx-maker-v2.0.0/
```

---

## Skills

### pptx-maker — 幻灯片生成

**当前版本：** v3.0.1  
**导入 URL：**
```
https://github.com/orchidlemon/skill_mulAgent/blob/main/pptx-maker/SKILL.md
```

生成 Gamma/Manus 风格的网页原生幻灯片，支持 4 种视觉风格预设：

| Style | 适用场景 |
|-------|---------|
| `tech` | AI、软件、SaaS、开发工具 |
| `scientific` | 学术研究、数据分析、理工科 |
| `artistic` | 创意、设计、心理、文化 |
| `business` | 企业汇报、咨询、产品 |

---

### html-designer — 网页设计

**当前版本：** v1.0.0  
**导入 URL：**
```
https://github.com/orchidlemon/skill_mulAgent/blob/main/html-designer/SKILL.md
```

生成完整可运行的 HTML 页面，支持 4 种视觉风格预设：

| Style | 适用场景 | 视觉语言 |
|-------|---------|---------|
| `tech` | AI、软件、编程、SaaS | 深色 `#0B0F14`，靛蓝点阵，渐变边框，辉光 |
| `scientific` | 学术、研究、数据、理工科 | 白色底，方格纸背景，蓝色数据，衬线标题 |
| `artistic` | 创意、设计、心理、文化 | 深紫 `#0F0A1E`，色彩光晕，磨砂玻璃卡片 |
| `business` | 企业、汇报、咨询、商业 | 纯白底，藏蓝顶部色条，KPI 卡片，专业 |

---

## System Prompts

### multica-assistant — Multica 通用助手

**文件：** [`system-prompts/multica-assistant.md`](system-prompts/multica-assistant.md)

配套上述两个 skill 使用，内含：
- pptx-maker 自动触发规则（中英文触发词）
- html-designer 自动触发规则（中英文触发词）
- 两个 skill 的优先级决策规则

**使用方式：** Settings → Agents → Edit System Prompt → 粘贴文件中 `---BEGIN---` 至 `---END---` 之间的内容。

---

## Changelog

| 日期 | 变更 |
|------|------|
| 2026-05-27 | html-designer v1.0.0 发布 |
| 2026-05-27 | pptx-maker v3.0.1 — 新增 AUTO-ACTIVATE 规则 |
| 2026-05-27 | system-prompts/multica-assistant.md v1.1 |
| 2026-05-26 | pptx-maker v3.0.0 — 新增 4 种视觉风格预设 |
| 2026-05-26 | pptx-maker v2.0.0 存档 |
