# Google Apps Script 後台資料庫格式

此資料庫格式以 Google Sheets 作為後台資料來源，提供 Apps Script Web App 管理內容，前端 `index.html` 透過 API 取得最新資料。

## Sheet: SiteSettings

網站全域設定。前端會以 key/value 方式讀取。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| key | text | yes | 設定鍵，唯一值 | site_title |
| value | text | yes | 設定值 | 教育部高級中等學校原住民學生青年領袖培育營 |
| group | text | no | 設定分類 | site |
| description | text | no | 後台說明 | 網站主標題 |
| is_public | boolean | yes | 是否提供給前端 API | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

建議初始資料：

| key | value | group | description | is_public |
| --- | --- | --- | --- | --- |
| site_title | 教育部高級中等學校原住民學生青年領袖培育營 | site | 網站主標題 | TRUE |
| site_subtitle | 南區初階 | site | 網站副標題 | TRUE |
| contact_phone | 08-7882017#307 | contact | 聯絡電話 | TRUE |
| contact_email | indigenous@apps.ccsh.ptc.edu.tw | contact | 聯絡信箱 | TRUE |
| school_url | https://www.ccsh.ptc.edu.tw | contact | 學校網站 | TRUE |
| youtube_url | https://www.youtube.com/embed/MD51Io48GNQ | media | 首頁影片 | TRUE |
| google_analytics_id | G-WLW67H2H8T | site | GA 追蹤 ID | TRUE |

## Sheet: Pages

管理 `index.html` 內各頁籤區塊，例如首頁、實施計畫、活動課程、錄取學員、行前通知、推薦表上傳。
活動課程區不另建課程資料表，未來由 `embed_type=iframe` 搭配 `embed_url` 嵌入外部課程網站或系統。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| page_key | text | yes | 頁面代號，對應前端 `data-api-view` | about |
| nav_label | text | yes | 導航列顯示文字 | 實施計畫 |
| title | text | yes | 區塊標題 | 實施計畫 |
| subtitle | text | no | 區塊副標題 | 活動辦理資訊 |
| content_html | html | no | 主要 HTML 內容 | `<p>活動目的...</p>` |
| embed_type | text | no | 嵌入類型 | iframe / pdf / form / none |
| embed_url | url | no | iframe、PDF 或表單網址 | https://... |
| api_endpoint | text | no | 未來細部 API 端點 | getPage |
| sort_order | number | yes | 顯示順序 | 20 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

建議初始資料：

| page_key | nav_label | title | embed_type | api_endpoint | sort_order | is_active |
| --- | --- | --- | --- | --- | --- | --- |
| home | 首頁 | 首頁 | none | getHome | 10 | TRUE |
| about | 實施計畫 | 實施計畫 | none | getPage | 20 | TRUE |
| class | 活動課程 | 活動課程 | iframe | getPage | 30 | TRUE |
| news | 錄取學員 | 錄取學員 | pdf | getAdmissions | 40 | TRUE |
| notice | 行前通知 | 行前通知 | none | getNotices | 50 | TRUE |
| reform | 推薦表上傳 | 推薦表上傳 | form | getForms | 60 | TRUE |

## Sheet: Documents

管理所有文件、PDF、圖片、表單下載連結。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| document_key | text | yes | 文件代號，唯一值 | recommend_115_pdf |
| year | number | yes | 年度 | 115 |
| category | text | yes | 文件分類 | recommend / parent_consent / admission / notice / map |
| page_key | text | no | 所屬頁面 | about |
| title | text | yes | 顯示名稱 | 推薦表 PDF |
| file_type | text | yes | 檔案類型 | pdf / docx / image / url |
| file_url | url | yes | 檔案網址或站內路徑 | /document/115年原民領培營南區初階推薦表.pdf |
| description | text | no | 文件說明 | 115 年南區初階推薦表 |
| sort_order | number | yes | 顯示順序 | 10 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: Forms

管理 Google Forms 或其他外部表單。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| form_key | text | yes | 表單代號，唯一值 | registration |
| page_key | text | yes | 所屬頁面 | about |
| title | text | yes | 表單名稱 | 報名學員 |
| form_url | url | yes | 表單網址 | https://forms.gle/... |
| open_at | datetime | no | 開放時間 | 2026-05-01 00:00:00 |
| close_at | datetime | no | 截止時間 | 2026-05-22 23:59:00 |
| button_label | text | yes | 按鈕文字 | 點擊報名 |
| sort_order | number | yes | 顯示順序 | 10 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: Notices

管理行前通知，例如物品、交通、地圖、重要提醒。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| notice_key | text | yes | 通知代號，唯一值 | packing |
| title | text | yes | 通知標題 | 攜帶物品 |
| content_html | html | no | 通知內容 | `<ul><li>健保卡</li></ul>` |
| image_url | url | no | 圖片網址 | /document/113/113領培營-物品.png |
| file_url | url | no | 附件網址 | /document/...pdf |
| sort_order | number | yes | 顯示順序 | 10 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: Admissions

管理錄取名單與公告 PDF。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| admission_key | text | yes | 錄取公告代號，唯一值 | admission_115 |
| year | number | yes | 年度 | 115 |
| title | text | yes | 公告標題 | 115 年原民領培營錄取名單 |
| pdf_url | url | yes | PDF 網址 | /document/115原民領培營錄取名單.pdf |
| publish_at | datetime | no | 發布時間 | 2026-06-01 12:00:00 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: Media

管理首頁圖片、Logo、社群連結、影片等素材。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| media_key | text | yes | 素材代號，唯一值 | hero_image |
| media_type | text | yes | 素材類型 | image / video / social |
| title | text | yes | 素材名稱 | 首頁主視覺 |
| url | url | yes | 素材網址 | /images/HEAD2.JPG |
| alt_text | text | no | 替代文字 | 活動主視覺 |
| sort_order | number | yes | 顯示順序 | 10 |
| is_active | boolean | yes | 是否啟用 | TRUE |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: AdminUsers

後台管理者帳號。正式上線時建議不要儲存明文密碼，可改存 `password_hash`，或使用 Apps Script PropertiesService 管理敏感資訊。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| username | text | yes | 帳號，唯一值 | admin |
| password_hash | text | yes | 密碼雜湊 | sha256... |
| display_name | text | no | 顯示名稱 | 管理者 |
| role | text | yes | 權限角色 | admin / editor |
| is_active | boolean | yes | 是否啟用 | TRUE |
| last_login_at | datetime | no | 最後登入時間 | 2026-06-05 10:00:00 |
| updated_at | datetime | yes | 更新時間 | 2026-06-05 10:00:00 |

## Sheet: AuditLogs

紀錄後台修改行為，方便追蹤內容更新。

| 欄位 | 型別 | 必填 | 說明 | 範例 |
| --- | --- | --- | --- | --- |
| log_id | text | yes | 紀錄 ID | 20260605_100000_admin |
| username | text | yes | 操作者 | admin |
| action | text | yes | 動作 | update_page |
| target_sheet | text | yes | 目標資料表 | Pages |
| target_key | text | no | 目標資料 key | about |
| before_json | json | no | 修改前資料 | `{...}` |
| after_json | json | no | 修改後資料 | `{...}` |
| created_at | datetime | yes | 建立時間 | 2026-06-05 10:00:00 |

## Public API 建議回傳格式

```json
{
  "success": true,
  "settings": {},
  "pages": {},
  "documents": [],
  "forms": [],
  "notices": [],
  "admissions": [],
  "media": [],
  "updated_at": "2026-06-05 10:00:00"
}
```

## 前端對應

| 前端區域 | data-api-view | 主要資料表 |
| --- | --- | --- |
| 首頁 | home | SiteSettings, Media, Forms |
| 實施計畫 | about | Pages, Documents, Forms |
| 活動課程 | class | Pages |
| 錄取學員 | news | Pages, Admissions |
| 行前通知 | notice | Pages, Notices, Documents |
| 推薦表上傳 | reform | Pages, Forms |
| 活動系統 | info | SiteSettings |
