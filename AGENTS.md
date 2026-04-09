# GitHub 偵察機 - 開發者指南

## 專案目標
建立一個 Vue 3 網頁應用，用於搜尋與展示 GitHub 使用者資訊。

## 開發者身份
- 大二初學者
- 只懂 HTML
- 需要白話文比喻來理解 Vue 概念

## 對話守則
- **禁止使用 Vue 專業術語**（如 ref、reactive、lifecycle、computed、watcher 等）
- **使用生活比喻**：
  - `ref` → 「盒子」（裝資料的盒子）
  - `reactive` → 「袋子」（裝很多相關東西的袋子）
  - `function` → 「工廠」（做事的功能）
  - `component` → 「小工具」（可重複使用的零件）
  - `props` → 「輸入」（從外面傳進來的資料）
  - `emit` → 「喊話」（跟外面溝通的方式）

## 實作守則
1. 每次只寫一小段程式碼（約 10-20 行）
2. 在程式碼旁邊加上**白話文註解**（用中文）
3. 寫完後解释這段程式在做什麼

## 技術 stack
- Vue 3（Composition API）
- Vite（開發伺服器）
- GitHub API（取得使用者資料）

## 常用指令
```bash
npm install     # 安裝需要的工具
npm run dev     # 啟動開發伺服器（網頁會自動打開）
npm run build   # 打包成正式網站
```

## 檔案結構
```
專案資料夾/
├── src/
│   ├── components/   # 小工具（可重複使用的零件）
│   ├── App.vue       # 網站的主要入口
│   └── main.js       # 程式的開始點
├── index.html        # 網頁的門面
└── package.json     # 專案的設定檔
```

## 開發流程
1. 先寫小功能 → 測試成功 → 再寫下一個
2. 不確定時先問使用者
3. 每次改動後都要確認網頁正常運作