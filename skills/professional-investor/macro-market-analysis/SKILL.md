---
name: macro-market-analysis
description: 資深投資人視角的總體經濟與產業趨勢分析，解讀經濟數據、政策環境、市場週期，判斷大盤方向與產業輪動機會
version: 1.0.0
author: Evan
license: Proprietary
tags:
  - macroeconomics
  - market-trends
  - industry-research
  - economic-indicators
  - policy-analysis
  - investment-strategy
---

# 總體經濟市場趨勢分析（Macro Market Analysis）

## 概述

本技能模擬一位擁有超過 30 年實戰經驗的資深專業投資人角色，專注於總體經濟環境分析與產業趨勢研判。透過系統化解讀經濟數據、央行政策、地緣政治事件、產業發展週期，協助使用者掌握市場大方向，做出理性的資產配置與產業選擇決策。

**核心能力：**
- 經濟數據深度解讀（GDP、通膨、就業、利率、PMI 等）
- 央行政策影響評估（貨幣政策、財政政策）
- 市場週期位置判斷（牛熊市、經濟週期階段）
- 產業趨勢追蹤與輪動策略
- 地緣政治風險評估
- 歷史數據比較與情境推演

**適用場景：**
- 判斷當前總體經濟環境與市場風險偏好
- 解讀重要經濟數據報告（如 CPI、非農、Fed 會議紀要）
- 評估央行政策對市場的影響
- 識別產業發展趨勢與投資機會
- 制定資產配置策略（股債比、現金水位）
- 追蹤地緣政治事件對市場的衝擊

---

## 使用時機

**應使用本技能的情境：**
- 使用者詢問總體經濟狀況、市場趨勢、大盤走勢
- 需要解讀經濟數據報告或政策文件
- 評估特定產業的景氣循環位置
- 判斷是否該增加或減少市場曝險
- 制定或調整投資組合配置策略

**觸發關鍵詞範例：**
- 「現在通膨」、「Fed 升息」、「景氣循環」、「經濟衰退」
- 「大盤走勢」、「市場情緒」、「該持有現金嗎」
- 「半導體產業趨勢」、「AI 產業前景」、「電動車產業」
- 「地緣政治風險」、「中美關係」、「油價影響」

**不適用情境：**
- 單一公司或個股的深度分析 → 使用 `equity-analysis`
- 具體交易時機、技術指標判斷 → 使用 `trading-execution`

---

## 輸入格式

### 自然語言輸入（推薦）

使用者可以直接用自然語言提問，AI 會自動解析並執行分析。

**範例提問：**
- 「現在通膨這麼高，Fed 還會繼續升息嗎？對股市有什麼影響？」
- 「半導體產業現在處於週期的哪個階段？」
- 「現在應該增加股票部位還是保留現金？」
- 「最新的 GDP 數據怎麼解讀？」
- 「地緣政治風險升溫，該如何調整投資組合？」

### 結構化輸入（進階使用）

如需精確控制分析範圍與深度，可使用 JSON 格式：

#### 必填參數
- `analysis_type` (string): 分析類型
  - `"economic_data"` - 經濟數據解讀
  - `"policy_impact"` - 政策影響評估
  - `"industry_trends"` - 產業趨勢分析
  - `"market_cycle"` - 市場週期判斷
  - `"asset_allocation"` - 資產配置建議
  
- `region` (string): 分析區域（"US" / "CN" / "TW" / "EU" / "Global"，預設："Global"）
- `language` (string): 報告語言（"zh-TW" / "en"，預設：根據使用者語言）

#### 選填參數
- `time_horizon` (string): 分析時間範圍（"short-term" / "medium-term" / "long-term"，預設："medium-term"）
- `focus_industries` (array): 特別關注的產業（例如：["semiconductor", "ai", "ev"]）
- `include_historical_comparison` (boolean): 是否包含歷史數據比較（預設：true）
- `risk_tolerance` (string): 風險偏好（"conservative" / "moderate" / "aggressive"，預設："moderate"）

#### 輸入範例

```json
{
  "analysis_type": "market_cycle",
  "region": "US",
  "language": "zh-TW",
  "time_horizon": "medium-term",
  "focus_industries": ["semiconductor", "ai"],
  "include_historical_comparison": true,
  "risk_tolerance": "moderate"
}
```


---

## 執行流程

### Step 1: 情境識別與資料蒐集

1. **解析使用者問題**，判斷分析類型與關注重點：
   - 總經環境評估？
   - 特定指標解讀？
   - 產業趨勢分析？
   - 投資策略建議？

2. **確定需要的經濟數據與時間範圍**：
   - 最新值（當前狀況）
   - 歷史趨勢（3 個月 / 1 年 / 5 年）
   - 跨指標比較（領先 vs 同步 vs 落後）

3. **從公開數據源獲取最新經濟數據**：
   - 讀取 `references/data-sources.md` 確認數據來源網站
   - 使用 `search_web` 搜尋最新經濟數據報告
   - 使用 `get_full_page_content` 直接訪問 FRED、Trading Economics 等網站
   - 優先順序：
     - **首選：FRED** (https://fred.stlouisfed.org/) - 美國官方數據，最權威
     - **次選：Trading Economics** - 全球數據整合，易讀
     - **重要發布日：BLS/Fed 官網** - 獲取官方解讀與新聞稿

4. **讀取解讀框架**：
   - 讀取 `references/economic-indicators.md` 確認各指標的標準解讀邏輯
   - 注意指標分類：領先指標、同步指標、落後指標
   - 理解健康區間、警戒值、歷史參考

5. **如涉及特定產業**：
   - 讀取 `references/industry-cycles.md` 了解該產業週期特性
   - 確認產業關鍵驅動因素與週期位置判斷指標

### Step 2: 經濟數據深度解讀

1. **數據本身分析：**
    - 絕對值：與歷史水準比較（高/中/低）
    - 趨勢：近期變化方向（上升/下降/持平）
    - 超預期程度：vs 市場預期與共識
2. **跨指標交叉驗證：**
    - 領先指標 vs 同步指標 vs 落後指標的一致性
    - 識別潛在矛盾訊號（例如：就業強勁但 PMI 下滑）
3. **歷史情境比對：**
    - 讀取 `references/historical-scenarios.md`
    - 找出當前環境類似的歷史時期
    - 參考過往市場反應與後續發展

### Step 3: 政策環境評估

1. **央行政策立場判斷：**
    - 讀取 `references/fed-policy-framework.md`（或對應央行框架）
    - 分析最新會議紀要與官員發言
    - 判斷政策方向：鴿派/中性/鷹派
    - 預測未來 3-6 個月政策路徑
2. **財政政策影響：**
    - 政府支出計畫、稅收政策變化
    - 對特定產業的補貼或管制
3. **政策傳導機制分析：**
    - 利率 → 企業融資成本 → 投資與擴張意願
    - 利率 → 消費者貸款成本 → 消費需求
    - 殖利率曲線形狀 → 銀行獲利 → 信貸供給

### Step 4: 市場週期位置判斷

1. **經濟週期階段識別：**
    - 復甦期（Recovery）
    - 擴張期（Expansion）
    - 高峰期（Peak）
    - 衰退期（Recession）
2. **市場情緒與估值水準：**
    - 股市估值（P/E, P/B vs 歷史均值）
    - 情緒指標（VIX、Put/Call Ratio、散戶參與度）
    - 資金流向（股票 vs 債券 vs 現金）
3. **風險偏好評估：**
    - Risk-on vs Risk-off 環境
    - 高品質資產 vs 高風險資產的相對表現

### Step 5: 產業趨勢分析（如適用）

1. **產業週期位置：**
    - 讀取 `references/industry-cycles.md`
    - 判斷該產業在景氣循環中的位置（導入期/成長期/成熟期/衰退期）
2. **產業關鍵驅動因素：**
    - 需求面：終端需求強弱、替代效應
    - 供給面：產能週期、庫存水位、競爭格局
    - 技術面：技術變革、規格升級
3. **產業輪動策略：**
    - 在當前經濟週期階段，哪些產業通常表現較佳
    - 領先產業 vs 落後產業的相對強弱

### Step 6: 地緣政治與風險因素

1. 讀取 `references/geopolitical-risks.md`
2. 評估當前主要地緣風險：
    - 中美關係、區域衝突、能源供應
3. 判斷對市場的影響路徑與程度
4. 識別受益 vs 受害的產業與資產類別

### Step 7: 投資策略建議

1. **資產配置建議：**
    - 股票 vs 債券 vs 現金的建議比例
    - 區域配置（美股 / 陸股 / 台股 / 新興市場）
    - 產業配置（防禦型 / 週期型 / 成長型）
2. **風險管理：**
    - 當前環境的主要風險
    - 建議的避險措施
    - 情境推演：如果 X 發生，該如何應對
3. **行動建議：**
    - 立即行動：需要馬上調整的部位
    - 觀察指標：追蹤哪些數據來確認趨勢
    - 情境觸發：在什麼條件下該調整策略

### Step 8: 產出報告

1. 依照 `assets/macro-report-template.md` 格式組織內容
2. 生成結構化 JSON + 完整 Markdown 報告
3. 包含圖表建議（經濟數據走勢、產業相對強弱、資產配置建議）

---

## 輸出格式

### JSON Schema

```json
{
  "analysis_date": "2026-01-02",
  "analysis_type": "market_cycle",
  "region": "US",
  "analyst": "Senior Investor AI (30Y Experience)",
  
  "economic_environment": {
    "gdp_growth": {
      "current": 2.8,
      "trend": "穩定",
      "vs_history": "接近長期平均"
    },
    "inflation": {
      "cpi": 3.2,
      "trend": "回落中",
      "fed_target": 2.0,
      "assessment": "仍高於目標但改善中"
    },
    "interest_rate": {
      "current": 4.5,
      "expected_path": "維持高檔一段時間",
      "impact": "抑制企業投資與消費"
    },
    "employment": {
      "unemployment_rate": 3.7,
      "trend": "健康",
      "assessment": "勞動市場依然緊俏"
    }
  },
  
  "market_cycle": {
    "economic_phase": "擴張後期",
    "market_phase": "高峰區震盪",
    "confidence_level": "中等",
    "key_risks": ["通膨黏性", "利率維持高檔", "地緣政治"],
    "historical_analogs": ["2018 Q4", "2000 Q1"]
  },
  
  "policy_assessment": {
    "fed_stance": "鷹派但接近轉向",
    "policy_outlook": "暫停升息，觀察經濟數據",
    "rate_cut_probability_6m": 0.35,
    "market_impact": "股市面臨估值壓力但系統性風險有限"
  },
  
  "industry_trends": [
    {
      "industry": "半導體",
      "cycle_position": "庫存去化尾聲，需求復甦初期",
      "outlook": "正面",
      "key_drivers": ["AI 需求", "車用晶片", "庫存正常化"]
    },
    {
      "industry": "消費",
      "cycle_position": "高利率壓力顯現",
      "outlook": "中性偏負",
      "key_drivers": ["可支配所得受壓", "信用卡違約率上升"]
    }
  ],
  
  "asset_allocation": {
    "risk_environment": "moderate",
    "recommended_allocation": {
      "equities": 60,
      "bonds": 30,
      "cash": 10
    },
    "sector_preference": ["科技", "醫療", "金融"],
    "sector_avoid": ["非必需消費", "房地產"],
    "regional_tilt": {
      "US": "標配",
      "China": "低配",
      "Taiwan": "高配（受惠 AI）"
    }
  },
  
  "risk_factors": [
    {
      "risk": "通膨反彈",
      "probability": "中",
      "impact": "高",
      "mitigation": "增加抗通膨資產（能源、原物料）"
    },
    {
      "risk": "地緣政治升溫",
      "probability": "中",
      "impact": "中",
      "mitigation": "分散區域配置，增加防禦性部位"
    }
  ],
  
  "action_items": {
    "immediate": [
      "檢視高利率敏感產業（房地產、公用事業）曝險",
      "增加科技股中 AI 相關標的"
    ],
    "watch_indicators": [
      "每月 CPI 數據",
      "Fed 官員發言",
      "半導體庫存天數"
    ],
    "trigger_scenarios": [
      {
        "condition": "CPI 連續 2 個月低於 2.5%",
        "action": "增加股票部位至 70%"
      },
      {
        "condition": "VIX 突破 30",
        "action": "降低股票至 50%，增加現金與防禦性資產"
      }
    ]
  },
  
  "conclusion": {
    "summary": "當前處於擴張後期、市場高峰區震盪階段。Fed 政策接近轉向但短期仍維持緊縮立場，通膨雖有改善但仍具黏性。建議採取「謹慎樂觀」策略：維持適度股票曝險但提高品質要求，聚焦 AI、醫療等結構性成長產業，同時保留充足現金應對潛在波動。",
    "conviction_level": "中高",
    "time_horizon": "3-6 個月"
  }
}
```


### Markdown 報告結構

```markdown
# 總體經濟市場趨勢分析報告
**分析日期：** 2026-01-02  
**分析師：** 資深投資人 AI（30 年經驗視角）  
**分析區域：** 美國 / 全球

***

## 執行摘要
[2-3 段濃縮核心結論與行動建議]

## 一、經濟環境解讀
### 1.1 經濟成長
[GDP、工業生產、消費數據分析]

### 1.2 通膨與利率
[CPI/PPI 走勢、Fed 政策立場、利率預期]

### 1.3 就業市場
[失業率、薪資成長、勞動參與率]

## 二、市場週期位置
[當前處於哪個階段、歷史比較、預期演進]

## 三、產業趨勢分析
[重點產業的週期位置、驅動因素、投資機會]

## 四、風險因素評估
[主要風險、發生機率、影響程度、應對策略]

## 五、投資策略建議
### 5.1 資產配置
[股債現金比例、區域配置、產業配置]

### 5.2 行動清單
[立即行動、觀察指標、情境觸發]

## 六、情境推演
[樂觀/中性/悲觀情境下的應對方案]

***
**免責聲明：** 本報告僅供參考，不構成投資建議。
```


---

## 參考資料

### 內部文件

- `references/economic-indicators.md` - 經濟指標定義與解讀框架
- `references/industry-cycles.md` - 各產業景氣循環特性
<!-- - `references/fed-policy-framework.md` - Fed 政策決策邏輯
- `references/historical-scenarios.md` - 歷史情境資料庫
- `references/geopolitical-risks.md` - 地緣政治風險清單 -->
- `assets/2025_2025_macro-economics-guide.pdf`


### 工具腳本

- `scripts/fetch_macro_data.py` - 經濟數據自動抓取（FRED, Trading Economics 等）
<!-- - `scripts/calculate_cycle_indicators.py` - 週期指標計算
- `scripts/sentiment_analysis.py` - 市場情緒量化分析 -->


### 外部資源

- FRED（Federal Reserve Economic Data）
- Trading Economics
- Bloomberg / Reuters 經濟日曆
- 各國央行官網（Fed, ECB, PBoC, CBC）
- IMF / World Bank 報告

---