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

**当前版本：** v7.2.0  
**导入 URL：**
```
https://github.com/orchidlemon/skill_mulAgent/blob/main/pptx-maker/SKILL.md
```

生成 Keynote/TED/Linear 风格的网页原生幻灯片。AI 运行完整 8 层创意流水线，输出结构化 JSON，由 Multica 渲染引擎实时渲染为 16:9 幻灯片。

| 功能 | 说明 |
|------|------|
| 12 种布局族 | hero_statement / split_argument / evidence_board / timeline_flow / process_flow / architecture_map / matrix_compare / quote_focus / dense_report / card_cluster / image_caption / before_after |
| 5 种视觉风格 | tech / scientific / artistic / business / linear |
| 叙事导演系统 | 研究协议 → 叙事张力 → 场景语法 → 视觉导演 → 内容压缩 |
| Validation + Repair Pipeline | 生成 → 验证 → 修复 → 渲染，所有规则编译为可执行约束 |

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

| 日期 | 版本 | 变更摘要 |
|------|------|---------|
| 2026-05-29 | pptx-maker **v7.2.0** | Generate→Validate→Repair→Render 可执行流水线；5-pass validateAndRepair()；render-time 字体硬上限（60px）；LAYER 8 Renderer Guarantee |
| 2026-05-29 | pptx-maker **v7.1.0** | LAYER 7 Presentation Restraint；Typography Governance 字体规范；Slide Intensity Curve；Layout Capacity Validation；Dominant Element Enforcement |
| 2026-05-29 | pptx-maker **v7.0.0** | 12 种布局族（layout_family）；content-fit 内容适配规则；5 个新结构视图（DenseReport/MatrixCompare/ProcessFlow/SplitArgument/CardCluster）；layout_family 优先路由；LAYER 6 Content-Fit Rules |
| 2026-05-29 | pptx-maker **v6.3.0** | dominant_element 支柱层级；SourceAttribution 来源引用条；mkSurface 语义表面规则 |
| 2026-05-29 | pptx-maker **v6.2.0** | STORYBOARD 步骤强制写入 JSON；layout_intent 结构路由表（5 种命名值）；focus:flow 新增；EvidenceBoardView / HeroStatementView / BreathingPauseView / ArchitectureMapView / NarrativePivotView 5 个新视图 |
| 2026-05-29 | pptx-maker **v6.1.0** | 显式导演字段（visual_weight / density / focus）必填；Visual Weight Engine 更新；content_length 内容长度字段 |
| 2026-05-29 | pptx-maker **v6.0.0** | Runtime Intelligence：EmotionType（7 种情绪）；所有 slide 继承 BaseSlide；emotion → 动效预设 + 视觉权重 |
| 2026-05-28 | pptx-maker **v5.1.0** | Narrative Tension System；Scene Emotions（情绪驱动渲染）；Research-Driven Story Rewrite；Visual Weight Logic |
| 2026-05-27 | pptx-maker **v5.0.0** | Research Protocol（Layer 0）；Scene Grammar（scene_type 8 种）；Visual Director（Style DNA + 内容压缩） |
| 2026-05-27 | pptx-maker **v4.0.0** | Director OS：5 种新布局（insight / editorial / big-stat / architecture / narrative）；linear 风格预设 |
| 2026-05-27 | html-designer **v1.0.0** | 发布 HTML 页面设计 skill，4 种视觉风格预设 |
| 2026-05-27 | pptx-maker **v3.0.1** | 新增 AUTO-ACTIVATE 中英文触发词规则 |
| 2026-05-27 | system-prompts **v1.1** | multica-assistant 通用系统提示词 |
| 2026-05-26 | pptx-maker **v3.0.0** | 4 种视觉风格预设（tech/scientific/artistic/business）+ 装饰背景层 |
| 2026-05-26 | pptx-maker **v2.0.0** | 8 种布局（hero/content/two-column/comparison/metrics/timeline/quote/cta）；dark theme |
| 2026-05-25 | pptx-maker **v1.0.0** | 初始发布，4 种基础布局 |
