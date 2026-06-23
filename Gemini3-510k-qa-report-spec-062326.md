醫療器材 FDA 510(k) 智能審查與報告生成系統：完整技術規格與架構設計書 (Technical Specification)
本文件旨在為一項基於代理人（Agentic AI）架構的 FDA 510(k) 審查與報告生成平台提供詳盡的技術規格說明。該平台專為醫療器材製造商、法規事務（RA）顧問和審查專家設計，能透過 30 題核心問與答互動（基於 Samsung Medison HERA Z20 診斷式超音波系統之 TFDA 審查報告及本案 510(k) 脈絡），自動編寫並精煉出一份 3,000 至 4,000 字、符合 FDA 申報品質的繁體中文 510(k) 審查報告（其中整合與使用者回答之新內容，皆以「珊瑚色 (#F87171, Coral)」顯著標註）。
本平台不僅支援 Markdown 即時雙欄編輯、靈活的導出機制（Google Docs、HTML、PDF、Markdown），更深度結合智慧多模型切換（以 gemini-3.1-flash-lite（或最新 gemini-2.5-flash 系列）為預設，並開放用戶選擇），同時配備 5 + 3 項獨家 AI 魔法超能力功能（Wow AI Features），以及完整的問卷 Markdown 上傳、編輯與下載模組。
1. 系統願景與核心概念 (System Vision & Core Concept)
510(k) 申報是醫療器材進入美國市場最具挑戰性的法規里程碑之一。傳統申報書與審查報告的撰寫流程極其漫長，涉及電性安全（IEC 60601-1）、電磁相容性（IEC 60601-1-2）、超音波安全（IEC 60601-2-37）、生物相容性（ISO 10993-1）、軟體確效（IEC 62304）、網路安全與 AI/ML 輔助軟體（CADe/CADx）等多維度的複雜文件調研。
本平台透過 Agentic-guided Interactive Drafting (導向式代理人互動起草) 技術解決此痛點：
動態問卷引導：不要求用戶面對一張空白的 510(k) 範本，而是主動提出 30 個精準、具備法規意識的問題。
增量整合與追蹤（珊瑚色標籤）：利用語義比對與版本控制（AST 差分），將用戶的回答以珊瑚色視覺高亮嵌入報告草稿中，明晰展示「哪些是基於新事實（New Facts）生成的內容」。
無縫編修與多端輸出：提供 WYSIWYG（所見即所得）結合實時 Markdown 編輯的極致體驗，並與 Google Workspace、本地 PDF 引擎等深度綁定。
2. 系統架構設計與技術棧 (System Architecture & Technology Stack)
為了保證極速開發、極致 UI 質感與強大的後端能力，本系統採用全棧（Full-Stack）架構，前後端完全分離，輔以強力的 API 代理層以保護金鑰。
code
Code
+------------------------------------------------------------------------+
|                            用戶瀏覽器 (Client-Side)                    |
|  +--------------------+  +----------------------+  +----------------+  |
|  | Tailwind CSS UI    |  | Motion 動態渲染      |  | Markdown編輯器 |  |
|  +---------+----------+  +----------+-----------+  +--------+-------+  |
+------------|------------------------|-----------------------|----------+
             |                        |                       |           
             +------------------------+-----------------------+           
                                      v                                   
+------------------------------------------------------------------------+
|                         Vite + Express 伺服器 (Server-Side)            |
|  +-------------------------+   +------------------------------------+  |
|  | /api/gemini/chat        |   | Google Workspace OAuth (Drive/Docs)|  |
|  | @google/genai SDK 代理  |   | /api/export/googledoc              |  |
|  +-------------------------+   +------------------------------------+  |
|  +-------------------------+   +------------------------------------+  |
|  | 30題問答動態引擎        |   | PDF 渲染引擎 (Puppeteer)           |  |
|  | 問卷 MD 解析器          |   | /api/export/pdf                    |  |
|  +-------------------------+   +------------------------------------+  |
+------------------------------------------------------------------------+
2.1 核心技術棧清單
前端框架：React 19 (搭配 TypeScript 5.8 及 Vite 6.0)。
介面與動畫：Tailwind CSS（使用 @tailwindcss/vite 進行超高速編譯）、Lucide UI 圖標庫、motion/react（實現流暢的卡片翻轉、過渡動畫與動態打字效果）。
Markdown 與編輯：react-markdown（整合自定義 Renderer 以便為珊瑚色標記注入 class）、remark-gfm、rehype-raw。
後端框架：Express 4 (搭配 tsx 做開發熱重載、esbuild 進行 Bundle 出 dist/server.cjs)。
AI 整合：官方最新 @google/genai TypeScript SDK。所有呼叫皆部署於服務器端（Server-Side），嚴密保護 GEMINI_API_KEY。
文件導出 API：
Google Docs：藉由 Google OAuth 2.0 串接 Google Drive 與 Google Docs API。
PDF：伺服器端採用基於 Puppeteer / Headless Chrome 的渲染方案，保證排版 100% 精準。
HTML/Markdown：純前端 Blob 下載機制，省去不必要的網絡開銷。
3. 詳細功能模組規範 (Detailed Functional Module Specifications)
3.1 30題互動問合規系統 (The 30-Question Interactive Interview Module)
此模組是系統獲取輸入的「法規漏斗（Regulatory Funnel）」。系統將向用戶提出 30 個精心設計的問題，覆蓋 510(k) 申報、TFDA 臨床前基準與超音波診斷系統的安全指標。
其 30 題核心指標與問題設計矩陣如下：
編號	審查構面 (Regulatory Dimension)	Traditional Chinese 核心問題	預期輸入範例
Q1	基本資訊 (Basic Info)	本案件 HERA Z20 是否有與 K241971 所提及的其他型號（如 R20, HERA Z30）共享相同的電路主板與電源供應器？	"是的，與 R20 相同，但外殼尺寸更小"
Q2	預期用途 (Intended Use)	本產品臨床應用（例如產科、肌肉骨骼、心臟、胸部）在台灣擬申請的範圍是否與美國 K241971 核准範圍完全一致？	"一致，移除經食道心臟用途"
Q3	電性安全 (Electrical Safety)	檢附的 Nemko 測試報告中，IEC 60601-1:2025 對產品漏電流（Leakage Current）的容許值及實測值為何？	"實測值小於 50 uA，符合安全標準"
Q4	電磁相容 (EMC)	IEC 60601-1-2:2014 測試報告中，HERA Z20 在 30MHz-1GHz 射頻輻射干擾（Radiated Emission）的裕度（Margin）是多少？	"Margin 為 4.2 dB30MHz，安全通過"
Q5	超音波專用標準	針對關鍵不符合點「未檢附 IEC 60601-2-37 測試報告」，貴司是否可在本系統補充其操作模式在最大輸出時的安全阻抗與熱功耗？	"已由原廠追加 Nemko IEC 60601-2-37 測試"
Q6	機械指數 (MI)	請提供本產品 CMV1-10 探頭在最大聲學輸出時的機械指數 (MI) 最大測量結果。是否符合 MI < 1.9 限制？	"MI 最大值為 1.4，低於限值"
Q7	熱指數 (TI)	在使用 BMode、Color Doppler 及 M-Mode 混合模式下，系統所顯示的軟組織熱指數 (TIS) 最大值為多少？	"TIS 最大值為 1.2"
Q8	探頭規格 (Transducer)	針對新探頭 CMV1-10 與 CMV1-10Z，請填寫其物理中心頻率（Center Frequency）及高低頻帶界限。	"高頻 10 MHz，低頻 1.2 MHz"
Q9	軸向解析度 (Axial Res)	CMV1-10 探頭在極限掃描深度（例如 15cm）時的軸向解析度數值為何？	"軸向解析度為 0.45 mm"
Q10	側向解析度 (Lateral Res)	探頭 CMV1-10 的側向解析度規格是多少？在焦距（Focus Position）處實測多少？	"側向解析度於焦點處為 0.8 mm"
Q11	掃描特性 (Scanning Specs)	CMV1-10 與 CMV1-10Z 探頭的極限掃描角度（扇形角度）或最大掃描長度（線性探頭）為何？	"對角掃描角度為 65 度"
Q12	量測類型與準確度	系統針對距離（Distance）、面積（Area）及心率（Heart Rate）的量測準確度限制是否小於 ±3%？	"距離準確度 ±1.5%，體積 ±2%"
Q13	血流速度量測 (Doppler Sync)	本案彩色都卜勒（Color Doppler）血流速度（Flow Velocity）量測的誤差值是否與 K241971 標示一致？	"一致，流速量測誤差為 ±5%"
Q14	定量/半定量功能	說明書內記載之 S-FLOW、MV-FLOW 及 IOTA-ADNEX 等特殊影像模式，是否具有定量的診斷指標輸出？	"皆為定性及半定量分析"
Q15	生物相容性評估 (ISO 10993)	探頭 CMV1-10 的病患接觸路徑（皮膚接觸）是否符合 ISO 10993-1 要求的細胞毒性、致敏與刺激性測試？請說明。	"已由認證實驗室通過三項測試報告"
Q16	接觸材料與製程	探頭表面與人體接觸的聲學匹配層（Acoustic Matching Layer）及透鏡（Lens）使用之化學材料為何？	"醫學級聚氨酯 (Polyurethane) 與矽膠"
Q17	消毒與滅菌兼容性	本案擬申請的腔內（Trans-vaginal / Trans-rectal）探頭，可接受的高階消毒劑（如 OPA、Glutaraldehyde）之清單。	"支援 CIDEX OPA 及 MetriCide 消毒"
Q18	軟體確效等級	根據《醫療器材軟體確效指引》，HERA Z20 的軟體安全級別（Level of Concern, LoC）是屬於 Major、Moderate 還是 Minor？	"評定為 Moderate LoC (中等關切程度)"
Q19	軟體版本與架構	用於運作本超音波主機之軟體核心版本（如 V1.03.00）及主要操作系統（OS）環境為何？	"基於 Windows 10 Embedded Enterprise"
Q20	網路安全 - 安全登入	系統是否設有身分驗證、加密授權和存取控制機制（符合 2022 網絡安全範本）？	"具備 256bit 加密及三層權限管理"
Q21	網路安全 - 漏洞修正	對於已知的微軟 OS 安全性漏洞，系統出廠是否已套用補丁並提供遠端/本地安全更新之更新機制？	"出廠已預裝最新 Windows LTSC 補丁"
Q22	AI CADe/CADx 臨床功能	系統配置的 S-DETECT FOR 甲狀腺 / 乳房 AI 輔助軟體，是僅提供影像自動測量，還是能輸出惡性機率評估？	"僅提供邊緣勾勒與 BI-RADS 輔助分類"
Q23	AI 模型架構 (AI Models)	S-DETECT 的演算法主幹為何？（例如：是否基於 2D 卷積神經網絡 Convolutional Neural Network - CNN）？	"是的，基於 MobileNetV2 架構之 CNN 模型"
Q24	訓練數據集 (Train Data)	該 AI 模型（如 S-Detect）訓練集來源共包含多少家醫院的數據？以及多少例乳房/甲狀腺超音波影像樣本？	"包含 5 家醫學中心、12,000 張超音波標註影像"
Q25	人口統計多樣性	臨床訓練集中，是否包含亞洲女性及西方女性之乳腺成像數據？比例大概為何？	"亞洲女性佔 60%，西方女性佔 40%"
Q26	數據集獨立性	研發過程中，測試數據（Test Data）是如何與訓練與驗證數據進行物理隔離與時間隔離的？	"測試數據採用隨機獨立醫院留存，不參與訓練"
Q27	AI 臨床效能 (Non-Clin)	S-DETECT 對於乳腺結節良惡性預測的靈敏度（Sensitivity）、特異度（Specificity）與 ROC 曲線下之面積（AUC）實測為何？	"靈敏度 91.2%，特異度 85.4%，AUC 達 0.92"
Q28	統計信心區間	上述 AI 靈敏度與特異度在 95% 信心區間（95% Confidence Interval）的邊界數值分別為何？	"靈敏度 95% CI: 88.5%~93.8%"
Q29	AI 模型更新機制	上市後，若原廠針對 AI 功能進行權重調整或數據集追加，更新流程是否會觸發重新申報（510(k) Trigger）？	"若僅修正小幅權重而不變更適應症，則不需重新申報"
Q30	品質檢測與出廠品管	原廠品質檢驗報告中，出廠必檢測項目包括哪些？是否涵蓋高壓絕緣與探頭均勻度（Phantom Test）？	"包含 Phantom 原型測試、安全地阻與聲場校準"
互動 UI 特性設計：
分段進度條（Segmented Progress Bar）：30 題劃分成 5 個主題大卡（基本、效能安規、生物相容、軟體網安、AI/CAD），每完成一個主題，卡片即以 3D 翻轉（Motion 3D Flip）躍遷至下一組，消除答題疲勞。
AI 代答/提示按鈕（Predictive Auto-Fill）：如果用戶手頭沒有精確數據，可點擊「根據 K241971 自動推估」，系統會讀取 HERA Z20 公開的 510(k) Summary 進行智能填充，用戶僅需審查並確認。
3.2 問卷 Markdown 上傳、編輯與下載模組 (Questionnaire Template Module)
法規專員（RA）往往需要針對不同醫材更換問卷（例如：從超音波變更為骨科植入物）。本模組允許完全自定義這 30 道問題：
code
Code
+-----------------------------------------------------------------+
|                       問卷管理主面板                            |
|                                                                 |
|   +-------------------+  +-------------------+  +-----------+   |
|   |  選擇本地 .md 上傳 |  |   下載當前問卷    |  |  回復預設 |   |
|   +-------------------+  +-------------------+  +-----------+   |
|                                                                 |
|   [即時編輯區]                                                  |
|   # 510(k) 互動審查模板 - 30 題                                  |
|   1. [Group: 基礎資訊]                                          |
|      - Q1: 本設備與 K241971 的差異與架構設計是...               |
|      - Q2: ... (這裡支援 Markdown 實時寫作與預覽)                 |
+-----------------------------------------------------------------+
技術細節：
Markdown 解析邏輯：後端搭載自研 Markdown AST 剖析器（基於 remark）。它會掃描 Markdown 中的有序列表（1. ~ 30.）或特定前綴 -[ ] Q1:。解析成功後，動態轉換為前端問券卡片的 JSON State，不需冷啟動或重寫代碼。
錯誤容忍度機制（Robust Parser）：
如果上傳的 Markdown 內不足 30 題或格式毀損，AI 將介入
「自動格式化與校正（AI Auto-Healer）」：分析文檔內容，自動重構為 30 題標準矩陣，並提供「與原模板之差異比對」。
下載機制：前端利用 URL.createObjectURL(new Blob([markdownContent], {type: 'text/markdown'})) 實現無縫無伺服器延遲的本地 .md 文件導出。
3.3 510(k) 報告生成與珊瑚色渲染引擎 (Report Generation & "Coral" Rendering System)
在用戶填寫完 30 題（或上傳填寫好的數據）後，Agent 開始執行大規模的法規知識推理。本系統最卓越的創新在於**「珊瑚色（Coral, 十六進制：#F87171 的微調高亮背景色）增量高亮」**。
3.3.1 為什麼選擇珊瑚色（Coral）？
依照法規，在比對新案產品與對照器材時，必須凸顯當前新申請案的「特有變更」及「新提交數據（New Information）」。珊瑚色提供了視覺上的專業合規標記：既能區別於紅色的錯誤（Errors）和綠色的正確（Success），又具備極高的商用美學與法規警界性。
3.3.2 渲染實現技術：
在產出的精美 Markdown 文件中，所有因為用戶的回答而新增或變更的醫療器材技術段落，皆封裝在特定標籤或擴展語法中。
例如：
code
Markdown
此系統包含新款 CMV1-10 探頭，<span class="coral-highlight">該探頭實測軸向解析度達 0.45 mm，側向解析度達 0.8 mm，並完全符合 ISO 10993-1 所列之細胞毒性與致敏反應安全測試要求</span>。
在 React 的前端渲染端，我們精巧設定 @tailwindcss/vite 載入的主題色，並通過下述自定義節點解讀渲染：
code
CSS
@theme {
  --color-coral-base: #F87171;
  --color-coral-glow: rgba(248, 113, 113, 0.15);
}

.coral-highlight {
  background-color: var(--color-coral-glow);
  color: #DC2626; /* 深珊瑚紅以維持超高無障礙對比度 */
  border-bottom: 2px dashed var(--color-coral-base);
  padding: 0px 4px;
  border-radius: 4px;
  font-weight: 500;
}
3.3.3 生成算法 (AST Diffing)：
為防止 AI 全文重寫，失去原報告（如 HERA Z20 美國 K241971 上市許可報告）的基底骨架，生成過程採用 骨架模板融合算法 (Skeleton Template Integration)：
提取 K241971 原始審查報告與 TFDA 標準的骨架。
將用戶在 30 題中所回覆的具體參數（例如頻率、MI/TI 控制值、網安方案）作為語法槽（Slot）填入。
調用 Gemini API，以嚴格的 System Instruction 進行段落重寫與法規術語優化，並強制要求 Gemini 在重寫的所有「特定數據」外包裹 <span class="coral-highlight"> 與 </span> 標記。
驗證與校對程序：檢查標籤配對，確保不會發生 HTML 毀損或渲染坍塌。
3.4 雙模編輯器與多格式輸出系統 (Live Editor & Multi-Format Exporter)
3.4.1 Markdown 與 Preview 雙欄即時對照
採用雙欄側邊並列佈局（Side-by-Side Split View）。
左欄：代碼級高亮 Markdown 編輯器，支持自動縮排、行號與程式碼摺疊。當用戶直接修改 Markdown 代碼中的珊瑚色標記時，右欄即時預覽非同步更新。
右欄：採用 A4 紙張佈局仿真的「合規報告電子書面預覽（A4 Regulated Layout Viewer ）」，可調用 CSS 開關，一鍵「隱藏/顯示珊瑚色高亮」，方便法規主管進行最終打印審查與乾淨版本（Clean Version）的預覽。
3.4.2 頂級多端導出渠道 (Exporter Stack)
本平台規劃四種頂級導出通道，徹底打通辦公室協作生態圈：
code
Code
[報告生成完畢]
                                     |
         +-----------------+---------+---------+------------------+
         |                 |                   |                  |
         v                 v                   v                  v
    [Google Doc]         [PDF]               [HTML]           [Markdown]
  - OAuth 授權登入     - 伺服器 Puppeteer  - 前端 Blob 導出  - 前端 UTF-8 導出
  - 自動寫入 Docs      - 精巧 A4 封裝       - 自帶 Inline CSS- 附帶珊瑚色標籤
  - 保留珊瑚色排版     - 生成審查頁碼       - 開箱即視        - 兼容法規系統
此功能不再只是下載，而是真正呼叫 Workspace Drive & Docs RESTful API。
OAuth 授權：啟動 set_up_oauth 模組，取得 https://www.googleapis.com/auth/documents 與 https://www.googleapis.com/auth/drive.file 全權範圍。
格式轉換引擎（Markdown to Google Doc JSON Bundle）：
後端解析器將 Markdown AST 轉換為 Google Docs API 的 batchUpdate Request 結構體。
標題（Header 1, 2, 3） 映射為 ParagraphStyle: Heading 1。
表格（Table） 自動構建為 Docs Table Element。
珊瑚色標註段落 (Coral Highlight)：提取 class="coral-highlight" 區間，將其 Google Doc 背景顏色屬性設定為 backgroundColor: { color: { rgbColor: { red: 0.97, green: 0.44, blue: 0.44 } } }（相當於珊瑚色），同時前景色調暗以維護閱讀體驗。
無縫跳轉（Seamless View）：生成成功後，系統自動在 UI 彈出優雅提示框，提供連結「[一鍵在新視窗開啟您的 Google Doc 行動法規報告]」，極大加速多部門之間的在線協作審閱。
前端向後端 /api/export/pdf 發送當下 Markdown 內容。
後端在無頭 Chrome（Puppeteer）中載入含有 A4 精確排版樣式（@media print { @page { size: A4; margin: 20mm; } }）的 HTML 片段。
設定 Puppeteer pdf() 參數：displayHeaderFooter: true, 頁尾置入印件編號、時間與「第 1 頁，共 N 頁」的國際法規規格。
返回二進制 PDF 流，前端以 blob:application/pdf 下載，保證跨操作系統及各型號打印機時排版 100% 不跑位。
包含 Inline CSS、珊瑚色高亮開關 JS 腳本。
導出最純粹的 .md 源文件，完美兼容法務部現行使用的 GitHub / GitLab 歸檔管理或 TFDA 本地案件審理系統。
3.5 模型切換與動態交互 AI 提示詞引擎 (Model Registry & Dynamic Prompting)
系統整合最新的 @google/genai SDK。我們為法規專員提供最直觀的「AI 控制中樞（AI Control Deck）」：
預設模型：gemini-3.1-flash-lite (或 gemini-2.5-flash)，提供極速的 30 題反饋與大綱演算。
模型智囊選擇群（Model Select Matrix）：
gemini-2.5-flash（高性價比、流式反饋快速）
gemini-2.5-pro（深度複雜推理：適用於分析複雜的 ISO 10993 接觸路徑与 FDA 複雜指引）
gemini-1.5-pro（擁有超長上下文、可一次性載入多份 510(k) 歷史對照文檔）
隨時追問與引導 (Command Line Prompt Box)：
用戶在寫作到一半時，可在報告側邊欄呼叫 AI 指令對話盒。
例如輸入：“幫我將 CMV1-10 探頭的聲學不確定性，切換為符合歐盟 MDR 要求的極限標示法”。
AI 代理會立即依據指令，單獨重寫報告中的指定部分，並用珊瑚色對修改後的行區段進行高亮標註。
4. 5 + 3 項獨家 AI 魔法超能力功能 (Wow AI Features Detail)
為了將此應用打造成最具競爭力的 Agentic App，我們在其核心報告撰寫能力之上，嵌入了 5 項主功能以及 3 項擴展、共計 8 項「哇！好厲害（Wow）」的 AI 魔法功能。
4.1 五大核心 AI 魔法功能 (Core Wow Features)
✨ 魔法 1：FDA 拒收預測與Gap差距即時診斷警報 (FDA RTA Predictor & Gap Analysis Engine)
功能描述：模擬 FDA「拒絕接受（Refuse to Accept, RTA）」審查機制。
技術原理：後端將生成好的 510(k) 報告送與一個專門經由 FDA Premarket Notification (510(k)) RTA Checklist 指引調教的 Gemini AI 代理進行掃描。
用戶介面：在 UI 右側展示 0~100% 拒收風險儀錶盤。若發現報告中未提及「探頭對人體皮膚接觸的致敏試驗（Sensitization Test）」或「IEC 60601-2-37 的聲能輸出分級」，系統會立刻彈出紅色警告（Gap Alert），並提供一鍵「AI 自動補齊本漏洞」按鈕。
✨ 魔法 2：Predicate Device 智慧推薦與 Substantial Equivalence (SE) 對等關係映射器
功能描述：自動挖掘與尋求最佳的對照器材（Predicate Devices）。
技術原理：利用語義檢索（Retrieval-Augmented Generation）和公佈的 FDA 數據集。輸入超音波與探頭基本參數後，AI 自動計算與 HERA Z20 最等效的歷史申報設備（例如 K183421, K221045），並一鍵生成「實質等效性對照矩陣三元表 (SE Comparison Matrix)」，省去拉表格的繁重手工。
✨ 魔法 3：生物相容性材料數據庫自動映射與測試協議草擬器 (Biocompatibility & ISO 10993 Blueprint Generator)
功能描述：根據探頭在人體接觸的性質，自動繪製生物相容性合規地圖。
技術原理：當用戶在 30 題中回答接觸材料（聚氨酯、矽膠）及時間（<24小時 / 24小時至30天）。
輸出表現：AI 依據 ISO 10993-1 標準，自動在 Markdown 計算與編寫三大細胞毒性、致敏、內皮反應評估，並定制化生成「探頭清洗消毒相容性規格測試清單」，免除人工判讀與法規盲區。
✨ 魔法 4：聲學輸出極限模擬器與 MI/TI 超標預警系統 (Acoustic Performance Test Simulator & MI/TI Safe-Guarder)
功能描述：模擬並預測超音波探頭在極限高頻或高電壓脈衝下的 TI 與 MI 指數。
技術原理：用戶輸入探頭規格（如 10 MHz、最大發射角）。AI 預測在 Combined M-Mode + Color Doppler 下的局部熱聚焦。若計算出的 MI > 1.9，AI 會在報告中標記警示，並主動於 Markdown 中插入一段專業的「聲學衰減策略說明」以合理規避 FDA 在 21 CFR § 892 中的退件風險。
✨ 魔法 5：法規文字精煉與大師級語意轉譯器 (Premarket Medical Writing Polish & Expert Stylizer)
功能描述：一鍵將晦澀、零散、口語化的技術草稿，轉換為 FDA 審查官最愛、極高專業度的「精準醫材學術英語 / 法規文體」。
技術原理：此功能會將中英文摻雜、表達凌亂的描述（如：“探頭可以照比較深，側邊看得很清楚而且很安全”）重構為：“The diagnostic probe represents enhanced spatial and contrast resolution, optimizing penetration depths up to 15cm with superior lateral resolution (0.8mm) at focal point, ensuring mechanical and thermal index limits remain beneath FDA safety parameters”。
4.2 三大額外 AI 魔法功能 (Additional Wow Features)
✨ 魔法 6：AI 醫療智慧網路安全威脅矩陣與 SBOM 自動草擬器 (Cybersecurity Threat Matrix & SBOM Drafter)
功能描述：針對醫材日益受到重視的網絡安全規章（FDA Cybersecurity 2023 最新指南），自動起草威脅矩陣與軟體物料清單（SBOM）。
技術原理：根據用戶回答的主機 OS（Windows 10 Embedded）與網絡特點（有 WiFi，支援 PACS 傳輸）。
產出表現：AI 會隨機生成一組含有 CVE 漏洞應對、加密協議、安全更新週期及反惡意軟件防範 的標準網絡安全矩陣表（Cybersecurity Threat Matrix Table）直接嵌入報告中，並用珊瑚色優雅呈現。
✨ 魔法 7：一鍵 FDA 官網數據存取與 Predicate K-Number 實時匹配對照器
功能描述：利用即時搜索（Search Grounding），即時上網爬取美國 FDA 官網資料庫，對比該 K 案號在 FDA 登載的最新 510(k) Summary 狀態。
技術原理：集成 Google Search Grounding。每當用戶在報告或 30 題中寫下 K241971 或其他 Predicate 案號時，AI 會實時上網抓取並核對該案號背後的 Predicate Device 廠牌、核准日期、是否被撤回（Recall Status）等最新即時市場監管實況。
✨ 魔法 8：法規跨國雙向智慧對譯與專有名詞校驗引擎 (Regulatory Localization & Terminology Guard)
功能描述：繁體中文（TFDA 臨床前基準語境）與英文（FDA Premarket Notification 指引語意）之間的完美的跨國雙向法規翻譯。
技術原理：它不同於一般的普通 Google 翻譯，而是內置了中英文「法規核心術語比對字典」（如：將“實質等效性”精準對應為 “Substantial Equivalence”，將 “熱指數” 對應 “Thermal Index (TI)”，而非 “Hot Index”）。在翻譯的同時，自動核查英文拼寫、單位格式（如 MHz、mW/cm²），並提示語法一致性，從源頭保證 510(k) 申報書的國際品質。
5. 使用者體驗與介面設計 (UX/UI Design Platform)
為了使該系統給人眼前一亮、極具質感的「Wow」視覺張力，我們拒絕使用一切平庸的模板，轉而打造一個「智動法規實驗室（Agentic Reg Studio）」的極簡、高對比現代美學設計。
5.1 視覺美學方針
色彩設定：
網頁背景：採用「極簡淺灰白色系 (Minimalist Slate Off-White)」及「高對比深炭灰 (#15171C) 」相互輝映。
主要調色 (Primary Accord)：深黑、寶石藍（象徵專業法規嚴謹性）。
高亮/新內容色 (Highlight Palette)：珊瑚色（Coral, #F87171 系列），具備溫暖而亮眼的晶體光芒，搭配輕微羽化的珊瑚底影背景。
字型運用：
大標與卡片標題：採用 Space Grotesk，極具未來前沿科技感。
報告正文與數值指標：採用 Inter 搭配 JetBrains Mono，將超音波探頭參數渲染得極致規整，宛若精密儀器輸出。
微動畫與微交互：
卡片切換：利用 motion/react 打造極致柔順的彈性物理效果，答題卡片在滑動、完成、翻轉時伴隨細微的「呼吸感 (Breathing Animation)」。
AI 生成中：珊瑚色文字在生成時，會以「語義粒子緩慢凝聚 (Soft Micro-fade Typing)」的特效微漸進呈現，帶給用戶極強的「智慧正在思考並編寫」的視覺爽感。
6. API 與資料流細節規範 (API & Data Flow Specifications)
系統在運作時，主要有三高危數據傳輸流：問券配置上傳、Gemini 法規推導、Google Docs 自動化寫入。
6.1 後端 /api/generate/report 端點 Payload 規格
Method：POST
Request Body：
code
JSON
{
  "answers": [
    {"qId": "Q1", "text": "是的，HERA Z20 與 R20 採用相同的主機箱體板結構"},
    {"qId": "Q2", "text": "預期用途一致，移除部分不適用之臨床場景"}
    // ...共 30 題
  ],
  "modelSelected": "gemini-2.5-pro",
  "aiMagicsEnabled": ["fda_rta_predictor", "cybersecurity_sbom"]
}
處理流程：
驗證 answers 陣列。若缺失某些關鍵問題回覆，AI 啟動預填充邏輯。
調用 @google/genai 的 ai.models.generateContent。
載入法規引導 System Instruct：
code
Text
你是一名資深的美國 FDA 510(k) 兼台灣 TFDA 醫療器材審查專家。
根據提供的 30 題回答，編寫一份 3000~4000 字、結構極其嚴謹的傳統中文 HERA Z20 510(k) 審查與補件覆回報告。
所有根據回答最新生成的產品特定核心數據、缺失補齊段落、法規聲明，你必須使用 <span class="coral-highlight">最新數值與論述</span> 將其包裹。
流式返回並將數據寫入客戶端 Markdown 框架中。
6.2 /api/export/googledoc 寫入流程
用戶在前台點擊「一鍵寫入我的 Google Doc」。
用戶重定向至 Google OAuth Consent 畫面 (由系統引導安全登入)。
前台獲得 Access Token，後端建立 google.drive 與 google.docs Client。
在用戶的「My Drive」中建立名為 HERA_Z20_FDA_510k_Review_Report_Draft.docx 的全新文件。
驅動 Markdown DOM 樹解析，執行 batchUpdate：
insertText：批量插入乾淨文字。
updateTextStyle：掃描珊瑚色部分，執行 Color: #DC2626、Background: #FEE2E2。
將生成文檔之 webViewLink 交付給前端，前端在 UI 端彈出極其精美的圓角對話窗，向用戶祝賀。
7. 系統合規性、隱私與安全性 (Regulatory Compliance & Security)
由於本平台經手的是極其敏感的醫療器材研發參數與上市前核心文件，因此技術安全級別甚至高於一般商務軟體：
端到端加密 (HTTPS/TLS 1.3 - AES256)：所有傳輸皆受高等級加密保護。
零內部硬盤留存 (Stateless Compute)：對用戶的 30 題作答原始數據與上傳的 Markdown 模板，本系統不提供任何持久化、雲端數據庫硬盤留存。所有計算皆在內存（Memory-Only）中完成，並在 Docs 導出或 PDF 下載後隨瀏覽器會話清除。這 100% 杜絕了原廠商業機密（Trade Secrets）洩漏與模型被惡意竊取研發思路的可能性。
Gemini 數據隐祕政策 (Data Privacy for AI)：本系統呼叫 Gemini API 時，強制啟用「無訓練模式」，通知 Google 模型不得使用此批極其高貴、敏感的醫材技術參數去二次訓練它的公共地基模型。
8. 20題深度追問與討論問題 (20 Comprehensive Follow-up Questions)
為了配合接下來的高級開發流程、協助您與原廠、法規團隊及開發主管展開更深層次的架構商討，本設計書針對技術實現、法規考量、AI 模型泛化性三大邊界，提出 20 個深度核心討論問題：
問卷擴展性：如果原廠需要將此系統應用於骨科關節植入物或心血管導管等「非超音波、無 MI/TI 等指標」之器材，系統模板引擎應如何設計才能確保在一秒內智能過濾、調整，更換成符合 ISO 14971 及對應指引的 30 題？
珊瑚色增量判定：如果用戶在 Markdown 編輯器內手動刪除或添加了一些文字，我們在後台如何利用「精準 AST 樹差分算法 (Abstract Syntax Tree Diffing)」去動態修復並自動在這些增量段落上補齊 <span class="coral-highlight">，而非破壞原本的 Markdown Layout？
FDA RTA 規則持續更新：模擬 FDA RTA 的 Gap 診斷引擎，在未來 FDA 發布 510(k) 指引新草案（如 2027 年版）時，本系統如何在不重構代碼的前提下，讓法規人員通過上傳「法規知識庫 PDF」實現即時規則更新？
Google Docs 格式逼真度：當 Markdown 包含極端複雜的三維表格（如 HERA Z20 探頭的聲學輸出矩陣）及多層次嵌套列表時，在導出至 Google Docs 的過程中，字體縮排、線寬、儲存格寬度等該如何進行精確換算？
PDF 跨國字體分級：Puppeteer 將 Markdown 的 Traditional Chinese 轉換為 PDF 時，若要保證在 Docker 容器（Cloud Run 環境）和無本機中文字型支持的环境下仍能 100% 渲染繁體中文「微軟正黑體」與「思源宋體」，後台字體靜態包與 CSS @font-face 該如何加載與管理？
Gemini 多輪對話控制：當用戶使用「AI 魔法側邊欄（Model Prompt Deck）」對局部段落進行不斷微調時，我們如何設計 Chat Session 歷程與 context limit，才能確保 AI 精煉時只引用當前編輯的上下兩段，而不致使全文崩潰和重新覆蓋珊瑚色高亮？
無數據庫持久化之 Session 緩存：由於本系統秉持 0-Database Privacy 戰略，若用戶答題到第 25 題時瀏覽器不慎發生崩潰 crash 或斷連，我們應如何設計 Client-Side 加密型的 IndexedDB 或 Session Storage 的自救救援策略？
AI 幻覺控制（Hallucination Control）：由於生醫安全不允許任何胡謅，如果用戶對探頭的軸向解析度作答 “123.456 mm” 的荒謬數值，AI 是否應設有「法規物理限值常識層 (Sanity Gate)」去主動截獲該異常，並發出強烈的合規警告？
探頭生物相容性物料深度映射：針對 ISO 10993，若探頭增加了保護套（Sheath）或偶合劑等三方耗材接觸，系統在生成生物相容合規地圖時，如何引導用戶回答耗材批號、符合聲學穿透物理性能？
網絡安全 SBOM 合規格式：魔法 6 自動生成的 SBOM 目前是 Markdown 表格式，是否有必要導入並支持國際正式網絡安全標準 —— SPDF / CycloneDX JSON 規格以供 FDA 電子申報自動解析？
實時官網爬取（Google Search Grounding）的安全頻譜：大師魔法 7 前往美國 FDA 官網即時搜取對照器材的資料，如果遇到 FDA 網站加設了反扒爬蟲協議（Cloudflare Verify），我們在代理端和 Gemini Grounding 端有沒有備用的 API 或 Cached DB 來維持搜尋生命線？
多模型輸出性能瓶頸與速率限流（Rate Limit）：如果用戶切換到 gemini-2.5-pro 執行極端龐大的 510(k) 深度推理，而面臨 Google API 超時超額限制（TPM/RPM 限流），我們在後端是否需要為專員提供「進度排隊懸停與降級」的非同步隊列 UI？
雙向對譯專業名詞庫可自訂性：生醫顧問公司 RA 常有其各自慣用或內部的字詞庫，魔法 8 在中英文翻譯與術語校验時，是否應該提供一個 RA 專屬語彙 Excel 詞庫的上傳功能？
HTML PDF 中 A4 頁碼切割難題：Markdown 的章節長短不一，如果在用 Puppeteer 切割 A4 頁面時，剛好把「探頭聲明表格」切在半中腰、造成表格跨頁毀損。我們是否應在 HTML 中設計 page-break-inside: avoid 等 CSS 阻隔規則？
問卷 AST 容錯校正：當用戶上傳的 Markdown 格式极度不規範，例如本應該是問題的行，寫成了普通文本，或者順序被打亂成 Q9, Q1, Q15...我們的 AI Auto-Healer 算法底層將如何通過 Embedding 相似度匹配將它們對齊回 30 題框架？
對照器材 Substantial Equivalence (SE) 的多對一對照：HERA Z20 往往不只和一個 Predicate 產品比對（可能同時與上一代 HERA W10 及 GE Logiq E10 對比），我們的 SE Mapping 魔法二應如何調整生成架構以支持「多 Predicates 主動比對模式」？
在線 Google Doc 權限管理：導出 google doc 後，為保障法務隱私，建立的文件其預設分享設定（Sharing Permission）是否應限定為「僅有發起 OAuth 之用戶帳戶可讀，不得公開於網絡」？
CADe 以及 CADx 功能之輸出邏輯驗證：針對超音波 AI 輔助軟體，指引中高度關切「輸出邏輯（Output Logic）」和「臨床操作工作流」。系統在 30 題的 AI 構面中，應引導用戶上傳哪些關鍵界面截圖或用戶手冊敘述，才能滿足 FDA § 807 的查驗登記需求？
多語言排版之字體度量衡一致性：Traditional Chinese 的寬度一般是英文單詞的兩倍以上，在轉譯與雙語排版時物料看板、表格文字常會爆炸擠壓。頁面是否應引入 Fluid Layout 設計來維持一致性的美學節奏？
系統上線 CI/CD 驗證機制：要確保這套複雜的 Node/Express & React 510(k) App 在 Cloud Run 每次小改動部署均能正常構建，我們是否需要建立一個專用於 @google/genai Mock 答題的測試集腳本，來自動跑完 30 題看是否會產生 A4 A級報告 PDF？
