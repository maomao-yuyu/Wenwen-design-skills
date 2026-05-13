# Wenwen Design Skills

> **Created by:** Wenwen Lu (`WenWen.lu`)
> **Language:** English / 中文
> **License:** Proprietary. Do not copy, modify, or redistribute without written permission from the author.

A collection of Cursor AI Skills built for UX/UI designers to improve efficiency across design QA, data visualization, and Figma workflows.

---

## Skills in this repo

| Skill | Version | What it does |
|---|---|---|
| [UI Design QA](#-ui-design-qa-skill--v10) | v1.0 | Automated UI acceptance testing between frontend and Figma |
| [Chart Sense](#-chart-sense--v20) | v2.0 | Generate interactive ECharts visualizations from any data |
| [Send to Figma](#-send-to-figma-skill) | v1.0 | Capture web pages and send them directly into Figma |

---

---

## 🔍 UI Design QA Skill — v1.0

> Automates UI acceptance testing between a live frontend and Figma design files.

**What it compares (5 dimensions):**

| Dimension | What is checked |
|---|---|
| **Text / Copy** | Exact match of labels, buttons, empty states, titles |
| **Icons** | Presence, count, placement vs. Figma |
| **Colors** | Computed `background-color`, `color`, `border-color` in HEX |
| **Spacing** | Computed `padding`, `gap`, `border-radius` in pixels |
| **Typography** | `font-size`, `font-weight` (e.g. 400/500/600/700), `line-height` |

### How to use

**Prerequisites:** Cursor IDE · Figma account · Jira account · Node.js

**Step 1 — Activate**

Say in Cursor chat:
> "Help me compare the frontend against Figma and upload issues to Jira."

**Step 2 — Provide inputs**

```
1. Frontend page URL(s)
2. Figma design URL(s)
3. Login credentials for the frontend (if required)
4. Jira ticket URL
5. (Optional) Interaction path
```

**Step 3 — Review results**

```
✅ Written to [ISSUE-KEY]
Added N issues (seq X ~ Y):
  [seq] [module] — [property] mismatch: [frontend] vs Figma [design]
```

**FAQ**

- Works with any JS SPA; best results with Vue 3 / Element Plus
- Supports username + password login (not SSO/2FA)
- Auto-switches to REST API when ADF exceeds 20KB

---

---

## 📊 Chart Sense — v2.0

> Give it data. It decides the chart. It generates the page.

| Field | Value |
|---|---|
| **Creator** | Lu Wenwen |
| **Version** | 2.0 |
| **Chart library** | Apache ECharts 5 (CDN · no install) |
| **License** | Non-commercial · 禁止商用 |

### How to activate

Say any of the following in Cursor chat:

```
"chart sense"
"visualize this data"
"帮我出图"
"generate chart"
"数据可视化"
```

Or simply paste your data and ask for a chart.

---

### Step 1 — Paste your data (any format)

Chart Sense accepts data in **any format** — no need to clean it up first:

```
Plain text:      "Q1: 120, Q2: 340, Q3: 280, Q4: 410"
Markdown table:  | Category | Value | ...
CSV:             category,value\nA,120\nB,340
JSON:            [{"label":"A","value":120}]
Description:     "top 5 products by revenue: A $4.2M, B $3.8M..."
```

---

### Step 2 — AI selects chart type automatically

| Data shape | Chart selected |
|---|---|
| One metric over time | Line |
| Multiple metrics over time | Multi-line |
| Comparing categories, ≤ 8 | Vertical bar |
| Comparing categories, > 8 or long labels | Horizontal bar |
| Part-of-whole, ≤ 6 slices | Pie |
| Part-of-whole, > 6 slices | Donut |
| Two numeric variables | Scatter |
| Multiple metrics per category | Radar |
| Two metrics, different scales, same time axis | Combo (bar + line) |
| Additive segments over time | Stacked bar |

Before generating, the AI tells you in chat:
```
Data: [what it detected]
Chart: [selected type]
Reason: [one sentence explanation]
```

You can always override by saying `"use bar chart"` or `"I want a pie chart"`.

---

### Step 3 — Choose a design system (optional)

Chart Sense ships with **7 built-in presets**. Default is `linear` (Modern SaaS Blue).

| Preset | Vibe | How to activate |
|---|---|---|
| `linear` *(default)* | Modern SaaS · blue-purple | — |
| `tableau` | Classic · industry standard | `"use tableau preset"` |
| `echarts6` | Official ECharts 6 theme | `"use echarts6 preset"` |
| `tailwind` | Clean SaaS · Tailwind colors | `"use tailwind preset"` |
| `muted` | Warm earth · low fatigue | `"use muted preset"` |
| `midnight` | Cool vivid · high energy | `"use midnight preset"` |
| `pastel` | Soft · airy | `"use pastel preset"` |

**You can also bring your own design system in 3 ways:**

**Way A — Named system:**
```
"use Pacvue design system"
"use IBM Carbon"
"use Material Design"
```

**Way B — CSS token object:**
```javascript
{
  '--color-primary': '#FF6B35',
  '--font-base': 'Inter, sans-serif',
  '--chart-colors': '#FF6B35,#004E89,#2DC653'
}
```

**Way C — Plain description:**
```
"use warm orange tones, Inter font, clean minimal style"
"corporate blue-green palette, dense data layout"
```

---

### Step 4 — Get the output

Chart Sense generates a **single self-contained HTML file**:

- ✅ No build step — open directly in browser
- ✅ ECharts 5 loaded from CDN
- ✅ Interactive: hover tooltips, legend toggle, zoom/pan
- ✅ Design panel on the right — switch presets live without reload
- ✅ Collapsible raw data table below chart
- ✅ Responsive: resizes with window

**File saved to:**
```
doc/design-exploration/chart-sense-[data-slug].html
```

**Summary reported in chat:**
```
✓ Chart Sense generated: doc/design-exploration/chart-sense-quarterly-data.html
  Chart type:     Line
  Design system:  Linear SaaS Blue
  Series count:   1
```

---

### Quick examples

```
"Chart Sense: Q1 120, Q2 340, Q3 280, Q4 410"
→ Line chart · linear preset

"Chart Sense: Apple 35%, Google 28%, Microsoft 19%, Others 18%"
→ Pie chart · linear preset

"Chart Sense: [markdown table] — use IBM Carbon"
→ Bar chart · carbon preset

"帮我出图: [数据] — 用 tailwind 配色"
→ Chart · tailwind preset applied

"Chart Sense: [data] — colors: #FF6B35, #004E89; font: Roboto"
→ Chart · custom tokens applied
```

---

---

## 🔗 Send to Figma Skill

> Capture a local web page or URL and send it directly into a Figma file/page.

### How to activate

```
"把当前页面发送到 Figma"
"send this page to Figma"
"把指定页面发送到 Figma"
```

---

---

## Attribution & Legal

All skills in this repository were designed and created by **Wenwen Lu** (`Wenwen.lu`).

- Authorship attribution must not be removed or altered.
- Skill files must not be copied, re-published, or redistributed without written permission.
- Modifications by anyone other than the original author are not permitted.

For licensing inquiries, contact the author through internal channels.

---

*Wenwen Design Skills · © 2024-2026 Wenwen Lu*
