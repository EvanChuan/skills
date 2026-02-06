---
name: cross-asset-fund-flow-tracker
description: 自動化追蹤跨資產 ETF 資金流、CFTC COT 大戶持倉、機構持倉(13F)、暗池交易、期權 Gamma Exposure 及系統性流動性，生成多維度「跨資產資金流追蹤報告」，透過七重驗證機制提升分析可靠度。
version: 4.0
last_updated: 2026-02-06
---

# Cross-Asset Fund Flow Tracker (v4.0 - Advanced Institutional Intelligence)

本 Skill 是一個多維度的跨資產資金流分析系統，整合了從微觀機構行為到宏觀流動性的七大數據來源：

## 一、 七大核心數據維度

### 1. 第一層驗證：現貨市場流量 (Real-time Flow)
* **ETF 資金淨流入/流出**：反映散戶與一般機構的實際買賣行為。
* **暗池交易 (Dark Pool Insights)**：追蹤機構在非公開交易所的大額「隱形」買賣單 (Block Trades)。

### 2. 第二層驗證：衍生品與情緒 (Derivatives & Sentiment)
* **CFTC COT 大戶持倉**：揭示期貨市場專業投機者與商業對沖者的真實頭寸（領先指標）。
* **期權 Gamma Exposure (GEX)**：判斷造市商對沖壓力及市場潛在波动性。
* **異常期權活動 (Unusual Options Activity)**：捕捉針對特定價格或時間的大規模方向性押注。

### 3. 第三層驗證：大機構長線持倉 (Long-term Positioning)
* **SEC 13F 持倉報告**：季度追蹤頂級避險基金（如 Bridgewater, Renaissance, Berkshire）的增減倉方向。
* **機構資產配置觀點**：整合 BlackRock, PIMCO, Goldman Sachs 等一線機構的宏觀戰略報告。

### 4. 第四層驗證：系統性流動性 (Systemic Liquidity)
* **央行資產負債表 (Fed/ECB/BoJ)**：追蹤 QE/QT 政策對市場總體流動性的注入或回收。
* **貨幣市場與 Repo 壓力**：監控短期資金融通壓力及貨幣市場基金 (MMF) 的流向。

---

## 二、 預設追蹤資產類別與信號來源

| 資產類別 | 代表 ETF | 對應 COT 期貨 | 進階追蹤維度 |
|---|---|---|---|
| **美股科技** | QQQ | NQ (Nasdaq-100) | GEX, 13F (Big Tech Weighting) |
| **美股價值** | VTV | 無 | 13F (Dividend Reallocation) |
| **美股小型股** | IWM | RTY (Russell 2000) | Dark Pool Print, PCR |
| **黃金/避險** | GLD | GC (COMEX Gold) | Central Bank Gold Reserves |
| **美國公債** | IEF/TLT | TY/US (Treasury) | Reverse Repo (RRP) |
| **加密貨幣** | IBIT/ETH | CME BTC/ETH | On-chain Exchange Flow, GEX |

---

## 三、 分析流程與輸出格式

當使用者下達指令時，Claude 會自動執行：

1. **數據抓取**：檢索 16 大資產類別的最新資金流與持倉數據。
2. **多維驗證 (Multi-Layer Scoring)**：
   * 為每個資產計算「資金溫度分數」 (-3 到 +3)。
   * **分數加權**：13F(長線) 30% + COT(中線) 30% + ETF/暗池(短線) 20% + 期權/情緒 20%。
3. **報告生成**：
   * **資金流向統計表**：包含價格、流量、與大戶信號。
   * **機構一致性檢查**：標註當前「散戶 vs 大機構」的立場差異。
   * **流動性預警系統**：當央行或 Repo 市場出現壓力時發出警示。

---

## 四、 資金溫度分數指南 (Fund Flow Heat Map)

* **+3 (強烈看多)**：13F 機構加倉 + COT 大戶淨多單增加 + ETF 淨流入 + 暗池大買單。
* **0 (中性)**：各項指標產生矛盾或資金處於觀望狀態。
* **-3 (強烈看空)**：大機構撤離 + COT 空單激增 + ETF 大額流出 + Gamma 轉負。

---

## 五、 操作指令範例

* 「整理本週跨資產資金流向報告，包含 13F 的最新趨勢。」
* 「分析最近美股小型股的暗池交易與期權 Gamma 變化。」
* 「檢查比特幣與黃金在大機構持倉上的重合度與資金流動。」

---
**Data Sources**: ETFdb, CFTC, SEC EDGAR (13F), Dark Pool Trackers, Options Volatility Data, Fed H.4.1.
