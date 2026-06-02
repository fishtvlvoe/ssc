# SSC — Super Skills Creator

> **[English](README.en.md)** | 繁體中文

**目前版本：** v1.2.0

SSC 是一個給 AI 程式代理用的 Skill，把重複的工作流程變成可重用的資產：**Skill**、**Agent** 和 **Hook**。

支援任何能載入 Skill 的代理：
**Claude Code** · **Codex** · **OpenAI Codex CLI** 及其他。

它回答一個實際問題：

> 這個工作流程應該做成互動式 Skill、自主執行的 Agent、還是事件觸發的 Hook？

SSC 會引導你完成分類、需求訪談、檔案結構、模板產出和品質檢查，讓結果不只是一段 prompt，而是可重用的自動化單元。

---

## 為什麼需要 SSC

AI 程式工作流程常常從一次性 prompt 開始。用一次沒問題，但跨團隊、跨專案時無法維護。

SSC 幫你把這些工作流程轉成有結構的資產：

| 需求 | SSC 產出 | 範例 |
|------|---------|------|
| 需要跟人來回確認的流程 | Skill | 規劃、除錯、寫文件、部署手冊 |
| 可以獨立完成的專家任務 | Agent | Code Review、安全掃描、程式碼分析 |
| 事件觸發的自動化 | Hook | Session 初始化、護欄、日誌、前置檢查 |

目標很簡單：讓 AI 開發工作流程可以被檢視、版控、重用、持續改善。

---

## SSC 做什麼

SSC 支援三種模式：

| 模式 | 用途 |
|------|------|
| 新建 | 從零打造 Skill、Agent 或 Hook |
| 轉換 | 把別人的 Skill 或 prompt 改造成 SSC 結構 |
| 升級 | 把舊的世代 1/2 工作流升級到世代 3 標準 |

工作流程：

```text
GATE 對焦確認
  → 分類 Skill / Agent / Hook
  → 收集需求
  → 產出結構
  → 品質檢查
  → 確認完成
```

---

## 世代 3 標準

SSC 使用世代 3 標準來確保產出的 Skill 可維護。

每個 Skill 應該包含：

| 要求 | 為什麼重要 |
|------|-----------|
| 執行元資料 | 宣告呼叫模式，讓代理正確載入 |
| GATE 對焦 | 動手前先確認使用者意圖 |
| 強制停止點 | 防止 AI 偷偷做產品決策 |
| 品質檢查 | 完成標準可測試，而非主觀判斷 |
| 完成清單 | 給維護者明確的「做完 / 沒做完」界線 |

Agent 和 Hook 各有自己的檢查：

- **Agent**：單一職責、清單驅動的審查、結構化輸出
- **Hook**：事件正確、可執行、有 timeout 上限、失敗時安全

---

## 檔案結構

```text
ssc/
├── SKILL.md
├── VERSION
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
└── knowledge/
    ├── classification.md
    ├── templates.md
    └── quality-check.md
```

| 檔案 | 用途 |
|------|------|
| `SKILL.md` | SSC 主工作流，AI 代理載入此檔 |
| `knowledge/classification.md` | Skill vs Agent vs Hook 決策樹 |
| `knowledge/templates.md` | 產出模板和結構規則 |
| `knowledge/quality-check.md` | 產出物的品質驗證規則 |
| `CHANGELOG.md` | 版本紀錄 |
| `VERSION` | 目前版本號 |

---

## 安裝

### Claude Code

```bash
cd ~/.claude/skills
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

重啟 Claude Code，輸入 `/ssc` 即可使用。

### Codex CLI

```bash
cd ~/.codex/skills      # 或你的 Codex skills 目錄
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

### 其他代理

把 `SKILL.md` 和 `knowledge/` 資料夾複製到你的代理載入 Skill 的位置。唯一要求是代理能讀 Markdown 檔案並按照裡面的工作流程指示執行。

### 觸發方式

安裝後，用 `/ssc` 或自然語言觸發：

- 建一個 Skill
- 做一個 Agent
- 加一個 Hook
- 升級這個 Skill

---

## 使用範例

| 情境 | 建議產出 |
|------|---------|
| 需要使用者確認的重複部署流程 | Skill |
| 可以獨立跑的 Code Review 流程 | Agent |
| 攔截危險 Shell 指令的規則 | Hook |
| 團隊一直在不同專案間複製貼上的長 prompt | Skill |
| 讀取程式碼並回報風險的分析工具 | Agent |

---

## 維護者說明

SSC 是一個開源的 AI 輔助開發工作流程工具。刻意保持精簡：主工作流保持可讀性，較大的參考資料放在 `knowledge/`，用到時才載入。

適合貢獻的方向：

- 審查修改決策樹或模板的 PR
- 產生 Skill / Agent / Hook 分類的迴歸測試範例
- 檢查產出的 Skill 是否符合世代 3 品質標準
- 改善 Release Notes 和文件
- 審查產出 Hook 的安全性

---

## 授權

MIT. 見 [LICENSE](LICENSE)。

---

由 [@fishtvlvoe](https://github.com/fishtvlvoe) 建立與維護。
