# EXECUTION_LOG.md - 實際執行紀錄與 Workflow 反思調整報告

本文件完整記錄了「從牙齒到心靈：口腔健康與身心福祉 LLM Wiki」之實際編譯歷程、品質審查紀錄、出錯節點分析與 Workflow 檢查左移（Shift-Left）之反思調整。

---

## 1. 執行歷程與節點產出紀錄 (Execution Trace)

* **執行時間**：2026-11-23
* **知識庫路徑**：`c:\Users\user\Downloads\LLM Wiki`
* **輸入源材料 (6 篇 PDF)**：
  1. `MeasuringOral Health A ConceptualFramework Locker (1).pdf` -> Locker (1988)
  2. `development-and-evaluation-of-the-oral-health-impact-profile-fj2epi4bk9 (1).pdf` -> Slade & Spencer (1994)
  3. `Comm Dent Oral Epid - 2017 - Chaffee - Oral health‐related quality‐of‐life scores differ by socioeconomic status and caries.pdf` -> Chaffee et al. (2017)
  4. `1-s2.0-S0163834314000139 (1).pdf` -> O'Neil et al. (2014)
  5. `J Clinic Periodontology - 2024 - Wang - Associations between oral health and depression and anxiety  A cross‐sectional and.pdf` -> Wang et al. (2024)
  6. `J Public Health Dent - 2025 - Zhang - Association of Oral Microbiome Diversity With Depression Status  NHANES 2009 2012.pdf` -> Zhang et al. (2025)

---

## 2. 品質審查點執行結果 (Quality Gate Audit)

### 門禁 1：Check 1 - 增量編譯與概念完整性檢查
* **受檢對象**：`papers/` (6篇), `concepts/` (4篇), `tools/` (4篇), `synthesis/` (1篇)
* **檢驗項目**：
  1. 是否所有論文皆遵循 Schema，並包含「一分鐘通俗總結」與「研究限制」？ -> **[通過]**
  2. 是否所有引用的量表（OHIP, ECOHIS, PHQ-9）均有建立反向連結？ -> **[通過]**
  3. 文獻間數值是否精確（如 Wang 2024 的 HR 1.19 / 1.13 / 1.27，Zhang 2025 的 OR 0.992）？ -> **[通過]**
* **審查結論**：Check 1 通過，允許觸發 `INDEX.md` 更新。

---

### 門禁 2：Check 2 - 通俗化教學審查 (大綱認知負擔評估)
* **受檢對象**：`presentation/outline.md`
* **審查標準**：能否讓非醫學、非牙科背景之一般大眾完全理解？
* **初次審查發現之缺陷 (Defects Caught)**：
  - 在第 7 頁與第 8 頁大綱中，初版出現「16S rRNA V4 區高通量定序」、「擴增子序列變體 ASVs」、「Bray-Curtis 相異度」等艱澀詞彙，未附帶生活化比喻，讀者將產生嚴重認知斷層。
* **觸發迴圈 (Trigger Loop to Outline)**：
  - 退回 Node 5 修正大綱：將 ASV 菌群豐富度改以**「熱帶雨林 vs 單一草坪」**生活比喻進行轉譯，並將口腦軸路徑歸納為直觀的三張卡片（血管巡航、口腸腦轉移、腦神經直通）。
* **複審結論**：修正後通過 Check 2。

---

### 門禁 3：Check 3 - 簡報真實性與離線瀏覽驗證
* **受檢對象**：`presentation/index.html`
* **檢驗項目**：
  1. 投影片各項統計數字（NHANES 10,214人、UK Biobank 26萬人 9年追蹤、OR 1.60/2.13/3.94）是否 100% 能在 Wiki 中溯源？ -> **[通過]**，各頁皆附帶 `Wiki 知識溯源` 標註。
  2. 檔案是否為單一獨立 HTML，無任何外部 CDN/Server 依賴即可離線運作？ -> **[通過]**，CSS 與 JS 均內嵌。
  3. 鍵盤導航（左右箭頭、空白鍵、全螢幕）與進度指示器是否運作流暢？ -> **[通過]**。

---

## 3. 作業核心問題深度反思 (Reflection & Shift-Left)

### Q1：哪一個節點最常出錯？
> **回答**：在初版工作流中，**Node 6（HTML 簡報生成節點）最常出錯且代價最高**。
> 
> **出錯本質分析**：
> 當直接將學術論文交由 Agent 生成最終簡報時，LLM 傾向於直接搬用論文的生硬字眼（例如：「限制性立方樣條 RCS 顯示非線性檢驗 p=0.232」、「小膠質細胞激活」、「Thurstone 成對比較權重」）。在最後生成 HTML 程式碼時才叫 Agent 修改內容，往往會導致：
> 1. HTML/CSS 標籤未閉合、版面破版。
> 2. 為了塞下冗長學術字詞導致排版溢出（Overflow）。
> 3. 反覆重寫數百行 HTML 代碼，耗費大量 token 與運算時間。

---

### Q2：發現問題後，你把檢查往前移到了哪一個步驟（Shift-Left）？
> **回答**：我們將檢查大幅**「往前移（左移）」到了兩個上游步驟**：
> 
> 1. **左移至 Node 2（Wiki 論文編譯階段）**：
>    在 `AGENTS.md` 中強制增設規範：每一篇論文在被編譯進 `papers/` 時，**第一節必須強制產出「一分鐘通俗總結（Plain Language Summary）」**，要求在編譯當下就必須完成一次大眾白話轉譯。
> 2. **左移至 Node 5（大綱 Storyboard 階段）增設 Check 2**：
>    在動手寫任何 HTML/CSS 程式碼前，先由純文字的 `outline.md` 接受「受眾認知負擔檢驗」。在 Markdown 純文字層面解決語氣生硬與術語過載問題，成本遠遠低於在 HTML 程式碼層面修改。

---

### Q3：你有沒有因此修改 workflow / graph？為什麼？
> **回答**：**有，我們對原始線性流程進行了重大重構！**
> 
> * **原先直覺的線性流程（Naive Linear Pipeline）**：
>   `取得文獻 → 寫入 Wiki → 直接生成 HTML 簡報 → 最後人工檢查修復`
> * **修改後的二階段雙迴圈 Graph（Two-Phase Dual-Loop Graph）**：
>   1. **拆分為兩大子圖（Ingest Graph 與 Presentation Graph）**：將「知識沉澱」與「教學應用」解耦，讓 Wiki 成為不可撼動的「單一真實來源（Single Source of Truth）」。
>   2. **引入 Check 2 認知負擔反饋迴圈**：大綱未達通俗化標準前，嚴格禁止進入 Node 6 撰寫 HTML，從源頭根絕了後端代碼崩潰的風險。
>   3. **增設 Check 3 事實查核機制**：強制投影片標註 `wiki-ref` 溯源路徑，確保簡報內容與 Wiki 保持 100% 精確對應，杜絕幻覺。
