---
name: industry-research
description: 產業研究與輪動策略，整合全球頂尖投行報告，識別景氣循環中的產業機會，判斷產業競爭格局與長期趨勢，承接總體經濟分析為個股選擇提供方向指引
version: 2.0.0
author: Evan
license: Proprietary
tags:
  - industry-analysis
  - sector-rotation
  - investment-themes
  - supply-demand-analysis
  - competitive-landscape
  - megatrends
  - institutional-research
---

# 產業研究與輪動 (Industry Research & Rotation)

## 概述

承接總體經濟分析的結論，本模組專注於產業層面的深度研究，整合全球頂尖投行與研究機構的產業報告，識別景氣循環中的產業機會，判斷產業競爭格局與長期趨勢，為個股選擇提供方向指引。

### 核心理念

**選對產業比選對個股更重要**

- 產業順風時，平庸的公司也能有好表現（產業 Beta 效應）
- 產業逆風時，再優秀的公司也難有超額報酬
- 在對的時間佈局對的產業，事半功倍
- 結構性成長優於週期性反彈：長期趨勢的力量遠大於短期波動

**機構投資人的智慧**

本模組整合全球頂尖投行與研究機構的集體智慧：
- 摩根大通預期 2026 年 S&P 500 目標 7,500 點，AI 與數位基礎建設為主要動能
- 高盛強調十大投資主題：AI 與電力、軍備演進、人形機器人為核心
- 貝萊德認為 AI 仍是 2026 年股市主導力量，但需要挑選真正有營收的贏家
- 摩根士丹利預測核電投資至 2050 年將達 2.2 兆美元，較前次預測增加 47%

### 核心能力

1. **機構報告整合能力** - 追蹤 13F 文件與頂尖投行產業報告
2. **產業生命週期定位** - 判斷產業處於導入期/成長期/成熟期/衰退期
3. **供需分析與景氣追蹤** - 識別供需拐點與產業週期轉折
4. **競爭格局評估** - 市場集中度與龍頭企業護城河分析
5. **技術變革影響研判** - 破壞性創新與技術成熟度評估
6. **產業鏈上下游分析** - 價值鏈拆解與關鍵瓶頸識別
7. **產業輪動時機判斷** - 基於經濟週期與主題投資的動態配置

---

## 適用場景

### 應使用本模組的情境

**產業趨勢研判：**
- 「現在該佈局哪些產業？」
- 「半導體 / AI / 電動車 / 核電產業現在處於什麼階段？」
- 「哪些產業有結構性成長機會？」

**產業比較與選擇：**
- 「金融股 / 科技股 / 傳產股哪個比較好？」
- 「為什麼投行推薦國防股？邏輯是什麼？」
- 「AI 產業鏈中，哪個環節最有投資價值？」

**供需與競爭分析：**
- 「產業供需如何？庫存健康嗎？」
- 「這個產業的競爭格局如何？誰是龍頭？」
- 「產業定價權在誰手上？」

**投資組合配置：**
- 「產業輪動策略怎麼做？」
- 「各產業該配置多少權重？」
- 「什麼時候該從科技股輪動到金融股？」

### 觸發關鍵詞範例

**產業名稱：** 半導體、AI、電動車、核電、國防、金融、醫療、能源、消費

**產業相關：** 產業趨勢、產業週期、產業輪動、供需、競爭格局、產業鏈

**投資主題：** AI 算力、數據中心、軍備、核電、去美元化、肥胖藥、GLP-1

### 不適用情境

- 單一公司深度分析 → 使用 `equity-fundamental-analysis`
- 總體經濟環境評估 → 使用 `macro-market-analysis`
- 技術線型與進場時機 → 使用 `technical-analysis`

---

## 輸入格式

### 自然語言輸入（推薦）

直接用自然語言提問，AI 會自動解析並執行分析。

**範例提問：**
- 「半導體產業現在是什麼階段？該進場嗎？」
- 「2026 年投行推薦哪些產業？」
- 「AI 產業鏈中，晶片設計、製造、還是應用軟體更有潛力？」
- 「現在該做產業輪動嗎？從哪輪到哪？」

### 結構化輸入（進階使用）

精確控制分析範圍與深度，使用 JSON 格式：

```json
{
  "analysis_type": "industry_overview",
  "industry": "Semiconductors",
  "region": "Global",
  "language": "zh-TW",
  "time_horizon": "medium-term",
  "include_institutional_reports": true
}
```

**分析類型選項：**

- `industry_overview` - 產業全貌分析
- `supply_demand` - 供需分析
- `competitive_landscape` - 競爭格局分析
- `industry_chain` - 產業鏈分析
- `sector_rotation` - 產業輪動策略
- `thematic_research` - 主題投資研究
- `institutional_consensus` - 機構共識整合

---

## 執行流程

### Step 1: 承接總體經濟分析

**自動讀取總經模組結論：**

- 經濟週期階段（復甦期/擴張期/高峰期/衰退期）
- 市場風險偏好（Risk-On / Risk-Off）
- 央行政策立場與利率環境
- 建議股票部位比例

**根據經濟週期初步篩選產業方向：**


| 經濟階段 | 優先產業（超配） | 次選產業（標配） | 避開產業（低配） |
| :-- | :-- | :-- | :-- |
| **復甦期** | 金融、工業、原物料、房地產 | 科技、非必需消費 | 公用事業、必需消費 |
| **擴張期** | 科技、非必需消費、工業 | 金融、原物料 | 能源、公用事業 |
| **高峰期** | 能源、原物料、金融 | 醫療、必需消費 | 科技、非必需消費 |
| **衰退期** | 必需消費、醫療、公用事業 | 科技（防禦型） | 金融、工業、原物料 |

**詳細框架參考：** `references/frameworks/sector-rotation-strategy.md`

---

### Step 2: 機構報告整合與共識追蹤

**追蹤全球頂尖機構：**

- **頂級投行：** J.P. Morgan, Goldman Sachs, Morgan Stanley, BofA, Citi
- **資產管理：** BlackRock, Vanguard, Fidelity
- **對沖基金：** 追蹤 13F 文件（Bridgewater, Pershing Square, Tiger Global）
- **管理顧問：** McKinsey, BCG, Forrester, Gartner

**機構共識評分系統：**

```
一致看多（5 分）：≥80% 機構推薦超配
偏多（4 分）：60-79% 機構推薦超配
中性（3 分）：40-59% 機構推薦超配
偏空（2 分）：20-39% 機構推薦超配
一致看空（1 分）：<20% 機構推薦超配
```

**詳細方法參考：**

- `references/institutional/institutional-reports-tracking.md`
- `references/institutional/13f-holdings-analysis.md`
- `references/institutional/consensus-scoring-system.md`

---

### Step 3: 產業深度分析（七步驟框架）

針對目標產業執行標準化分析：

1. **產業鏈拆解** - 上中下游價值鏈與利潤分配
2. **供需關係分析** - 需求驅動、產能利用率、庫存週期
3. **競爭格局分析** - 市場集中度（HHI）、龍頭企業護城河
4. **技術與政策驅動** - 破壞性創新、政府補貼與法規支持
5. **產業估值水準** - 本益比歷史分位數、相對估值
6. **領先與落後指標** - 設定預警指標與觸發條件
7. **泡沫風險評估** - 估值、情緒、基本面、機構面檢查清單

**詳細框架參考：**

- `references/frameworks/industry-lifecycle-analysis.md`
- `references/frameworks/supply-demand-framework.md`
- `references/frameworks/competitive-landscape-framework.md`
- `references/frameworks/bubble-risk-assessment.md`

---

### Step 4: 核心投資趨勢評估

**2026 年六大核心趨勢：**

1. **AI 算力革命**（優先級：⭐⭐⭐⭐⭐）
2. **軍備與國防**（優先級：⭐⭐⭐⭐⭐）
3. **核電復興**（優先級：⭐⭐⭐⭐）
4. **去美元化（黃金 + 穩定幣）**（優先級：⭐⭐⭐⭐）
5. **稀土與關鍵礦物**（優先級：⭐⭐⭐）
6. **穩定幣與區塊鏈基礎設施**（優先級：⭐⭐⭐）

**長期趨勢主題（3-5 年）：**

- 電動車供應鏈、6G 網路、金融科技、AI 製藥、GLP-1 肥胖藥

**非主流趨勢（待爆發）：**

- 人形機器人、醫療 AI、量子電腦

**詳細分析參考：**

- `references/themes/six-core-themes-2026.md`
- `references/themes/long-term-themes.md`
- `references/themes/emerging-themes.md`

---

### Step 5: 產業輪動策略制定

**輪動時機判斷（滿足任一即啟動）：**

- 經濟週期階段轉換
- 央行政策立場轉向
- 產業供需關係逆轉
- 機構共識評分變化 ≥1.0 分
- 關鍵領先指標連續 2 個月轉向

**2026 年產業配置建議：**


| 產業 | 配置權重 | 配置邏輯 |
| :-- | :-- | :-- |
| **科技（AI 相關）** | 25-30% | 機構一致看多，挑選營收兌現者 |
| **國防軍備** | 10-15% | 地緣政治持續，歐洲軍備化 |
| **核電與能源** | 8-12% | AI 用電需求，長期結構性成長 |
| **金融** | 12-15% | 利差穩定，降息預期利多 |
| **醫療（含 GLP-1）** | 10-12% | 防禦性 + 肥胖藥增長 |
| **現金 / 債券** | 10-15% | 保留彈性，等待回檔 |

**詳細策略參考：** `references/frameworks/sector-rotation-strategy.md`

---

### Step 6: 產業研究報告產出

**報告格式選擇：**

- 單一產業深度報告（15-20 頁）
- 多產業比較報告（10-15 頁）
- 產業輪動策略報告（8-12 頁）
- 機構共識追蹤報告（5-8 頁）
- 產業快訊（2-3 頁）

**標準報告結構：**

1. 執行摘要（產業評級、核心觀點、投資建議）
2. 總經環境與產業定位
3. 產業鏈與價值分配
4. 供需分析
5. 競爭格局
6. 技術與政策驅動
7. 估值與配置建議
8. 風險評估與領先指標追蹤

**報告範本參考：**

- `references/templates/industry-report-template.md`
- `references/templates/sector-comparison-template.md`
- `references/templates/rotation-decision-checklist.md`

---

## 參考資料

### 內部文件（核心框架）

**分析框架：**

- `references/frameworks/industry-lifecycle-analysis.md` - 產業生命週期與七步驟分析
- `references/frameworks/supply-demand-framework.md` - 供需分析方法論
- `references/frameworks/competitive-landscape-framework.md` - 競爭格局評估
- `references/frameworks/sector-rotation-strategy.md` - 產業輪動策略手冊
- `references/frameworks/bubble-risk-assessment.md` - 泡沫風險評估框架

**機構追蹤：**

- `references/institutional/institutional-reports-tracking.md` - 投行報告追蹤指引
- `references/institutional/13f-holdings-analysis.md` - 對沖基金持倉分析
- `references/institutional/consensus-scoring-system.md` - 機構共識評分系統

**投資主題：**

- `references/themes/six-core-themes-2026.md` - 六大核心趨勢深度分析
- `references/themes/long-term-themes.md` - 長期趨勢評估（3-5 年）
- `references/themes/emerging-themes.md` - 非主流趨勢（待爆發）

**數據來源：**

- `references/data-sources/industry-data-sources.md` - 產業數據來源清單
- `references/data-sources/leading-indicators.md` - 領先指標追蹤方法
- `references/data-sources/etf-flow-tracking.md` - ETF 資金流向追蹤

**實用範本：**

- `references/templates/industry-report-template.md` - 產業研究報告範本
- `references/templates/sector-comparison-template.md` - 產業比較分析範本
- `references/templates/rotation-decision-checklist.md` - 輪動決策檢查清單


### 外部資源（精選）

**頂級投行研究：**

- [J.P. Morgan Markets](https://www.jpmorgan.com/insights/research)
- [Goldman Sachs Research](https://www.goldmansachs.com/insights/pages/top-of-mind.html)
- [Morgan Stanley Research](https://www.morganstanley.com/ideas)
- [BlackRock Investment Institute](https://www.blackrock.com/corporate/insights/blackrock-investment-institute)

**產業數據追蹤：**

- [SEMI](https://www.semi.org/) - 半導體設備與材料
- [IEA](https://www.iea.org/) - 全球能源數據
- [SIPRI](https://www.sipri.org/) - 全球軍費資料庫
- [FDA Approvals](https://www.fda.gov/) - 新藥批准追蹤

**13F 持倉追蹤：**

- [SEC EDGAR](https://www.sec.gov/edgar) - 官方 13F 文件
- [WhaleWisdom](https://whalewisdom.com/) - 13F 整合分析
- [Dataroma](https://www.dataroma.com/) - 超級投資人持倉

**完整資源清單參考：** `references/data-sources/industry-data-sources.md`

---

## 常見問題

**Q1: 產業研究與個股研究的順序？**
建議順序：總經分析 → 產業研究 → 個股分析。選對產業，成功機率提升 50%。

**Q2: 如何判斷產業處於生命週期的哪個階段？**
使用三指標：營收成長率、市場滲透率、競爭格局。詳見 `references/frameworks/industry-lifecycle-analysis.md`

**Q3: 機構報告這麼多，如何高效篩選？**
三層過濾：機構權重（只看頂級投行）→ 報告類型（聚焦戰略報告）→ 時效性（優先最近 1 個月）

**Q4: 產業輪動的最佳時機？**
領先市場 1-2 個月最佳，使用輪動訊號確認檢查表（至少滿足 3 項條件）。

**Q5: 如何避免產業配置過度集中？**
使用「331 配置原則」：單一產業上限 30%、前三大合計 60-70%、其他分散 30-40%。

**更多 FAQ 參考：** 完整版說明文件

---

## 版本歷史

### v2.0.0 (2026-01-07) - Progressive Disclosure 重構

**核心改進：**

- ✅ 採用 Progressive Disclosure 設計，主文件精簡至 ~400 行
- ✅ 詳細框架、數據源、範本移至 references 目錄
- ✅ 改善可讀性與學習曲線
- ✅ 保持完整功能性，降低初學門檻

**參考官方 skill-creator 結構：**

- 主 SKILL.md 聚焦核心概念與執行流程
- References 分層組織：frameworks / institutional / themes / data-sources / templates
- 提供清晰的文件導航路徑


### v1.0.0 (2026-01-07) - Initial Release

完整功能實現，包含七步驟分析框架、機構共識追蹤、產業輪動策略。

---

## 使用指南

**新手（0-3 個月）：**

1. 閱讀本 SKILL.md 了解核心概念
2. 從 `references/frameworks/` 學習基礎分析框架
3. 追蹤 2-3 個感興趣的產業，練習七步驟分析

**進階（3-12 個月）：**

1. 深度研究六大核心趨勢（參考 `references/themes/`）
2. 每月追蹤機構共識變化（參考 `references/institutional/`）
3. 實戰產業輪動配置，記錄決策與結果

**專家（12 個月以上）：**

1. 建立個人產業研究體系
2. 開發自動化數據追蹤工具
3. 產出高品質產業研究報告

---

**文檔版本：** v2.0.0
**最後更新：** 2026-01-07
**作者：** Evan
**下次更新：** 每季度更新機構共識與核心趨勢
