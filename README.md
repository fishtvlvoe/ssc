# SSC — Super Skill Creator

> 為 Claude Code 設計的 Skill/Agent/Hook 工廠  
> A Skill/Agent/Hook factory built for Claude Code

---

## 目錄 / Table of Contents

- [中文說明](#中文說明)
- [English Guide](#english-guide)
- [架構設計 / Architecture](#架構設計--architecture)
- [安裝 / Installation](#安裝--installation)

---

## 中文說明

### 這是什麼？

SSC（Super Skill Creator）是一個幫你為 **Claude Code** 打造 Skill、Agent 和 Hook 的互動式工廠。

你只要說出你想做什麼，SSC 會：
1. 確認你的需求方向
2. 判斷該做 Skill、Agent 還是 Hook
3. 透過訪談收集資訊
4. 自動產出符合「世代 3」標準的完整結構
5. 執行品質檢查，確保產出可直接使用

### 快速開始

安裝完成後，在 Claude Code 中輸入：

```
/ssc
```

或直接描述你的需求：

```
幫我建一個 code review 的 Skill
把這個 Skill 升級到世代 3
我要做一個 session 開始自動載入記憶的 Hook
```

### 核心流程（世代 3 標準）

```
用戶描述需求
    │
    ▼
GATE 強制對焦（複述 → 確認 → OK 才繼續）
    │
    ▼
分類判斷（Skill / Agent / Hook）
    │
    ▼
訪談收集資訊
    │
    ▼
產出完整結構
    │
    ▼
品質檢查（5 項必備元件）
    │
    ▼
寫入檔案（完成）
```

### 三種產出類型

| 類型 | 一句話定義 | 適用場景 | 存放位置 |
|------|-----------|---------|---------|
| **Skill** | 互動式工作流 | 需要來回確認的任務（寫計畫、除錯、設計） | `~/.claude/skills/<name>/` |
| **Agent** | 獨立執行的專家 | 丟進去就能做完的任務（Code Review、分析） | `~/.claude/agents/<name>.md` |
| **Hook** | 事件觸發的自動化 | Session 開始、工具執行前後的自動操作 | `~/.claude/settings.json` |

### 判斷依據

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

### 品質標準（世代 3 完整性 5 項必備）

每個產出的 Skill 都必須包含：

| # | 元件 | 說明 |
|---|------|------|
| 1 | `disable-model-invocation: true` | 防止重複呼叫 |
| 2 | GATE 對焦 | 複述 → 確認 → OK 才往下 |
| 3 | 強制停止點 | 至少 1 個等用戶確認 |
| 4 | 品質檢查機制 | 依用途選擇對應類型 |
| 5 | 完成條件 Checklist | Checkbox 清單供核對 |

---

## English Guide

### What is SSC?

SSC (Super Skill Creator) is an **interactive factory** for building Claude Code Skills, Agents, and Hooks.

Just describe what you want to build. SSC will:
1. Confirm your intent (GATE)
2. Classify the right type: Skill, Agent, or Hook
3. Interview you for key details
4. Generate a complete "Generation 3" compliant structure
5. Run quality checks before writing files

### Quick Start

After installation, type in Claude Code:

```
/ssc
```

Or describe your need directly:

```
Build me a code review Skill
Upgrade this Skill to Generation 3
Create a Hook that loads memory at session start
```

### Three Output Types

| Type | Definition | Use When | Location |
|------|-----------|---------|---------|
| **Skill** | Interactive workflow | Task needs back-and-forth with user | `~/.claude/skills/<name>/` |
| **Agent** | Self-contained expert | Fire-and-forget tasks (analysis, review) | `~/.claude/agents/<name>.md` |
| **Hook** | Event-driven automation | Auto-actions on session events | `~/.claude/settings.json` |

### Classification Logic

```
Q1: Does it need back-and-forth conversation?
│
├── Yes → Skill
│
└── No → Q2: Does it need AI reasoning?
            │
            ├── Yes → Agent
            │
            └── No → Hook
```

### Generation 3 Quality Standard (5 Required Components)

Every Skill produced by SSC must include:

| # | Component | Description |
|---|-----------|-------------|
| 1 | `disable-model-invocation: true` | Prevents redundant model invocation |
| 2 | GATE alignment | Restate → Confirm → Proceed only on OK |
| 3 | Hard stop points | At least 1 user confirmation gate |
| 4 | Quality check | Type-matched quality verification |
| 5 | Completion checklist | Checkbox list for done criteria |

---

## 架構設計 / Architecture

```
ssc/
├── SKILL.md              ← 主流程骨架 / Main workflow (< 100 lines)
└── knowledge/            ← 按需載入的參考資料 / On-demand references
    ├── classification.md ← 分類決策樹 / Classification decision tree
    ├── templates.md      ← Skill/Agent/Hook 模板 / Output templates
    └── quality-check.md  ← 品質驗證規格 / Quality validation specs
```

### 設計原則 / Design Principles

**中文：**
- **< 100 行主骨架**：SKILL.md 只放流程，大段參考資料全部拆到 `knowledge/`，避免每次載入浪費 token
- **按需讀取**：每個步驟只在用到的時候才讀對應的 knowledge 檔，不一次全載
- **GATE 強制對焦**：每次任務開始必須先複述理解、確認方向，避免方向跑偏後才發現
- **世代 3 完整性**：5 項必備元件確保每個 Skill 都能被理解、被維護、被升級
- **三種模式支援**：新建、轉換（改造別人的 Skill）、升級（世代 1/2 → 3）

**English:**
- **< 100-line skeleton**: SKILL.md only contains the workflow. Large references are split into `knowledge/` to avoid token waste on every load
- **On-demand reading**: Each step only reads its corresponding knowledge file when needed
- **GATE alignment**: Every task starts with intent restatement and confirmation, preventing wasted work from misunderstood requirements
- **Generation 3 completeness**: 5 required components ensure every Skill is understandable, maintainable, and upgradeable
- **Three modes**: New build, Convert (adapt others' Skills), Upgrade (Gen 1/2 → Gen 3)

### 三種執行模式 / Three Execution Modes

| 模式 | 觸發詞 | 說明 |
|------|--------|------|
| **新建** | 「建 Skill」、「做 Agent」 | 從零開始打造 |
| **轉換** | 「把這個 Skill 改成我們的格式」 | 改造他人結構 |
| **升級** | 「升級這個 Skill」 | 世代 1/2 → 世代 3 |

---

## 安裝 / Installation

### 方法一：手動安裝 / Manual Install

```bash
# 建立目錄 / Create directory
mkdir -p ~/.claude/skills/ssc/knowledge

# 複製檔案 / Copy files
cp SKILL.md ~/.claude/skills/ssc/
cp knowledge/*.md ~/.claude/skills/ssc/knowledge/
```

### 方法二：Clone 安裝 / Clone Install

```bash
# Clone 到 skills 目錄 / Clone into skills directory
cd ~/.claude/skills
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

安裝完成後，重啟 Claude Code 即可使用 `/ssc`。  
After installation, restart Claude Code and use `/ssc`.

---

## 使用範例 / Usage Examples

### 範例 1：建立新 Skill（中文）

```
用戶：幫我建一個每週回顧的 Skill
SSC：我理解你要建立一個「週回顧」互動式工作流 Skill。方向對嗎？
用戶：對
SSC：[開始訪談] 這個 Skill 要完成什麼任務？...
```

### Example 2: Upgrade Existing Skill (English)

```
User: Upgrade my deploy skill to Generation 3
SSC: I understand you want to upgrade the existing "deploy" Skill to Generation 3 standard. Is that right?
User: Yes
SSC: [Reads current SKILL.md, identifies missing components, patches them in]
```

### 範例 3：建立 Hook（中文）

```
用戶：我要一個每次 Session 開始自動讀 today.md 的 Hook
SSC：這是 Hook（事件驅動），不需要 AI 互動，純 Shell 腳本就夠了。方向對嗎？
用戶：對
SSC：[產出 settings.json hook 片段]
```

---

## 貢獻 / Contributing

歡迎提交 Issue 或 PR。  
Issues and PRs are welcome.

---

*Built with [Claude Code](https://claude.ai/code) · Maintained by [@fishtvlvoe](https://github.com/fishtvlvoe)*
