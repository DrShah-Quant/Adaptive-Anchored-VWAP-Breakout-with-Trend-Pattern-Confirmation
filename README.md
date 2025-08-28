# Adaptive Anchored VWAP Breakout with Trend-Pattern Confirmation

## 📌 Strategy Description

This algorithmic trading strategy combines **anchored VWAP dynamics**, **trend classification**, and **pattern-based breakout confirmation** to detect and trade sustainable uptrend breakouts with adaptive risk control.

### 🔹 Core Logic
1. **Trend Classification**
   - Rolling windows of price are analyzed and classified into:
     - **Uptrend (1)**
     - **Downtrend (0)**
     - **Sideways / Neutral (-1)**
   - Macro **swing highs and lows** are extracted to anchor breakout zones.

2. **Anchored VWAP as Dynamic Benchmark**
   - VWAP is anchored at **local highs and lows**.  
     **Formula:**  
    VWAP = ( Σ(Price × Volume) ) / ( Σ Volume )

   - Acts as **dynamic support/resistance**, reflecting institutional accumulation/distribution.

3. **Buy Entry Conditions**
   - Price dips below the **highest low**, but reclaims above **1.05 × Anchored VWAP**.  
   - Adaptive position sizing:
     - **20% of equity** for initial entry.  
     - Scale-in **30–60%** if price improves relative to average cost.  
   - **Stop-loss:** max of  
     - 8% below entry OR  
     - Previous swing low.  
   - **Take profit:**  
     - +8% (standard) OR  
     - 3× entry (early-stage breakout).

4. **Sell Exit Conditions**
   - Triggered if:
     - New swing lows form (trend weakening).  
     - **High slope analysis** indicates fading momentum.  
     - Price rises ≥ 8% above average entry.  
   - Full or partial exits executed via `AlgoAPIUtil.OrderObject`.

5. **Risk & Capital Management**
   - Initial capital: **100,000 units**.  
   - Position sizes adjust dynamically with average entry price.  
   - Strict stop-loss prevents excessive drawdowns.

---

### 📊 Strategy Interpretation
- **Range-Bound Phase (Inside Swing Band):**  
  Awaits breakout above anchored VWAP with confirmation.  
- **Above Anchored VWAP:**  
  Institutional buy pressure → **validated breakout entry**.  
- **Weakening Highs:**  
  Signals **trend exhaustion** → close positions.  
- **Early Accumulation Phase:**  
  Small allocation (~5%) with wide TP (3×) for early movers.

---

## 📚 Libraries & Tools
- **AlgoAPI**
  - `AlgoAPIUtil` → Order creation, execution control.  
  - `AlgoAPI_Backtest` → Simulation & event-driven backtesting.  
- **datetime**  
  - Used for time-based reference IDs and slope computations.  

---

⚡ **Adaptive Anchored VWAP Breakout with Trend-Pattern Confirmation** leverages  
institutional VWAP dynamics, breakout recognition, and adaptive scaling rules  
to maximize gains during **sustainable uptrend continuations** while enforcing disciplined risk control.
