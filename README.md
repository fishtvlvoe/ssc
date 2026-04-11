# SSC — Super Skills Creator

> 為 Claude Code 建立 Skill / Agent / Hook 的完整流程框架  
> A complete workflow framework for creating Skills, Agents, and Hooks in Claude Code

---

## 目錄 / Table of Contents

- [中文說明](#中文說明)
- [English Guide](#english-guide)
- [架構 / Architecture](#架構--architecture)
- [安裝 / Installation](#安裝--installation)

---

## 中文說明

### 這是什麼？

SSC 是一個互動式的 Claude Code Skill，幫你建立、轉換、或升級 **Skill / Agent / Hook**，走完整的「世代 3」品質流程。

你說出需求，SSC 帶你走完：

```
GATE 確認方向 → 分類判斷 → 訪談收集資訊 → 產出結構 → 品質檢查
```

### 使用方式

在 Claude Code 中輸入：

```
/ssc
```

或直接描述需求，觸發詞包括：

```
建 Skill、做 Agent、加 Hook、升級這個 Skill
```

### 三種模式

| 模式 | 說明 |
|------|------|
| **新建** | 從零打造一個 Skill / Agent / Hook |
| **轉換** | 把別人的 Skill 改造成我們的結構 |
| **升級** | 把現有世代 1/2 升級到世代 3 |

### 三種產出類型

| 類型 | 定義 | 適用場景 | 存放位置 |
|------|------|---------|---------|
| **Skill** | 互動式工作流 | 需要來回確認（寫計畫、除錯、設計） | `~/.claude/skills/<name>/` |
| **Agent** | 獨立執行的專家 | 丟進去就能做完（Code Review、分析） | `~/.claude/agents/<name>.md` |
| **Hook** | 事件觸發的自動化 | Session 開始、工具執行前後的自動操作 | `~/.claude/settings.json` |

### 分類判斷邏輯

```
問題 1：需要跟用戶來回對話嗎？
│
├── 是 → Skill
│
└── 否 → 問題 2：需要 AI 思考嗎？
            │
            ├── 是 → Agent
            │
            └── 否 → Hook
```

### 世代 3 品質標準（5 項必備）

每個產出的 Skill 都必須包含這 5 個元件：

| # | 元件 | 說明 |
|---|------|------|
| 1 | `disable-model-invocation: true` | 直接執行 SKILL.md，不多呼叫一次 Claude 解讀 |
| 2 | GATE 對焦 | 複述理解 → 確認方向 → 用戶 OK 才往下 |
| 3 | 強制停止點 | 至少 1 個等用戶確認的節點 |
| 4 | 品質檢查機制 | 依用途選對應類型（寫作／開發／部署／分析／工具） |
| 5 | 完成條件 Checklist | Checkbox 清單，全部打勾才算完成 |

---

## English Guide

### What is SSC?

SSC is an interactive Claude Code Skill that helps you **build, convert, or upgrade** Skills, Agents, and Hooks — following the complete "Generation 3" quality process.

Describe what you need. SSC walks you through:

```
GATE alignment → Classification → Interview → Generate structure → Quality check
```

### Usage

In Claude Code, type:

```
/ssc
```

Or describe your need directly. Trigger phrases include:

```
build skill, create agent, add hook, upgrade this skill
```

### Three Modes

| Mode | Description |
|------|-------------|
| **New** | Build from scratch |
| **Convert** | Adapt someone else's Skill into our structure |
| **Upgrade** | Bring a Gen 1/2 Skill up to Gen 3 standard |

### Three Output Types

| Type | Definition | Use When | Location |
|------|-----------|---------|---------|
| **Skill** | Interactive workflow | Back-and-forth needed (planning, debugging, design) | `~/.claude/skills/<name>/` |
| **Agent** | Self-contained expert | Fire-and-forget (code review, analysis) | `~/.claude/agents/<name>.md` |
| **Hook** | Event-driven automation | Auto-actions on session/tool events | `~/.claude/settings.json` |

### Classification Logic

```
Q1: Does it need back-and-forth with the user?
│
├── Yes → Skill
│
└── No → Q2: Does it need AI reasoning?
            │
            ├── Yes → Agent
            │
            └── No → Hook
```

### Generation 3 Quality Standard (5 Required)

| # | Component | What it does |
|---|-----------|-------------|
| 1 | `disable-model-invocation: true` | Runs SKILL.md directly, skips redundant Claude interpretation call |
| 2 | GATE alignment | Restate → Confirm → Proceed only on OK |
| 3 | Hard stop points | At least 1 user confirmation gate in the flow |
| 4 | Quality check | Type-matched verification (writing/dev/deploy/analysis/tool) |
| 5 | Completion checklist | All checkboxes must be ticked before done |

---

## 架構 / Architecture

```
ssc/
├── SKILL.md              ← 主流程骨架（< 100 行）/ Main workflow skeleton
└── knowledge/            ← 按需載入的參考資料 / On-demand reference docs
    ├── classification.md ← 分類決策樹 / Classification decision tree
    ├── templates.md      ← Skill / Agent / Hook 模板 / Output templates
    └── quality-check.md  ← 品質驗證規格 / Quality validation specs
```

### 設計原則 / Design Principles

- **< 100 行主骨架**：SKILL.md 只放流程，大段參考資料拆到 `knowledge/`，每個步驟只在用到時才讀，不一次全載
- **GATE 強制對焦**：每次任務必須先複述理解、確認方向，避免方向跑偏後才發現
- **強制委派**：讀 3+ 檔 → Kimi/Haiku；寫檔 → Haiku 子代理；主對話只做確認方向、決定結構、核查輸出

---

## 安裝 / Installation

```bash
# Clone 到 skills 目錄 / Clone into skills directory
cd ~/.claude/skills
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

重啟 Claude Code 後即可使用 `/ssc`。  
Restart Claude Code, then use `/ssc`.

---

*Built with [Claude Code](https://claude.ai/code) · by [@fishtvlvoe](https://github.com/fishtvlvoe)*
