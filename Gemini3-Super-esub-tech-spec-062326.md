# 醫療智慧監管系統：基於 Agentic 智慧協同與雙向 Markdown 互動的 FDA/TFDA 510(k) 查驗登記審查系統與 30 問答、8 大 AI 神奇功能之技術規格說明書

**版本 (Version):** 2.0.0-PRO  
**目標系統環境 (Target Workspace):** React 19 + Express 滿版 Full-Stack 軟體  
**主要大語言模型引擎 (Primary Engine):** `gemini-3.1-flash-lite` (預設使用且支援更換型號)  
**格式標準 (Format):** Markdown 雙向數據流同步與多格式本地編譯  
**輸出語言 (Language):** 繁體中文 (Traditional Chinese - zh-TW) 與關鍵法規專有名詞英文對照  

---

## 1. 系統設計願景與核心哲學 (System Vision & Design Philosophy)

在醫療器材查驗登記的生命週期中，準備並審查一份符合「美國 FDA 510(k)」與「台灣 TFDA 電子送審 (e-submission)」標準的技術報告，向來是一項高成本、高出錯風險、且對專業法規經理（RA）極度依賴的工程。

本「MedAgent FDA-Submit 智慧監管系統」旨在跳脫傳統法規軟體單純進行文字存取的靜態框架，將整個 510(k) 審查流程（Technical Review Report）轉化為一個**「動態雙向交互式法規引擎」**。系統的核心設計哲學基於以下四大支柱：

1. **問答導向的材料溯源 (Question-Driven Traceability)**：不要求用戶從零開始編寫數百頁的報告，而是系統化地提出 **30 道涵蓋安全性、有效性與演算法效能的核心查驗問題**。用戶的回答直接決定了技術報告的深度與就緒度。
2. **雙向 Markdown 生態系統 (Bidirectional MD Ecosystem)**：引入全新的「問題模板編輯模組」，支持用戶在 UI 中上傳、即時修改與下載 Markdown 格式的新舊問答集。同時，生成的 3000 到 4000 字 510(k) 審查報告亦在 Markdown Canvas 視圖中完全可編輯，實現「修改問答即更新報告，修改報告能反向標記」的高效閉環。
3. **珊瑚橙色彩標註系統 (Coral HIGHLIGHT Indicator)**：所有由 AI 演算法生成、經由用戶反饋後動態修正、或經由 Wow 功能一鍵補修（Magic Patch）的全新或變更內容，均會在 Markdown 視圖與導出文檔中以**珊瑚橙色 (Coral Color, 樣式代碼：`<span style="color: coral">...</span>`)** 像素級標記，確保審查官或 RA 能一眼辨識出增補後的安全評估文字。
4. **8 大 AI 充能魔法 (The 8 WoW AI Magics)**：整合 5 個核心 AI 交互特色與 3 個全新開發的深度法規評估特徵，全面涵蓋知識圖譜（Knowledge Graph）、對抗式模擬審查官（PRQ Sim）、自動補丁差分、通關機率預算、標準解析映射、生物相容統計分析、AI CADe/CADx 模型漂移與網路安全 SBOM 特性，利用 `gemini-3.1-flash-lite` 的超低延遲和強大上下文性能進行實時推理。

---

## 2. 30 道 510(k) 審查核心引導問答集設計 (30-Question Assessment Blueprint)

系統為了對診斷式超音波系統（以 Samsung Medison HERA Z20 為本案受測對象， clearance 參照 K241971）做出全方位就緒度評估，技術層面歸納出 30 個精準法規問答。這些問題可以用 Markdown 格式導入、編輯並導出：

### 2.1. 基礎技術與法規宣告 (Q1 - Q5)
*   **Q1 [法規主機與型號界定]**: 本次 TFDA/FDA 申報是否僅包含 Samsung Medison 超音波診斷系統之單一型號 HERA Z20？若 K241971 包含 HERA Z20, R20, HERA Z30, R30 多個型號，需說明本案僅申報單一型號之技術邊界與不影響等效性之理由？
*   **Q2 [臨床預期用途劃分]**: 請確認 HERA Z20 的預期用途（Intended Use）是否完整涵蓋：胎兒/產科、腹部、婦科、手術中、小兒科、小器官、新生兒頭部、成人頭部、經直腸、經陰道、肌肉骨骼、泌尿科、成人心臟、小兒心臟、胸部、經食道以及周邊血管？是否有未涵蓋之潛在臨床風險？
*   **Q3 [探頭型號與規格清單]**: CMV1-10 與 CMV1-10Z 兩款新款高頻探頭，在產品說明書中註明的中心頻率、操作頻帶、針導引夾具規格，是否與母案 K241971 核准規格完全一致？
*   **Q4 [等效切入點對比]**: 與前代或等效器械相比，HERA Z20 採用的數位波束合成（Digital Beamforming）與脈衝都卜勒技術，在信號處理速度與最大成像深度上是否有顯著變更？
*   **Q5 [法規指引適用性核對]**: 系統是否已將 2023 年 FDA 最新版 Guideline "Marketing Clearance of Diagnostic Ultrasound Systems and Transducers" 作為本次申報的主要符合性標準？

### 2.2. 電氣安全與電磁相容性 (Q6 - Q10)
*   **Q6 [IEC 60601-1 安全測試]**: HERA Z20 是否檢附第三方 Nemko Korea 出具、適用最新 IEC 60601-1:2025 標準的完整安全測試報告？報告中是否有任何在特殊電應力測試下的不適用或排除條款？
*   **Q7 [IEC 60601-1-2 電磁相容]**: 對於電磁相容性（EMC）標準，本系統提供的是 IEC 60601-1-2:2014 還是更高等級的 2024 年版測試數據？是否針對手術室高頻電刀干擾做出評估？
*   **Q8 [漏電流與接地阻抗極限值]**: 針對 HERA Z20 探頭接觸患者部分（Patient Applied Part），其微安培（µA）等級的漏電流是否符合 Type BF 或 Type CF 安全容許上限？
*   **Q9 [基本性能要求 (Essential Performance)]**: 在電磁干擾環境下，系統如何定義其「基本性能要求」？例如是否會發生超音波影像不可逆凍結、雜訊失真度超標或探頭表面溫度漂移？
*   **Q10 [環境適應性試驗]**: 主機在中文說明書標示之工作溫度下，是否檢附高溫高濕耐久運轉測試報告，以確保臨床使用的安全不打折？

### 2.3. 超音波專屬安規與聲場輸出 (Q11 - Q15)
*   **Q11 [IEC 60601-2-37 特殊安規]**: 針對 HERA Z20 主機及其所搭配的 CMV1-10、CMV1-10Z 探頭，是否檢附 IEC 60601-2-37（超音波診斷與監控設備特定安全要求）的完整型式檢驗報告？目前原廠文件是否存在此 [GAP]？
*   **Q12 [聲學輸出最大值宣告]**: 本系統在各操作模式下（如 2D, M, Doppler, TDI, MV-Flow, Elastoscan+），其機械指數（MI）最大值與熱指數（TIB/TIC/TIS）之最大值是否分別低於 FDA 規定的 1.9 與 1.0 上限？
*   **Q13 [IEC 62359 聲學參數確定]**: 主機所採用的聲場特徵測試方法，是依據 IEC 62359 標準還是美國 NEMA UD 2-2004 標準？兩款新探頭的最大強度位置及波束寬度數據是否齊全？
*   **Q14 [聲功率即時顯示機制]**: 當探頭聲輸出超過特定閾值時，HERA Z20 螢幕上是否能即時、準確地顯示 MI 與 TI？其量測不確定度是否控制在 ±15% 以內？
*   **Q15 [ALARA 臨床聲輸出原則]**: 說明書中是否明確包含指導臨床醫師在維持最低可達影像品質的前提下，盡可能降低患者聲暴露量的 ALARA（As Low As Reasonably Achievable）指南？

### 2.4. 探頭生物相容性評估 (Q16 - Q20)
*   **Q16 [ISO 10993-1 風險評估]**: 本案所配之 CMV1-10 及 CMV1-10Z 探頭，屬於與黏膜或破損皮膚短暫接觸（<24h）之器材。其 ISO 10993-1 生物相容性評估報告是否齊全？目前是否存在原廠報告未檢附之限制？
*   **Q17 [細胞毒性與致敏性測試]**: 探頭外殼與聲透鏡（Acoustic Lens）接觸材質是否通過 ISO 10993-5（細胞毒性）與 ISO 10993-10（刺激與遲發型超敏反應）測試？
*   **Q18 [皮內反應試驗 (Intradermal Reactivity)]**: 是否針對所有可能接觸人體之黏膜探頭（例如經陰道、經直腸應用）進行了 ISO 10993-11 的全身毒性或皮內反應測試？
*   **Q19 [化學溶出物分析]**: 兩款高頻探頭其封裝點膠及塑料件在長期清洗/高溫環境下，是否有化學單體或塑化劑溶出之風險？
*   **Q20 [臨床消毒耐受度验证]**: 說明書中推薦的化學化、液態化高階消毒劑（如 Glutaraldehyde）對探頭外殼之生物相容性完整性是否有長期腐蝕性評估？

### 2.5. 軟體驗證與網路安全 (Q21 - Q25)
*   **Q21 [IEC 62304 軟體生命週期]**: HERA Z20 系統所內嵌之超音波控制軟體，其軟體安全等級（Software Safety Class）被列為 Class B 還是 Class C？是否檢附完整 IEC 62304 軟體架構與生命週期開發文件？
*   **Q22 [異常管理與錯誤追蹤]**: 軟體驗證報告（Software Validation Report）中，對於可能導致成像中斷、影像凍結等 Bug，其未解決異常（Unresolved Anomalies）之風險評估與緩解方案是否齊備？
*   **Q23 [SOUP 外部軟體組件評估]**: 本系統使用的第三方軟體或開放原始碼組件（SOUP）是否有對應的風險控制、安全漏洞補丁機制與版本控管說明？
*   **Q24 [網路安全威脅模型分析]**: HERA Z20 支持 DICOM 圖像傳輸與醫院 PAX 系統相連。是否依據台灣《適用於製造業者之醫療器材網路安全指引》與 FDA 網路安全新規，檢附網路安全威脅模型分析（Threat Modeling）與漏洞補救報告？
*   **Q25 [軟體 SBOM 清單]**: 系統是否提交了軟體物料清單（SBOM, Software Bill of Materials），描述所有軟體模組及其已知的惡意軟體防範與權限金鑰設計？

### 2.6. AI 演算法與電腦輔助偵測/診斷 (Q26 - Q30)
*   **Q26 [AI 功能群組定義]**: HERA Z20 中標榜的 AI 功能包括 ViewAssist, Live ViewAssist, HeartAssist, EzVolume，其是否屬於電腦輔助偵測/診斷（CADe/CADx）範疇？其演算法輸出邏輯與臨床決策鏈的關聯是什麼？
*   **Q27 [演算法架構與核心架構]**: ViewAssist 與 HeartAssist 等模型，是基於卷積神經網路（CNN）還是循環神經網路（RNN）開發？使用的深度學習框架與關鍵超參數設定為何？
*   **Q28 [數據集規模與外部驗證]**: 用於訓練與驗證 AI 模型之數據集，規模為何？共包含幾家醫療機構、多少位患者的超音波掃描影像？標註人員（Annotator）的臨床資歷如何？
*   **Q29 [數據獨立性與防過擬合]**: 如何保障測試數據集（Test Dataset）與訓練集（Training Dataset）、驗證集（Validation Dataset）在機構、患者、乃至掃描時間上的絕對獨立性？是否有效消除了模型過擬合（Overfitting）與數據偏見？
*   **Q30 [模型漂移與上市後更新機制]**: 當面對不同人種、年齡或不同探頭老化程度導致的模型輸出準確度漂移（Model Drift）時，原廠是否有定期監控模型表現並依據臨床反饋進行上市後軟體靜態更新的標準流程？

---

## 3. 雙向 Markdown 互動式問答與報告模組設計 (Dynamic Markdown Modules)

為了讓上述 30 道核心問答與最終生成的審查報告具備極佳的靈活性，本系統設計了兩個交互式核心組件。

### 3.1. 30 道問答 Markdown 編輯與上傳下載模組

在系統中，這 30 道引導問題並非固化在代碼中，而是由一個獨立的 **「Q&A Markdown 範本引擎」** 進行動態加載。

```
+-------------------------------------------------------------+
|               Questions & Answers Config Module             |
+-------------------------------------------------------------+
| [ Drag & Drop / Upload MD File ] [ Download Current QA.md ]|
|                                                             |
|  # Q1 [法規主機與型號界定]                                    |
|  * Question Text: 本次申報是否僅包含 HERA Z20 單一型號...?   |
|  * [Edit Input Box: ]                                       |
|    "是的，雖然原 FDA 510(k) (K241971) 涵蓋 HERA Z20, R20 等  |
|     多個型號，但因台灣市場策略，本次 TFDA 查驗登記僅限 HERA   |
|     Z20 單一主機。未申報型號之技術變更已在等效性報告中隔離..."|
+-------------------------------------------------------------+
```

*   **上傳模組 (Markdown Parser)**：用戶可以將本地編寫好的 `.md` 問答對文件拖曳上傳。系統會解析 Markdown 發音符號與二級標題 `## Q[1-30]`，自動將內容映射到系統內置的 Q&A 輸入欄位。
*   **在線修改 (Live Config Engine)**：用戶可在網頁表單中逐條修改問題陳述與已答內容，系統內置的 React 狀態管理器會即時重新快取表單的 JSON 數據結構。
*   **導出與下載模組 (MD Generator)**：修改後，用戶點擊「匯出 Q&A 模板」，系統將自動生成標準 Markdown 文檔，方便用戶歸檔或在其他編輯器（如 Typora, VS Code）中查閱。

### 3.2. 雙向同步編輯與珊瑚橙色（Coral Color）渲染引擎

當用戶完成 30 問答後，點擊「執行全面審查」，AgentSwarm 會呼叫 `gemini-3.1-flash-lite` 引擎，參考 `skill.md` 對回答進行綜合推論，並產出一份 **3000 到 4000 字的 Traditional Chinese 510(k) 審查報告**。

*   **雙向 Markdown 編輯 (Dual-Sync Canvas)**：
    *   本頁面將分為兩個視圖：**「Markdown 編輯碼視圖」** 與 **「渲染預覽視圖」**。
    *   用戶點擊 Preview 報告中的任何段落，即可對其進行編輯，系統底層的 AST（抽象語法樹）編譯器會即時在背景進行渲染。
*   **珊瑚橙（Coral Color）變更內容標記演算法**：
    *   **核心規則**：所有**非原始導入文字、由 AI 後續生成插補（Wow-Magic Patch）、或由用戶在二輪 Prompting 中更新的全新技術描述**，其容器節點均會被賦予 HTML 標籤 `<span style="color: coral">內容...</span>` 或 CSS 類名 `text-coral-500`。
    *   在 Markdown 編輯器中展示為：
        ```markdown
        ### 4. 生物相容性評估審查
        本案 CMV1-10 探頭之表面接觸材質包含聚氨酯和醫療級矽膠。<span style="color: coral">為澄清先前缺失，原廠已對該材質進行 ISO 10993-5 細胞毒性及 ISO 10993-10 刺激性測試，其學術研究支持在接觸時間小於 24 小時內，無顯著細胞毒性與過敏反應。</span>所有安全評估報告均已歸檔於 Appendix C。
        ```
    *   在 HTML 預覽與最終導出的 PDF/Word/MD 格式中，這段文字會呈現為引人注目的**珊瑚橙色（Coral）**，象徵此段內容為本次對抗審查後重新補修的關鍵性安全宣誓。

---

## 4. 3000-4000 字 Traditional Chinese 510(k) 審查報告範本 (Sample Comprehensive Report)

以下為系統根據 30 問答及 HERA Z20 等效性差距（GAP）自動生成的正式 510(k) 技術審查報告（內含珊瑚橙補丁文字標記示例）：

---

# 510(k) Technical Review Report (FDA-TFDA 5k-eSub-HERA-Z20)
**審查日期 / Date:** 2026-06-23  
**主機型號 / Device Model:** HERA Z20  
**母案申請編號 / Predicate 510(k) No.:** K241971 (Samsung Medison Co., Ltd.)  
**法規承辦單位 / regulatory Body:** 衛生福利部食品藥物管理署 (TFDA) 第一筆審查 & 美國 FDA 510(k) 查驗登記審核對照  

---

### 一、 審查背景與產品申報邊界 (Executive Summary & Submission Scope)

本件查驗登記案為自主申報之新申請案，申報產品為南韓三星電子醫療子公司 Samsung Medison 所研發之「超音波診斷系統 (型號：HERA Z20)」。經法規組比對，本案之產品主機已於日前取得美國 FDA 510(k) 上市許可（K241971）。

然而，必須指出之關鍵邊界在於：**原美版 510(k) (K241971) 許可函所涵蓋之超音波主機包含 Samsung Medison Ultrasound Systems 下的多個產品型號，包含 HERA Z20, R20, HERA Z30, R30；而本案本次送審之中文說明書與申報規格，其目的「僅包含其中之單一型號規格 (即標的型號：HERA Z20)」**。

本報告針對 HERA Z20 的診斷超音波成像、體液影像分析之預期用途（包含產科、腹部、婦科、小兒、小器官、心臟、周邊血管等 17 項臨床應用），結合美國 FDA 指引《Marketing Clearance of Diagnostic Ultrasound Systems and Transducers (2023)》及台灣 TFDA《診斷用超音波影像系統暨超音波轉換器臨床前測試基準》開展全面性一致性審計（Concordance Review）。

<span style="color: coral">【新補行評估文字】經調閱原廠 K241971 申報卷宗，確認 HERA Z20 與美版 R20, Z30 採用完全相同之核心波束生成主控板與一體化電源濾波器晶片。本案僅申報 HERA Z20 單一型號，主要係因台灣市場之常規推廣策略；非申報型號之訊號採樣頻率與軟體安全防護機制，已在等效性邊界報告（Section 2.1.2）中進行了物理性與程式邏輯上的有效隔離，不影響 HERA Z20 之安全與等效效能。</span>

---

### 二、 適用標準與產品法規矩陣 (Applicable Regulatory Standards)

本案超音波診斷器械之安全與有效性設計，應符合並通過以下國際與本土協和標準（Harmonized Standards）之檢驗與考核：

1. **基本電性安全基準**: `IEC 60601-1:2025` 醫療電氣設備 - 第一部分：基本安全與主要性能之通用要求。
2. **電磁相容相容性**: `IEC 60601-1-2:2024` 醫療電氣設備 - 第1-2部分：電磁干擾試驗與防護要求。
3. **超音波專用安全基準**: `IEC 60601-2-37` 醫療電氣設備 - 第2-37部分：超音波診斷與監控設備安全性之特定要求。
4. **聲位輸出特徵測量**: `IEC 62359` / `NEMA UD 2-2004` 聲場特徵判定與機械指數 (MI)、熱指數 (TI) 計算標準。
5. **探頭生物相容性**: `ISO 10993-1` 醫療器材生物學評估 - 第一部分：風險管理程序。
6. **醫療軟體生命週期**: `IEC 62304` / 《醫療器材軟體確效指引》 Class B 級別全生命週期確效。
7. **醫療網路安全評估**: 《適用於製造業者之醫療器材網路安全指引》（2022年版）威脅建模。
8. **人工智慧電腦輔助診斷**: 《人工智慧/機器學習技術之電腦輔助偵測(CADe)及電腦輔助診斷(CADx)醫療器材查驗登記技術指引》。

---

### 三、 核心查驗重點與差距分析紀錄 (Technical Gaps & Audit Record)

本法規團隊針對本案技術資料（Technical Dossier）進行逐項查驗，並與中文說明書及 FDA 許可範圍對照，發現以下 5 大核心 [GAP] 缺失，急需原廠補足：

#### [GAP-1] 電氣安全與聲場安全檢驗报告之瑕疵 (IEC 60601-2-37 & IEC 62359)
*   **現狀記錄**: 申報資料中檢附了 Nemko Korea 出具的 `IEC 60601-1:2025` 測試報告（證號：N-192735）與 `IEC 60601-1-2` EMC 報告。
*   **缺失評估**: **[不符合 / MAJOR RISK] 卷宗內未檢附「本案擬申請 HERA Z20 主機及本次搭配探頭之超音波設備特殊安全性基本要求 (Particular requirements for the basic safety, IEC 60601-2-37、IEC 62359) 測試評估報告」。**
*   **法規要求**: 原廠必須提供所有搭載在 HERA Z20 上的探頭（含 CMV1-10 與 CMV1-10Z）在 B-Mode、Color Doppler、TDI、MV-Flow 及 Elastoscan+ 模式下的熱指數（TI）及機械指數（MI）最大聲學輸出測試數據，且測量儀器不確定度必須符合標準。

<span style="color: coral">【Wow 自動修正補丁】原廠於 2026 年 6 月 20 日補正並提交了 Nemko 出具之 HERA-IEC-60601-2-37 特殊安全測試報告（報告編號：NK-26-E0821）。測試結果證實：在全負載能量都卜勒（S-Flow）模式下，高頻探頭 CMV1-10 發射之最高聲學機械指數（MI）為 1.2（低於上限值 1.9），肌肉骨骼應用之最大熱指數（TIS）為 0.45（低於上限值 1.0）。探頭表面在連續激勵 30 分鐘後之最高升溫點為 41.2°C，符合標準中「接觸患者部分溫度不高於 43°C」之硬性限制，安全性達標。</span>

#### [GAP-2] 探頭生物相容性安全報告不全 (ISO 10993-1)
*   **現狀記錄**: 說明書中列載了多款可用探頭，並申報了最新研發之 CMV1-10 以及 CMV1-10Z 兩款高頻探頭。
*   **缺失評估**: **[不符合 / BLOCKING DEFICIENCY] 未檢附本次擬申請全部探頭之生物相容性評估報告。**
*   **法規要求**: 探頭之透鏡與護套直接接觸患者，必須提交依據 ISO 10993-1/5/10 標準的實驗室原廠毒性測試。

<span style="color: coral">【Wow 自動修正補丁】針對此缺失，申報代理人已補正並載入完整的 ISO 10993-1 生物相容性卷宗。該卷宗包含了 GLP 認證實驗室（KTR Lab）出具之體外細胞毒性（Cytotoxicity，MTT 法）報告（報告號：KTR-2025-0925），細胞存活率為 94.2%（大於評估合格限 70%）；皮膚致敏（Sensitization，LLNA 法）刺激係數低於 0.5（無致敏物特徵）；及皮內反應評估，證實 CMV1-10 及 CMV1-10Z 之皮膚直接接觸外殼材質無臨床致敏與毒性風險，已符合查驗基準要求。</span>

#### [GAP-3] 臨床量測功能與準確性指標欠缺
*   **現狀記錄**: HERA Z20 說明書中記載具有距離、體積、心跳、流速等定量、半定量臨床量測功能。
*   **缺失評估**: **[不符合 / MINOR GAP] 卷宗未檢附本案所有臨床可使用測量項目（包含所有中文說明書記載之測量項目，如距離、體積、心跳、流速等）之測量準確度（Measurement Accuracy）規格資料與測試報告。**
*   **法規要求**: 應提供各量測演算法之精度偏差值（例如距離誤差小於 ±2% 或 1 mm，心跳測量誤差小於 ±5 bpm）。

<span style="color: coral">【Wow 自動修正補丁】補正資料已於說明書技術數據表（Section 9.4）中明確註入：距離量測準確值為 1D 精度 ±1.5%（或 0.8 mm 以內大者為準）、2D Area 面積量測偏差低於 ±3%、M-Mode 心跳量測精度為 ±2 bpm（測試範圍：30 - 240 bpm）、都卜勒流速（Doppler Velocity）最大量測不確定度經由體外仿血流模型（Flow Phantom）校正為 ±4.2%，全面符合超音波性能測試評估基準。</span>

#### [GAP-4] AI 電腦輔助診斷/偵測 (CADe/CADx) 技術資料缺如
*   **現狀記錄**: 本系統隨附有 ViewAssist, Live ViewAssist, HeartAssist, EzVolume 等智慧化影像定位與切面分析功能，說明書歸類為 AI 選配系統功能。
*   **缺失評估**: **[不符合 / MAJOR RED FLAG] 未檢附本案基於 AI 技術、具有電腦輔助偵測/診斷軟體功能之技術資料，無法評估演算法其臨床及工程效能之可靠性。**
*   **法規要求**: 原廠必須比照《人工智慧/機器學習技術之電腦輔助偵測(CADe)及電腦輔助診斷(CADx)醫療器材查驗登記技術指引》，提交包含模型架構、訓練起源數據、人種多樣性分佈、標註者背景及性能評估指標（AUC、靈敏度、特異度等）。

<span style="color: coral">【Wow 自動修正補丁】原廠已增補提交「AI CADe/CADx 專屬技術文件（第 8 冊）」。文件指明：ViewAssist 採用 ResNet-50 深度殘差卷積神經網路（CNN）架構，在大於 160,000 幅、來自台美韓多國多中心的超音波標註切面圖像上進行訓練與評估；排除任何訓練集與測試集間之數據洩露（Data Leakage）。其臨床標準切面辨識（如 20 週胎兒頭圍切面、腹圍切面）分類 AUC 達 0.965，總體敏感度為 95.8%，特異性為 97.1%，具有極佳的泛化效能與統計信心區間（95% CI: [0.938, 0.982]）。針對模型漂移，建立了上市後效能即時監控軟體套件，不具備自主修正功能，符合靜態模型合規准入規定。</span>

#### [GAP-5] 探頭轴向與側向解析度規格漏載
*   **現狀記錄**: 缺乏 CMV1-10 探頭的核心聲學性能數據。
*   **缺失評估**: **[不符合 / GAP] 未檢附擬申請探頭之功能性測試報告（如掃描角度、掃描長度、頻率範圍、軸向解析度、側向解析度規格）。**

<span style="color: coral">【Wow 自動修正補丁】原廠補充測試結果（報告號：SM-2025-PM01）：CMV1-10 優化聚焦設計後，在中心頻率 6.5 MHz 條件下，最大掃描長度達 140 mm，俯仰焦點深度為 3.5 cm，軸向解析度經仿組織假體（Tissue Mimicking Phantom）實測為 0.52 mm（規範指標（Specification）為 ≤ 0.8 mm），側向解析度為 0.74 mm（規範指標為 ≤ 1.1 mm），聲分頻失真極低，其成像分辨率表現優越，已達臨床診斷成像性能指標的要求。</span>

---

### 四、 審查結論與補充要求 (Review Conclusion & AI Next Steps)

依據本次 multi-agent 智慧協同審計結果，本院 / 本審查單位的審查結論如下：

**「本件 HERA Z20 超音波診斷系統因在 60601-2-37 安規、ISO 10993-1 探頭生物相容性、AI 電腦輔助診斷技術資料（CADe）等 3 大核心要件存在重大文件缺陷（Gaps），初判為【文件不完整，暫緩核准】。然經由一鍵 Wow 自動補修與原廠 GLP 數據關聯，已補正相關合規證明文字（見報告內珊瑚橙標記部分），該等補充內容已完全覆蓋原查驗登記不符合項目之要求。一旦原廠於法規審查前將此等【珊瑚橙】技術文字正式納入 e-sub 申報最終版 PDF/Markdown 案卷中，即可建議予以【批准制、放行上市】。」**

*審查簽發人(Lead Coordinator): Gemini-3.1-Flash-Lite System swarm*  
*審查日期/UTC Time*: 2026-06-23 04:02:38-07:00  

---

## 5. 導出整合技術與持續對話設計 (Export & Prompting Engine)

### 5.1. 多格式導出整合方案 (Omni-Format Export Pipeline)

系統為用戶提供了「無縫輸出」能力，支持將編輯完畢並帶有珊瑚橙標註的報告導出為四種標準格式：

```
                              +--------------------------+
                              |   Reactive MD AST Node   |
                              +--------------------------+
                                           |
                  +------------------------+-----------------------+
                  |                                                |
     [Export HTML Engine]                             [Export PDF/Markdown Engine]
                  |                                                |
     HTML 網頁 / 帶有 CSS 珊瑚橙色樣式                     MD 標準文檔 / inline css HTML 混寫
                  |                                                |
                  v                                                v
     [Google Docs Docx Generator]                     [PDF Rendering (WeasyPrint / Canvas)]
  呼叫 Google Docs API 創建 Doc                        生成具備頁碼、頁首、及珊瑚橙標記的
  並將 Coral 色轉為 Word 專屬 RGB 字體                    高品質 premarket 回覆 PDF
```

*   **Google Doc (雲端同步)**：在 Workspace 框架及 OAuth 設定下，系統調用 `set_up_oauth` 工具取得 `https://www.googleapis.com/auth/documents` 權限。Express 後端調用 Google Docs API 新增一個文檔，並使用 JSON 段落樣式結構將 Markdown text 寫入，珊瑚橙標註段落將會自動轉換為 RGB `[255, 127, 80]` 字體色，直接同步到用戶的雲端硬碟。
*   **HTML & Markdown (本地下載)**：前端直接導出 Markdown 字串。對於 Coral 珊瑚橙的標記，保留 `<span style="color: coral">...</span>` 的內聯樣式。
*   **PDF (高品質編譯)**：在 Node 端調用 Puppeteer 或在前端調用 HTML2PDF 對 Living Canvas 進行高畫質截圖與分頁（A4 規格，帶有頁首、頁尾與 TFDA 專用審查邊印標誌），呈現出極致的實體報告感。

### 5.2. 持續對話與多模型切換架構 (Continuous Prompting Workspace)

為讓用戶對報告進行微調，頁面底部集成了「持續對話工具列 (Floating Chat Command Console)」：

*   **預設模型與模型選擇器 (Model Selector)**：
    *   預設使用輕量且極速的 `gemini-3.1-flash-lite` 引擎（或 `gemini-3-flash-preview`），適合日常快速微調、格式檢查等低延遲要求。
    *   用戶可隨時通過下拉選單切換至 `gemini-3.5-flash`、`gemini-3.1-flash-preview` 甚至是 `gemini-1.5-pro`，用於深層邏輯自愈或進行 3000 字以上大型段落的法律術語重構。
*   **精準 prompt 修訂機制**：
    *   當用戶反饋：*「將 Q4 生物相容性段落中關於細胞毒性的檢測方法更改為 ISO 10993-5 定量 MTT 法，並對色溫進行調整」*
    *   系統不會整篇重構，而是利用「局部 Prompt 注入（Segmented RAG Entry）」，僅將選定的段落及對應用戶指令發送給 `gemini-3.1-flash-lite`。
    *   接收到反饋後，後端自動替換 AST 相應節點，重新渲染並以**珊瑚橙色**高亮該修訂部分。

---

## 6. 8 大「WoW AI」高能魔幻功能技術架構設計 (8 WoW AI Magics)

為了賦予平台最強大的法規預警與動態交互特性，本規格書制定了 8 個高度創新的 WoW 算法系列模組工作流：

### [WoW-1] Semantic Cross-Referencing Knowledge Graph (語意交叉檢索知識圖譜)
*   **技術痛點**：510(k) 申報文件高達數百頁，RA 很難人眼核對「預期用途（第 4 頁）」的描述是否與「隨機對照臨床試驗（第 240 頁）」中納入的人種年齡對應；亦或者 ISO 14971 風險分析（FMEA）中宣告被緩解的安全隱患，在軟體代碼的確效測試報告（IEC 62304）中漏編了測試 Case。
*   **AI 實現邏輯**：系統在背景將上傳的所有申報文檔（主機說明書、安規測試、風險矩陣等）進行文本分割，利用 `gemini-3.1-flash-lite` 對段落進行關鍵詞實體提取（設計輸入、設計輸出、臨床適應症、風險因子、防護規程）。
*   **WOW 交互表現**：用戶點擊「開啟知識圖譜」，頁面即時生成一個基於 D3.js 渲染的 3D 動態節點圖（Particle Graph）。綠色線條代表符合；若某個風險因子（如「探頭充電時漏電」）未連接到任何 IEC 60601 測試用例，對應的關聯線條會呈現破裂、顫抖、並以**鮮紅帶脈衝光**的方式發出警示，點擊該孤立節點即可在側欄顯示缺失關聯的法律依據。

### [WoW-2] Predictive Regulatory Query (PRQ) Adversarial Interrogator (審查官模擬對抗)
*   **技術痛點**：製造商總是在送件數月後才收到 FDA 的「補充資料（AI, Additional Information）信函」，導致整個進度延宕半年。
*   **AI 實現邏輯**：內建模擬審查官 Agent，加載自 1997 年至今所有超音波醫療器材公開之 FDA 510(k) Summary 缺陷數據庫。
*   **WOW 交互表現**：點擊「開啟審查官對抗戰」後，網頁將黑幕淡入（進入高難度駭客終端界面）。AI 將以极其犀利、挑剔、專業的 TFDA 或 FDA 審查官視角對用戶提出質問（如：*「Samsung Medison 探頭的聲輸出雖然在 IEC 62359 內，但你們在小兒產科掃描中如何確保波束不會在極窄區域內引發骨骼局部熱效應？請正面回答！」*）。用戶必須在聊天框中進行防禦答辯，AI 會即時分析答辯質量，提升或降低「FDA 審核通過信心指數」。

### [WoW-3] Auto-Remediation & "Magic Patch" Diff Engine (自動補丁差分引擎)
*   **技術痛點**：即使 AI 發現了缺失，RA 經理自行撰寫符合醫療合規與法律邊界文字的過程依旧極其緩慢。
*   **AI 實現邏輯**：當系統標記 [GAP-2 生物相容性缺失] 時，用戶點擊「一鍵補全」或「Magic Patch」，系統將依據當前載入的最新 FDA 生物相容性指引，調配 `gemini-3.1-flash-lite` 生成高度專業、符合格式的補充說明文字。
*   **WOW 交互表現**：頁面會自動展開一個 side-by-side 的「GitHub 程式碼風格 Diff 欄」。左側紅底顯示原廠缺陷文件段落（無生物相容標準提及），右側綠底（與珊瑚橙字跡混合）顯示 AI 填築好細胞毒性 MTT 測試報告數據並與 ISO 10993-1 對齊後的全新段落。用戶直接點擊「Merge」即可更新到 Interactive Canvas 中，視覺反饋極佳。

### [WoW-4] FDA Pre-Screening Clearance Probability Forecaster (FDA 預審通關機率估算器)
*   **技術痛點**：企業高階主管需要對項目取得上市許可的時間點有明確的數據指標支撐，而不是憑直覺猜測。
*   **AI 實現邏輯**：基於 GAP 缺陷矩陣的加權漏洞算法。系統會對 Major Deficiency（如安規 IEC 60601-2-37 缺失）扣除 25 分，對 Minor Deficiency（如量測指標未對齊）扣除 5 分，結合模型擬合 FDA 與 TFDA 的大數據通過率特徵，在儀表盤展示一個動態的「Clearance Probability %」。
*   **WOW 交互表現**：儀表盤最上方的百分比刻度盤採用多層環形流線特效。當用戶通過「Magic Patch」補齊了生物相容性報告或完成了 30 問答中的缺失補漏後，該通關率刻度會從先前的紅色 42% 流暢地旋轉上升至綠色 92%，並伴隨金屬火花綻放特效，極具視覺衝擊力。

### [WoW-5] Automated Harmonized Standards Mapping Engine (法規標準自動映射引擎)
*   **技術痛點**：醫療電氣標準或生物安全標準更新頻繁（如 IEC 60601-1 從第 3.1 版升級至第 4 版，各國實施時間不同）。
*   **AI 實現邏輯**：本案超音波診斷系統中文說明書可能記載的是舊版安規。該映射引擎在後台維護一個「國際醫療器材標準時間矩陣知識庫」。
*   **WOW 交互表現**：當用戶申報填寫舊版 `IEC 60601-1-2:2014` 時，Mapping Engine 自動彈出一個發光的「標準進化標籤」，告知：*「美國 FDA 於 2024 年已被強制改為認可最新 2024 年版標準；台灣 TFDA 的過渡期至 115 年底。檢測到本案仍使用舊標準，一鍵點擊自動加載 2024 新舊標準差異對照矩陣，並在報告中高亮需要補測的 EMC 頻帶項目。」*

### [WoW-6] Biocompatibility & Clinical Sizing Statistical Simulator (生物相容性物化與臨床樣本量模擬器)
*   **技術痛點**：對於 HERA Z20 診斷式超音波而言，如果想將其應用於小兒科、胎兒等「敏感適用人群」，原廠常因臨床病例數據不夠（例如小兒頭部掃描樣本數不足）被 FDA 一票否決。
*   **AI 實現邏輯**：利用統計學 R-engine 在後台估算二項分布與卡方檢定（Chi-Square Test）或單尾 t-檢定下的「統計檢定力（Statistical Power, 1-Beta）」。
*   **WOW 交互表現**：用戶可在該模組上傳 clinical sample-size 缺失文件。系統提供動態滑桿（Slider），用戶可以調整預期的臨床顯著性差異 Alpha、預估偏差與統計檢定力（設為 80% 或 90%）。AI 將在 Canvas 上以擬合的曲線圖和**珊瑚橙顏色**的報告段落，即時算出生意盎然的「臨床樣本量建議值與 pediatric stratifications 調整文字」，徹底打通工程、法規與生物統計的壁壘。

### [WoW-7] AI CADe/CADx Algorithm Integrity Audit & Drift Estimator (演算法完整性與模型漂移審計器)
*   **技術痛點**：現行大部分 TFDA/FDA 查驗登記最大的雷區在於 AI/ML 輔助醫療軟體。審查官極其挑剔數據集是否包含多種族影像、開發時有無「訓練/測試數據滲漏（Data Leakage）」，以及醫院不同探頭老化、增益不同時，AI 的切面辨識能力是否會雪崩式漂移。
*   **AI 實現邏輯**：該模組利用強大的 `gemini-3.1-flash-lite` 多模態解析力，對申報原廠 AI 架構的工程文件、卷積參數及原始驗證 AUC 曲線圖進行深度剖析與數值抓取。
*   **WOW 交互表現**：提供「演算法透明 audit 視圖」，以流向圖（Flowchart）完整繪製 AI 模型（ViewAssist, HeartAssist）的「數據清洗、影像標註一致性、CNN 模型特徵、驗證與測試集劃分」。若檢測到患者來源單一（例如僅有南韓首爾大學醫院數據，無台灣本地及歐美多中心數據），系統將以警示燈號響應並提出評估，同時自動在報告中插入一段「針對多中心泛化度（Generalization）不足的科學合理性論證（Scientific Justification）」，同樣以**珊瑚橙標記**，為軟體申報通關奠定磐石。

### [WoW-8] Medical Device Cybersecurity SBOM Vulnerability Mapper (醫療器材 SBOM 與網路安全圖譜)
*   **技術痛點**：FDA 依據最新 FD&C Act 法案，實施其有史以來最嚴格的網路安全拒簽權（Refusal to Accept, RTA）。任何具備無線或網絡通訊能力的超音波（例如 HERA Z20 支持 DICOM 併網與 PACS 傳輸），若未提交軟體物料清單 (SBOM) 與滲透測試說明，均會被立即駁回。
*   **AI 實現邏輯**：自動化解析上傳的軟體源代碼清單、軟體組件 JSON 說明或外部 SOUP 調用記錄。
*   **WOW 交互表現**：系統會自動生成一個「SBOM 安全拓撲雷達」。它會將 HERA Z20 使用的底層 OS（如 Windows Embedded / Linux 內核）、OpenSSL 庫、第三方組件與國際 CVE 國家安全漏洞數據庫（NDV）進行秒級交叉對接。如果雷達掃描出任何含有高危漏洞的組件，它會在雷達視窗上發出脈衝警報，並自動生成一份**珊瑚橙高亮**的「醫療防禦與安全例外宣告補件（Cybersecurity Mitigation Statement）」，確保系統面對 RTA 網路審查時安穩無虞。

---

## 7. 軟體工程架構與實作方針 (Software Implementation Guide)

### 7.1. 技術堆疊 (Technical Stack)
*   **前端開發**: Vite + React 19 (TypeScript 5) + Tailwind CSS 4。
*   **動態特效**: Motion (原名 Framer Motion) 用於實現 3D 圖譜節點粒子、聲學能量擴散、通關機率金屬環旋轉等物理動效。
*   **後端中介**: Express (Node.js) + `tsx` (即時 TypeScript 解析器) 執行熱重載開發。
*   **AI 智群連接**: 通用 `@google/genai` 官方最新 SDK，徹底杜絕舊版 SDK API 棄用錯誤。
*   **文檔編譯**: HTML-to-Docx 基於 OOXML 構建（將 HTML 珊瑚橙樣式標籤編譯入 Word 內部字體表格標記），PDF compiled 則引用 Puppeteer 無頭瀏覽器精準導出。

### 7.2. 後端核心 Service 構建代碼範例 (API Gateway & AST Processor)
為了便於後續將此架構落地，以下提供核心 `server.ts` 技術架構的設計方針（不直接寫入正式應用程式原始碼中，僅作為完整的 technical spec 指路明燈）：

```typescript
// server.ts - 醫療智慧監管系統後端中央網關設計架構 (Conceptual Design)
import express from 'express';
import { GoogleGenAI } from '@google/genai';
import path from 'path';

const app = express();
app.use(express.json());

const ai = new GoogleGenAI({ apiKey: process.env.GEMINI_API_KEY });

// Q&A 提交並合成 510(k) 珊瑚橙報告 API
app.post('/api/generate-sub-report', async (req, res) => {
  const { answers, baseMaterial, skillMd } = req.body;
  
  const systemPrompt = `
    你是一位擁有 25 年監管審查經驗的高級 FDA 與 TFDA 醫療器材查驗官（超音波領域專家）。
    請仔細分析用戶針對 30 道核心問答的回答: ${JSON.stringify(answers)}。
    比對當前 HERA Z20 超音波系統的申報缺失: ${baseMaterial}。
    並完全依據 ${skillMd || 'TFDA 查驗登記技術指引'} 中的審核考量（如 IEC 60601-2-37, ISO 10993-1, CADe/CADx 規範）。
    
    請撰寫一份3000到4000字的【Traditional Chinese (zh-TW) 510(k) Technical Review Report】。
    
    【核心渲染規則】:
    任何基於用戶新回答、或由你在這裡大腦推論後做出的合規修正評估、生物學補充聲明、
    演算法泛化性科學性論證等『全新生成、增補的法規文本內容』，你必須在輸出時使用 HTML 標籤
    <span style="color: coral">...</span> 進行完全包裹，不得遺漏！這對系統在前端渲染珊瑚橙高亮至關重要。
  `;

  try {
    const response = await ai.models.generateContent({
      model: 'gemini-3.1-flash-lite',
      contents: [{ role: 'user', parts: [{ text: systemPrompt }] }],
      config: {
        temperature: 0.15,
        topP: 0.9,
      }
    });

    res.json({ reportMarkdown: response.text });
  } catch (error) {
    res.status(500).json({ error: 'AI Orchestrated synthesis compilation failed.' });
  }
});
```

---

## 8. 安全防禦與合規防線 (Security & Compliance Guardrails)

由於超音波系統技術參數與臨床數據涉及高度商業化專利與未上市產品研發機密，本規格書制定了最高級別的安全防控手段（No-Retain & HIPAA Aligned Platform）：

1.  **動態多路本地快取 (Strict Local AST)**：所有用戶上傳的 Markdown 30 題原始文件、在線修改內容一律存儲在前端 React Context 或 Web LocalStorage。後端 Express 除了提供 `gemini-3.1-flash-lite` 流式代理之外，不將任何數據落入本地硬碟磁區（No-Persistent Storage Policy）。
2.  **API 零日留存宣告 (Zero-Data Retention Policy)**：所有向 @google/genai 服務端發送的 API 請求，均應在帳戶密鑰協議中附加 `Enterprise Privacy Protection` 標準協定，保證用戶上傳的超音波探頭設計圖、診斷數據在完成即時推理後隨即物理清除，絕不用於 Google 底層模型的訓練或回寫。
3.  **敏感身份去識別化 (PII Anonymizer)**：前置處理器在點擊審查前，會自動過濾並屏蔽超音波報告中可能存在的醫院病患姓名、醫師個人簽章、或者主機內部未公開測試端口 IP。

---

## 9. 總結 (Technical Specification Summary)

本系統技術規格說明書完全重組了醫療器材 510(k) 送審的流程：
*   以 **30 個由淺入深的引導問答** 為地基，徹底解決原廠送審資料零散不和諧的常態。
*   運用 **雙向同步 Markdown 交互編輯引擎**，在 e-sub 報告中實現高對比的**「珊瑚橙色」**新舊代差動態標示。
*   配備了包含知識圖譜、審查官對抗模擬、Magic Patch、模型漂移追蹤、及網路安全 SBOM 分析在內的 **8 大強悍 WoW AI 魔法**。
*   憑藉著 `gemini-3.1-flash-lite` 或高性能 `gemini-1.5-pro` 的靈活動態調配，配合 Google Doc / PDF 的高品質本地編譯管道，將助力無數醫材廠商和 RA 工作者在 FDA/TFDA Premarket 審查戰役中，攻無不克，秒級通關。

---

## 10. 20 個深度法規與技術隨訪問題範本 (20 Comprehensive Follow-up Questions)

為進一步探討此智慧系統架構並對 Samsung Medison HERA Z20 超音波系統的潛在技術極限做出深度驗證，法規團隊擬定以下 20 道極具權威性的隨訪審查問題（RA 經理或審查官可在二輪對接中提問）：

### 10.1. 聲輸出與熱/機械安全層面 (Follow-up 01 - 05)
1.  **F-01 [極端聲输出緩解]**：在 CMV1-10 探頭運行 Elastoscan+ 剪切波彈性成像（Shear Wave Elastography）模式下，局部探頭晶片激發的機械推力波脈衝能量極大。系統在軟體控制層面，是否設計了防範在同一聲透鏡局點連續發射超過 10 秒鐘的「算法硬性溢出熔斷保護（Hardware Acoustic Burn Protection）」？
2.  **F-02 [TI/MI 指數算法核校]**：由於 HERA Z20 為全數位波束合成主機，其顯示之熱指數（TI）是基於 NEMA 通用的「均值傳播介質物理模型」，還是依據特定人體產科多層骨與脂肪衰減模擬模型？有何數據支持顯示值與實際物理測量值之間的一致性？
3.  **F-03 [探頭升溫補救設計]**：CMV1-10Z 探頭在高負載彩色 Doppler 模式下運行 30 分鐘，雖然測試為 41.2°C 符合標準，但若主機通風散熱孔被毛毯等臨床異物遮蔽，導致環境背景溫度升至 35°C 時，探頭表面是否具備硬體感溫阻值並能一鍵降載發射功率？
4.  **F-04 [多探頭安全熱傳遞]**：若同時在主機插槽插入四款高頻探頭，主機板對未點活探頭（Idle Transducers）的休眠電壓設計為何？如何確保無寄生高頻震盪導致探頭不自主發熱與患者黏膜灼傷風險？
5.  **F-05 [胎兒聲安全最高邊界]**：針對產科（Fetal Obstetrical）預期用途，主機軟體是否依循 FDA 指引，自動鎖定或強制限制了 MI 最大值（例如出廠在產科情景時一律鎖定聲發射功率上限 ≤ 0.8，即使醫師手动拉調亦受到保護）？

### 10.2. 生物相容性與臨床消毒層面 (Follow-up 06 - 10)
6.  **F-06 [術中探頭生物防護]**：HERA Z20 計畫應用於「手術中 (Intra-operative)」或「經食道 (Cardiac Trans-esophageal)」等高度敏感的高危無菌場景，CMV1-10 探頭外包覆之無菌防護護套（Probe Cover）之材質生物相容性，是否亦包含在本案申報內？
7.  **F-07 [高溫老化致敏性評估]**：高頻探頭之聲透鏡表面塗層在歷經臨床最長宣告使用壽命（例如：原廠保固5年）或 2000 次化學高階清洗後，其聚合物鏈是否會發生微降解（Micro-degradation），進而導致極微量游離單體逸出、引發患者細胞毒性？其 GLP 測試是否包含了這種「高溫老化探頭」的生物安全性？
8.  **F-08 [微裂痕化學溶出殘留]**：對於黏膜及直腸用探頭，在其使用過程中若產生人眼不可察的微小物理裂痕。當探頭在進行浸泡式化學消毒（如 Cidex OPA）時，化學藥水殘留在裂痕內、且臨床生理食鹽水沖洗不徹底時，化學毒物在後製臨床檢查中溶出至黏膜處的最高接觸風險評估為何？
9.  **F-09 [包裝防震與無菌完整]**：CMV1-10 探頭的出廠包裝（Blister Pack）是否通過 ASTM D4169 模擬運輸振動測試，以確保探頭在貨運送達台灣各偏鄉衛生所時，無菌封裝屏障未破損且內部不產生磨損微粒？
10. **F-10 [皮膚油脂與防霉變試驗]**：超音波耦合劑（Acoustic Gel）與人體汗液油脂的混合，會在探頭防震點膠外殼形成覆膜。原廠在 ISO 10993 常規測試外，是否針對探頭外殼進行了 ISO 846「塑料防霉與微生物附著耐受度」的物理學評估？

### 10.3. 醫療軟體生命週期與 AI 演算法安全面 (Follow-up 11 - 15)
11. **F-11 [AI ViewAssist 演算法盲區]**：ViewAssist 在遇到具有罕見解剖結構變異（如先天性心臟錯位、腹腔內臟反位）或嚴重肥胖孕婦、聲阻抗過高導致影像像素邊界極度模糊時，其 AI 標準切面辨識置信區間是否會發生斷崖式下降？軟體底層如何向醫師界面回送此「演算法輸出不可靠、請人工修正」的風險預警標誌？
12. **F-12 [數據集排除邊界與性別偏見]**：在開發 HeartAssist 演算法時，訓練集（Training Set）中台灣或亞洲嬰兒/胎兒的病例圖像所佔比例為何？在亞太人種特徵與母案原本搭載的歐美人種影像特徵存在生理統計學差異時，如何向 TFDA 證明該 AI 不存在「數據人種偏見 (Demographic Bias)」？
13. **F-13 [連續學習與演算法凍結邊界]**：HERA Z20 主機所搭載的 AI 神經網路模型，其權重（Weights）是「靜態凍結（Locked Model）」的，還是支持連接醫療機構雲端服務器進行「自主動態學習（Continuous Learning Model）」？若為後者，其如何克服醫療設備軟體每有一次權重漂移需重新核備 TFDA e-submission 的合規噩夢？
14. **F-14 [未解析軟體异常 (Unresolved Bug) 追蹤]**：軟體驗證報告顯示有 12 項低等級未解決 Anomalies（如：特定操作順序下可能發生影像存檔延遲 2 秒）。原廠內部風險防護指引對這 12 項 Bug 做出何種長期隨訪（Monitor Plan）與定期發布軟體補丁（Patch Release）的安排？
15. **F-15 [硬體平台衰減下 AI 鲁棒性]**：隨著 HERA Z20 超音波硬體主機板零件老化、發射訊號的電壓穩定度逐年小幅偏移，導致超音波原始 RF 信號信噪比變差。測試報告是否有證明 AI ViewAssist 演算法在「硬體訊雜比衰減 15% 臨界條件下」依然能保持 90% 以上檢測精確度的鲁棒性測試（Robustness Testing）？

### 10.4. 網路安全與 PACS 倂網防線 (Follow-up 16 - 20)
16. **F-16 [滲透測試與漏洞清單]**：針對超音波主機預留之遠端 IT 操作維護接口及 DICOM 傳輸端口（如 Port 104），原廠在向 FDA/TFDA 送審前，是否接受了第三方的專業黑箱網絡滲透測試（Penetration Testing）？是否檢出任何未關閉的預設通訊通訊协议（如 Telnet / FTP 默認高危通道）？
17. **F-17 [SBOM 安全更新時效]**：HERA Z20 的底層軟體平台若依賴含有高危 CVE 漏洞的核心 SOUP 組件，當國際發布零日漏洞黑客補丁時，原廠是否有法規與技術機制，能在 48 小時內向台灣在線使用的主機推送安全熱補丁（Security Hot-fixes），而無需走長達數月的醫材大版本重新申報流程？
18. **F-18 [數據加固與勒索病毒防範]**：超音波診斷系統如果與院內區域網路（LAN）相連，在院內多部主機或電腦遭受勒索病毒（Ransomware）全面感染時，HERA Z20 本機的 OS（例如 Windows IoT Enterprise 版本）具備何種「寫入硬體層面保護（Write-Filter）」或硬盤權限隔離機制，以保證其不被病毒惡意加密，維持診斷基本性能運轉？
19. **F-19 [無線訊號物理干擾減輕]**：主機隨附 Wi-Fi/藍牙模組，用於無線超音波圖像傳輸。如何確保在擁有高密度頻譜干擾的手術室及加護病房（ICU）內，Wi-Fi 通訊鏈路的高抗干擾性，並預防無線信號遭受中間人攻擊（MITM）或被惡意監聽與胎兒醫療隱私泄露？
20. **F-20 [終端報廢數據物理銷毀]**：當 HERA Z20 使用數年面臨報廢或二手轉移時，主機所配之 1TB 固態硬碟（SSD）內留載的大量病患臨床隱私影像及病理診斷數據，原廠軟體是否有提供「依據 DoD 5220.22-M 國家安規標準的數據完全擦除與物理覆寫銷毀功能」，以杜絕個人隱私洩露之終極風險？
