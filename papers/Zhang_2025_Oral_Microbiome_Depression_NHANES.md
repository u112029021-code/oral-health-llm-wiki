# [Zhang 2025] Association of Oral Microbiome Diversity With Depression Status: NHANES 2009–2012

- **作者**：Cuifeng Zhang, Lingli Qu, Yanhua Huang, Lan Tang, Jie Ma, Kaipeng Xie, Huaying Wu
- **年份**：2025
- **期刊/出處**：*Journal of Public Health Dentistry*, 85(3), 252–260.
- **文獻分類**：前沿微生物體學與神經精神學研究 (Microbiome-Epidemiological Study)
- **核心概念鏈結**：[[concepts/Oral_Microbiome_Dysbiosis|口腔微生態失調]], [[concepts/Oral_Brain_Axis|口腦軸]], [[tools/NHANES_Survey|NHANES 調查]]

---

## 1. 一分鐘通俗總結 (Plain Language Summary)
> **嘴裡的細菌越多樣化，大腦就越不容易陷入嚴重憂鬱！**  
> 南京醫科大學團隊透過高通量 16S rRNA 基因定序，解密了全美 1497 人的口腔漱口水微生物群落。研究發現：**口腔微生態的豐富度（α 多樣性）越高，罹患重度憂鬱症的風險就越低（每增加一個菌種 ASV，風險顯著下降約 0.8%）。** 嚴重憂鬱症患者的口腔細菌多樣性顯著匱乏。這揭露了口腔菌群不僅僅在嘴裡製造牙垢，還可能透過「口-腦神經發炎」或「口-腸-腦軸線」，成為大腦情緒健康的微生物晴雨表！

---

## 2. 研究背景與目的 (Background & Objective)
* **背景**：人體被視為由宿主與微生物組成的「超級生物體（Superorganism）」。雖然「腸腦軸（Gut-Brain Axis）」已為人熟知，但口腔作為消化道入口，擁有全身第二龐大多樣的菌群（超過 700 種細菌）。
* **核心疑問**：口腔菌群的生物多樣性是否與大眾族群的臨床憂鬱症狀嚴重度存在客觀關聯？
* **目的**：利用美國 NHANES 國家級微生物定序數據，分析口腔微生物 α 與 β 多樣性與重度憂鬱（PHQ-9 ≥ 15）的關聯。

---

## 3. 研究方法與定序分析 (Methods)
* **分析樣本**：NHANES 2009–2012 兩週期數據，納入具有完整口腔含漱樣本 16S rRNA 定序與 PHQ-9 資料之成年人 **N = 1,497**（重度憂鬱組 N = 111，佔 7.41%）。
* **微生物定序技術**：
  * 對口腔沖洗液中提取的 DNA 進行 16S rRNA 基因 **V4 可變區** PCR 擴增與高通量定序。
  * 以 QIIME 與 DADA2 軟體分析，產生擴增子序列變體（Amplicon Sequence Variants, **ASVs**），比對 SILVA v123 資料庫，共識別 41,378 個 ASVs。
* **生物多樣性指標**：
  * **α 多樣性（個體內菌群豐富度）**：以 Observed ASVs 作為核心指標。
  * **β 多樣性（群體間菌群結構差異）**：採用 Bray-Curtis 相異度與 ANOSIM 分析。
* **統計模型**：限制性立方樣條（RCS）檢驗劑量反應曲線、多變項 Logistic 迴歸（Model 3 控制人口學、BMI、菸酒、高血壓、糖尿病及牙周炎）並繪製預測列線圖（Nomogram）。

---

## 4. 關鍵實證結果 (Key Findings)
1. **α 多樣性與憂鬱程度呈顯著負相關**：
   * 重度憂鬱症組的 ASV 中位數為 **119.3**，顯著低於非重度憂鬱組的 **128.75** (p = 0.007)。
   * 多變項線性迴歸顯示 ASV 與 PHQ-9 得分呈顯著負相關（β = -0.008, p = 0.014）。
   * 限制性立方樣條（RCS）證實兩者呈現高度**線性負向劑量反應**（p-nonlinear = 0.232）。
2. **重度憂鬱風險降低**：
   * 邏輯迴歸 Model 3 顯示，ASV 每增加 1 單位，重度憂鬱風險下降（**OR = 0.992**, 95% CI: 0.987–0.997, p = 0.003）。
3. **β 多樣性具有群體顯著差異**：
   * 兩組在 Bray-Curtis 相異度分析上表現出顯著的菌相結構偏移（ANOSIM R = 0.087, p = 0.003）。

---

## 5. 生物機制：口-腦軸的三大可能途徑 (The Mechanistic Hypotheses)
文獻指出口腔微生物影響中樞神經系統（CNS）的潛在路徑：
1. **血液與血腦屏障滲漏（Hematogenous & BBB Breakdown）**：牙周致病菌（如 *Porphyromonas gingivalis* 牙齦卟啉單胞菌）及其分泌之牙齦蛋白酶（Gingipains），可穿透破損的微血管屏障進入血液，甚至穿透通透性增加的血腦屏障，誘發小膠質細胞活化與神經發炎。
2. **口-腸-腦軸轉移（Oral-to-Gut Translocation）**：每天吞嚥大量口腔細菌進入消化道；在菌群失調或腸黏膜脆弱時，造成腸道通透性上升（「腸漏症 Leaky Gut」），間接干擾腸腦神經內分泌。
3. **腦神經直通路徑（Cranial Nerve Invasion）**：病原菌直接沿著三叉神經或迷走神經末梢逆行侵犯中樞神經系統。
