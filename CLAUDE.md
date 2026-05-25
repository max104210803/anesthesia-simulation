# ANESTHESIA SIMULATION — 專案知識錨點

> 維護原則：每次做出架構決策或完成重要功能，立即更新本檔案。
> 超過 250 行時，將舊段落移至 `CC-Session-Logs/archive.md`。

---

## 專案基本資訊

| 項目 | 內容 |
|------|------|
| 專案名稱 | ANESTHESIA SIMULATION |
| Firebase 專案 ID | `anesthesia-simulation` |
| 專案編號 | 1045190313519 |
| 專案目錄 | `G:\我的雲端硬碟\firebase_project` |
| Firestore 位置 | asia-east1（台灣）|
| 建立日期 | 2026-05-24 |

---

## 環境與工具

### Firebase MCP 設定
- **設定位置**：`G:\我的雲端硬碟\firebase_project\.mcp.json`
- **啟動指令**：`node C:\Users\cc\AppData\Roaming\npm\node_modules\firebase-tools\lib\bin\firebase.js mcp --dir G:\我的雲端硬碟\firebase_project`
- **狀態**：✅ 已驗證可用（2026-05-24）
- **可用工具**：完整 Firestore CRUD、Auth、Storage、Messaging、RemoteConfig

### Firebase CLI
- **版本**：15.18.0（全域安裝於 `C:\Users\cc\AppData\Roaming\npm\`）
- **登入帳號**：已登入（執行 `npx firebase-tools@latest projects:list` 可驗證）
- **部署規則指令**：`npx firebase-tools@latest deploy --only firestore:rules`

### Node.js
- **版本**：v25.9.0

---

## Firestore 安全規則策略

**原則：白名單做法**（正式版模式，非測試模式）

- 預設全部禁止（`match /{document=**} { allow read, write: if false; }`）
- 每個功能集合單獨開放
- 規則檔位置：`firestore.rules`
- **新增集合時**：在 `firestore.rules` 加入對應 match 區塊，再執行部署

### 目前已開放集合

| 集合名稱 | 用途 | 權限 |
|---------|------|------|
| `wordcloud_words` | 預留（文字雲示範用）| read/write: true |

---

## Firestore 資料結構決策

> ⚠️ 尚待定義——開始開發功能時於此記錄

<!-- 範例格式：
### patients（病人情境集合）
- **路徑**：`patients/{patientId}`
- **決策**：使用子集合 `scenarios` 而非平坦結構，原因：方便獨立查詢單一病人的所有情境
- **欄位**：`name`、`age`、`diagnosis`、`created_at`
- **決策日期**：YYYY-MM-DD
-->

---

## 已完成功能

- [x] Firebase 專案建立（ANESTHESIA SIMULATION）
- [x] Cloud Firestore 啟用（正式版模式）
- [x] Firestore 安全規則部署（白名單架構）
- [x] Firebase MCP 連接 Claude Code（✅ CRUD 全驗證）

---

## 開發中 / 待辦功能

> 開始開發時於此更新

- [ ] （待定義）模擬情境的資料結構設計
- [ ] （待定義）前端介面框架選擇
- [ ] （待定義）學員互動流程設計

---

## 架構決策記錄（ADR）

> 每次做出「以後難以更改」的決策，就在這裡加一筆。

<!-- 範例格式：
### ADR-001：選擇 Firebase 而非 Supabase
- **日期**：2026-05-24
- **決策**：使用 Firebase Firestore
- **原因**：免費並發 100 萬、不會閒置暫停、MCP 工具完整
- **取捨**：放棄 SQL JOIN/GROUP BY 的強大統計能力
-->

### ADR-001：Firestore 安全規則採白名單模式
- **日期**：2026-05-24
- **決策**：以正式版模式啟動，逐集合開放
- **原因**：測試模式 30 天後自動失效，正式版模式更安全且可長期維護
- **操作方式**：編輯 `firestore.rules` → 執行 `npx firebase-tools@latest deploy --only firestore:rules`

---

## 常用指令速查

```bash
# 部署 Firestore 安全規則
npx firebase-tools@latest deploy --only firestore:rules

# 確認 Firebase 登入狀態
npx firebase-tools@latest projects:list

# 重新登入 Firebase
npx firebase-tools@latest logout
npx firebase-tools@latest login

# 移除並重設 Firebase MCP
claude mcp remove firebase
```

---

## 給 Claude 的工作提示

- Firestore 路徑格式：`projects/anesthesia-simulation/databases/(default)/documents`
- 查詢集合時，`collection_path` **不要**加尾巴 `/`（例如用 `wordcloud_words` 而非 `wordcloud_words/`）
- 新增功能需要新集合時，記得同步更新 `firestore.rules` 並部署
- 本專案為醫學模擬教育工具，資料設計需考慮**去識別化**（存座號不存真名）

---

*最後更新：2026-05-24*
