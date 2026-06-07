# 教育部高級中等學校原住民學生青年領袖培育營｜南區初階

這個專案是「教育部高級中等學校原住民學生青年領袖培育營｜南區初階」活動網站，提供活動資訊、實施計畫、課程內容、報名與推薦表上傳連結、錄取名單、活動系統入口與歷年文件整理。

網站以靜態 HTML/CSS/JavaScript 建置，可直接部署於 GitHub Pages，並透過 `CNAME` 設定自訂網域。主要內容已整合為單頁式 `index.html`，使用者可透過頁面選單切換各活動區域。

## 網站內容

- `index.html`：網站主頁與單頁式內容入口，包含首頁、實施計畫、活動課程、錄取學員、行前通知與推薦表上傳區域。
- `info.html`：活動系統入口，嵌入 Google Apps Script 活動系統。
- `archive/`：封存舊系統頁面，例如作業上傳、學員系統、報到頁面等。

## 專案結構

```text
.
├── archive/          # 已封存的舊頁面
├── css/              # Bootstrap、主要樣式與響應式樣式
├── document/         # 活動文件、表單、PDF、圖片資料
│   ├── 112/          # 112 年活動文件
│   └── 113/          # 113 年活動文件
├── fonts/            # Font Awesome 字型檔
├── images/           # 網站圖片、Logo、Icon
├── js/               # jQuery、Bootstrap 與自訂腳本
├── CNAME             # GitHub Pages 自訂網域設定
├── LICENSE           # MIT License
├── index.html        # 單頁式活動網站
└── info.html         # 活動系統入口
```

## 單頁區域

`index.html` 使用 hash routing 顯示不同內容區塊：

- `#home`：首頁主視覺與快速入口。
- `#about`：實施計畫與表單下載。
- `#class`：活動課程。
- `#news`：錄取學員。
- `#notice`：行前通知。
- `#reform`：推薦表上傳。

每個內容區塊都保留 `data-api-view` 屬性，之後可依區域串接 Google Apps Script API 載入後台資料。

## 使用技術

- HTML5
- CSS3 / SCSS
- Bootstrap
- jQuery
- Font Awesome
- Google Analytics
- Google Forms
- Google Apps Script iframe
- Google Apps Script API ready
- GitHub Pages

## 本機預覽

此專案是靜態網站，不需要安裝後端或建置工具。可以直接用瀏覽器開啟：

```text
index.html
```

若要用本機伺服器預覽，也可以在專案根目錄執行：

```powershell
python -m http.server 8000
```

然後開啟：

```text
http://localhost:8000
```

## 部署

此專案可透過 GitHub Pages 部署。推送到 `main` 分支後，GitHub Pages 會依 repository 設定更新網站。

自訂網域設定於：

```text
CNAME
```

目前網域為：

```text
wilc.work
```

## 維護注意事項

- 更新活動年份時，請同步檢查首頁、實施計畫、錄取名單、表單下載與 Google Forms 連結。
- 新年度文件建議放在 `document/` 下，歷年資料可依年度建立子資料夾保存。
- 若頁面引用 PDF 或圖片，請確認檔案路徑與大小寫正確，避免 GitHub Pages 上無法載入。
- 若要串接 Google Apps Script API，可先設定 `index.html` 內的 `window.CCSH_API.baseUrl`，再依 `data-api-view` 對應區塊載入資料。
- `archive/` 內為封存頁面，若不再提供公開入口，仍可作為歷史備份使用。

## 授權

本專案採用 MIT License，詳見 `LICENSE`。
