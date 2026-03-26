# AgentOS

基於 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 打造的多代理人作業系統。由中央協調者（Chief）將任務分派給各專業代理人，每位代理人擁有獨立的身份設定、記憶系統與技能。

> **[English Version](README.md)**

## 架構

```
AgentOS
├── CLAUDE.md          # Chief — 中央協調者
├── skills/            # 所有代理人共用的技能
├── templates/         # 新增代理人與技能的範本
├── memory/            # 跨團隊共享知識庫與每日日誌
└── agents/
    ├── dev/           # 程式碼、架構、除錯
    ├── ops/           # CI/CD、部署、基礎設施
    ├── writer/        # 寫作、文件、內容
    ├── researcher/    # 研究、分析、事實查核
    └── pm/            # 專案規劃、知識管理
```

## 運作方式

**卡卡西（Kakashi）** 扮演幕僚長的角色——所有請求先經過他。他會判斷要自行處理，還是派工給對的專家：

| 代理人 | 代號 | 負責範圍 |
|---|---|---|
| **@dev** | 鳴人（Naruto） | 功能開發、Bug 修復、Code Review、架構設計 |
| **@ops** | 大和（Yamato） | CI/CD 流水線、部署、基礎設施、監控 |
| **@writer** | 自來也（Jiraiya） | 文件撰寫、部落格、Email、內容編輯 |
| **@researcher** | 鹿丸（Shikamaru） | 研究調查、競品分析、事實查核 |
| **@pm** | 綱手（Tsunade） | 專案規劃、任務拆解、進度追蹤、知識管理 |

每位代理人在獨立的 context window 中運行，擁有自己的 `CLAUDE.md`、記憶與技能。Chief 會彙整結果後回報。

### 多代理人協作

跨領域任務會由 Chief 拆解後並行委派：

- 程式碼 + 部署 → 鳴人寫程式、大和處理流水線
- 研究 → 規劃 → 實作 → 鹿丸 → 綱手 → 鳴人
- 每位代理人會標記需要其他專家配合的部分，由 Chief 協調

## 核心特色

- **智慧路由** — Chief 分析請求，分派給最適合的代理人
- **持久記憶** — 每位代理人維護自己的記憶，記錄模式、經驗與上下文
- **自動反思** — 每位代理人完成重要任務後強制寫入 daily log（內建行為，非可選）
- **跨代理人協作** — 代理人會標記需要其他專家的工作，Chief 負責協調
- **可擴充技能** — SOP 以 markdown 檔案存在，可共用或代理人專屬

## 可用技能

| 技能 | 檔案 | 說明 |
|---|---|---|
| 分類 | `skills/triage.md` | 分類請求並路由到對的代理人 |
| 每日早報 | `skills/morning-briefing.md` | 每日啟動總覽 |
| Code Review | `skills/code-review.md` | 結構化程式碼審查流程 |
| 每週彙整 | `skills/weekly-summary.md` | 每週進度彙整 |

## 快速開始

1. 安裝 [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
2. Clone 這個 repo
3. 在專案根目錄執行 `claude`，Chief 會自動載入

```bash
git clone git@github.com:allen-hsu/agent-os.git
cd agent-os
claude
```

## 定時任務

可以透過標準 cron 或 Claude Code 內建排程來執行重複性工作（例如每日 Morning Briefing）。

### 方案一：本機 cron + Claude CLI

加入 crontab（`crontab -e`）：

```bash
# Morning Briefing — 每天早上 9 點
0 9 * * * cd /Users/you/agent-os && claude -p "執行 Morning Briefing：讀取 memory/daily/ 的近期團隊日誌、讀取 memory/MEMORY.md 的優先事項、檢查每個 agent 的 memory/daily/ 活動紀錄，輸出簡潔的每日簡報。" >> /tmp/morning-briefing.log 2>&1
```

**前提**：電腦要開著，Claude CLI 要裝好。

### 方案二：Session 內排程（僅限測試）

在 Claude Code session 中，請 Chief 建立臨時排程：

```
幫我每 10 分鐘跑一次 Morning Briefing
```

使用 Claude Code 內建的 `CronCreate`——僅限當前 session，最多存活 7 天。

### 可用的定時任務

| 任務 | Skill 檔案 | 建議排程 |
|---|---|---|
| Morning Briefing | `skills/morning-briefing.md` | 每天早上 9 點 |
| Weekly Summary | `skills/weekly-summary.md` | 每週一早上 9 點 |

## 新增代理人

使用 `templates/new-agent.md` 範本來建立新的專業代理人。每位代理人需要：

- `CLAUDE.md` — 身份、原則、工具、記憶、技能
- `IDENTITY.md` — 簡要摘要，供 Chief 做路由判斷
- `memory/MEMORY.md` — 持久知識索引

## 授權

MIT
