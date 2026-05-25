# ANESTHESIA SIMULATION — 即時文字雲

課堂互動工具：學生輸入關鍵字，老師即時看到文字雲。

---

## 🔗 網址

| 用途 | 網址 |
|------|------|
| 📱 **學生輸入頁**（給學生） | https://max104210803.github.io/anesthesia-simulation/ |
| 🖥️ **即時展示頁**（老師投影） | https://max104210803.github.io/anesthesia-simulation/display.html |

---

## 👨‍🎓 學生怎麼用

1. 手機開啟學生輸入頁網址
2. 輸入一個關鍵字（最多 20 字）
3. 按「送出」→ 完成

> 同一裝置只能送出一次，關閉再開頁面仍維持已送出狀態。

---

## 👨‍🏫 老師怎麼用

### 上課前
- 開啟**展示頁**，投影到螢幕

### 課中
- 學生用手機輸入關鍵字
- 文字雲即時更新（無需重新整理）
- 越多人輸入同一個詞，字體越大

### 開始下一個活動
1. 在展示頁按右上角「**🔄 開新活動**」
2. 確認 → 文字雲清空
3. 學生重新整理頁面後，可以重新送出

---

## 📊 查詢與分析資料

直接在 Claude Code 對話中說：

```
幫我統計 wordcloud_words 裡的關鍵字，列出前 10 名
```

```
幫我把今天的關鍵字整理成表格
```

```
幫我刪掉所有測試資料
```

Claude 會透過 Firebase MCP 直接查詢 Firestore，不需要進 Firebase Console。

---

## 🗂️ 專案結構

```
index.html        學生輸入頁
display.html      即時文字雲展示頁
firestore.rules   Firestore 安全規則
firebase.json     Firebase CLI 設定
```

---

## ⚙️ 新增功能時

每次新增需要新 Firestore 集合的功能，必須：

1. 在 `firestore.rules` 加入對應的 `match` 區塊
2. 執行部署：
   ```bash
   npx firebase-tools@latest deploy --only firestore:rules
   ```
3. 確認出現 `Deploy complete!`
