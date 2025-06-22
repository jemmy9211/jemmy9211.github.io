# Jemmy's Personal Website

這是我的個人網站，使用Jekyll靜態網站生成器和Minimal Mistakes主題建構。

🌐 **網站地址**: [jemmy9211.github.io](https://jemmy9211.github.io)

## 📖 關於

這個網站包含我的技術部落格、專案作品集和個人資訊。我在這裡分享程式設計經驗、技術學習筆記和專案成果。

## 🛠 技術棧

- **靜態網站生成器**: Jekyll
- **主題**: Minimal Mistakes
- **標記語言**: Markdown
- **樣式**: Sass/SCSS
- **部署**: GitHub Pages
- **版本控制**: Git

## ✨ 功能特色

- 📝 技術部落格文章
- 🎨 響應式設計
- 🔍 全站搜索功能
- 📱 移動端友好
- 🏷 標籤和分類系統
- 💬 評論系統支援
- 📊 Google Analytics 整合
- 🌙 多種主題皮膚

## 📁 目錄結構

```
├── _config.yml          # Jekyll 配置文件
├── _data/               # 數據文件
│   ├── navigation.yml   # 導航配置
│   └── ui-text.yml     # UI 文本配置
├── _includes/           # 可重用的HTML片段
├── _layouts/            # 頁面布局模板
├── _posts/              # 部落格文章
├── _sass/               # Sass 樣式文件
├── assets/              # 靜態資源
│   ├── css/            # 樣式文件
│   ├── js/             # JavaScript 文件
│   └── images/         # 圖片資源
├── about.markdown       # 關於頁面
└── index.html          # 首頁
```

## 🚀 本地開發

### 前置要求

- Ruby (>= 2.7.0)
- Bundler
- Git

### 安裝與運行

1. **複製專案**
   ```bash
   git clone https://github.com/jemmy9211/jemmy9211.github.io.git
   cd jemmy9211.github.io
   ```

2. **安裝依賴**
   ```bash
   bundle install
   ```

3. **本地運行**
   ```bash
   bundle exec jekyll serve
   ```

4. **訪問網站**
   打開瀏覽器訪問 `http://localhost:4000`

### 寫作流程

1. 在 `_posts/` 目錄下創建新的 Markdown 文件
2. 文件名格式：`YYYY-MM-DD-title.markdown`
3. 在文件開頭添加 YAML front matter：
   ```yaml
   ---
   title: "文章標題"
   date: 2024-01-01
   categories: [category1, category2]
   tags: [tag1, tag2]
   ---
   ```

## 📊 部落格文章主題

根據現有文章，主要涵蓋以下主題：

- 🤖 **機器學習**: YOLOv4, 計算機視覺
- 💻 **程式設計**: C++, 演算法, 資料結構
- 🔧 **開發工具**: Git, Markdown語法
- 📈 **演算法**: 時間複雜度分析, 佇列, 堆積, 環檢測
- 🎯 **專案經驗**: Mirror Forest, CV Team

## 🔧 自定義功能

- **多語言支援**: 支援繁體中文和英文
- **代碼高亮**: 支援多種程式語言語法高亮
- **數學公式**: 支援 LaTeX 數學公式渲染
- **圖片展示**: 支援圖片畫廊和燈箱效果
- **SEO優化**: 自動生成 meta 標籤和 sitemap

## 📈 網站統計

- Google Analytics 整合
- 頁面瀏覽量追蹤
- 用戶行為分析

## 🤝 貢獻

如果你發現任何問題或有改進建議，歡迎：

1. 提交 Issue
2. 發送 Pull Request
3. 通過網站聯繫我

## 📄 授權

本專案採用 MIT 授權條款。

## 📧 聯絡方式

- **網站**: [jemmy9211.github.io](https://jemmy9211.github.io)
- **GitHub**: [jemmy9211](https://github.com/jemmy9211)

---

*最後更新：2024年12月*

> 這個網站記錄了我的技術成長歷程，希望能對其他開發者有所幫助。如果你覺得有用，歡迎給個 ⭐️！
