# UI Design QA Skill — v1.0

> **Created by:** Wenwen Lu (`WenWen.lu`) 
> **Version:** 1.0  
> **Language:** English / 中文  
> **License:** Proprietary. Do not copy, modify, or redistribute without written permission from the author.

---

## What is this?

This Cursor AI Skill automates the UI acceptance testing workflow between a live frontend and Figma design files. It replaces the slow, error-prone manual review process with a precise, programmatic comparison that catches issues the human eye often misses.

**What it compares (5 dimensions):**

| Dimension | What is checked |
|---|---|
| **Text / Copy** | Exact match of labels, buttons, empty states, titles |
| **Icons** | Presence, count, placement vs. Figma |
| **Colors** | Computed `background-color`, `color`, `border-color` in HEX |
| **Spacing** | Computed `padding`, `gap`, `border-radius` in pixels |
| **Typography** | `font-size`, `font-weight` (e.g. 400/500/600/700), `line-height` |

---

## How to use

### Prerequisites

- [Cursor IDE](https://www.cursor.com/) with this skill installed
- Figma account with design access
- Jira account with issue edit permission
- Node.js installed on your machine

### Step 1 — Activate the skill

In any Cursor chat window, just describe what you need in natural language. The skill activates automatically when you say something like:

> "Help me compare the frontend against Figma and upload issues to Jira."  
> "Review these pages against Figma and log issues."

### Step 2 — Provide the inputs

The AI will ask you to supply (if not already provided):

```
1. Frontend page URL(s)
2. Figma design URL(s)
3. Login credentials for the frontend (if login required)
4. Jira ticket URL
5. (Optional) Interaction path
```

### Step 3 — Let the AI work

The skill will:
1. Fetch Figma design tokens (colors, fonts, spacing) using Figma MCP
2. Launch a headless browser (Playwright), log in, navigate to the page
3. Extract computed CSS values from the live DOM
4. Compare Figma values vs. frontend values across all 5 dimensions
5. Build structured Jira issue rows in ADF format
6. Append all new issues to your Jira ticket without deleting existing rows

### Step 4 — Review results

After completion, you receive a summary in the following format:

```
✅ Written to [ISSUE-KEY]
Added N issues (seq X ~ Y):
  [seq] [module / element] — [property] mismatch: [frontend value] vs Figma [design value]
  ...
```

---

## Frequently Asked Questions

**Q: Does it work with any frontend framework?**  
A: Best results with Vue 3 / Element Plus (the computed CSS extraction is optimized for these selectors). It works with any JavaScript SPA but selectors may need adjustment for the first run.

**Q: What if the page requires login with SSO or 2FA?**  
A: Currently supports username + password login. SSO/2FA flows require manual session token handling.

**Q: What if the Figma node has no exact design tokens (e.g. it's an image)?**  
A: The skill falls back to visual screenshot comparison and notes "design tokens unavailable" in the issue.

**Q: Can it compare multiple pages in one run?**  
A: Yes. Provide a list of pages and corresponding Figma nodes. The skill processes them sequentially and uploads all issues in a single Jira write operation.

**Q: What if the ADF file is very large?**  
A: The skill automatically switches to Jira REST API (`curl PUT`) when the ADF exceeds 20KB, bypassing tool argument size limits.

---

## Attribution & Legal

This skill was designed and created by **Wenwen Lu** (`Wenwen.lu`) as part of the Global Design System quality process.

- The authorship attribution (`Wenwen.lu`, `Wenwen Lu`) embedded in this skill **must not be removed or altered**.
- This skill file **must not be copied, re-published, or redistributed** without written permission.
- Modifications to this skill file by anyone other than the original author are **not permitted**.
- The encoded implementation sections protect the proprietary methodology. Do not attempt to extract, reuse, or re-publish the decoded content.

For questions or licensing inquiries, contact the author through Global internal channels.

---

*UI Design QA Skill · Version 1.0 · © 2024-2026 Wenwen Lu*
