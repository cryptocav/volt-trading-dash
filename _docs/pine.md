---
layout: default
title: "📈 PineScripts"
permalink: /pine/
image: /assets/images/volt_X.png
nav_order: 3
---

# 📈 PineScripts

This page hosts the current **PRISM** PineScript template used by the VOLT system.

PRISM dynamically allocates USDC across top-performing crypto assets using momentum, trend, and volatility filters.  
The PineScript version below implements the core signal logic — allowing for visual inspection and alert generation in TradingView.

> ⚠️ _Note: PRISM is in active testing. Parameters shown here are optimised for a particular research window and sector mix — and may evolve as the system matures._

---

## 📈 PRISM Entry Signal (1D)

//@version=5  
indicator("PRISM Entry Signal (1D)", overlay=true)

// === USER INPUTS ===
momentumWindow    = input.int(12,       title="Momentum Window",                  minval=1)
trendSpan         = input.int(8,        title="Trend EMA Span",                   minval=1)
useVolatility     = input.bool(true,    title="Enable Volatility Filter")
volThreshold      = input.float(0.07,   title="Volatility Threshold (ATR/Close)",   step=0.01, minval=0.0)
useADX            = input.bool(false,   title="Enable ADX Filter")
adxThreshold      = input.int(20,       title="ADX Threshold",                     minval=1)
enableVolumeCheck = input.bool(false,   title="Enable Min Volume Filter")
minVolume         = input.float(100000, title="Min Daily Volume",                  step=1000, minval=0)

// === CALCULATIONS ===
momentum = ta.valuewhen(barstate.islast, close / close[momentumWindow] - 1, 0)
plot(momentum, title="Momentum", color=color.new(color.teal, 70), display=display.none)

emaTrend   = ta.ema(close, trendSpan)
isTrending = close > emaTrend
plot(emaTrend, title="Trend EMA", color=color.orange)

atrValue   = ta.atr(14)
volatility = atrValue / close
volPass    = not useVolatility or (volatility < volThreshold)
plot(useVolatility ? volatility : na, title="Volatility (ATR/Close)", color=color.fuchsia)

[pdiValue, mdiValue, rawAdx] = ta.dmi(14, 14)
adxValue = useADX ? rawAdx : na
adxPass  = not useADX or (adxValue >= adxThreshold)
plot(useADX ? adxValue : na, title="ADX (14)", color=color.blue)

volPass2 = not enableVolumeCheck or (volume >= minVolume)
plot(enableVolumeCheck ? volume : na, title="Volume", color=color.yellow)

// === ENTRY SIGNAL ===
entry = isTrending and (momentum > 0) and volPass and adxPass and volPass2

// === BACKGROUND HIGHLIGHTING (SINGLE LINE) ===
bgcolor(not isTrending ? color.new(color.red, 90) : not volPass ? color.new(color.gray, 90) : not adxPass ? color.new(color.purple, 90) : not volPass2 ? color.new(color.blue, 90) : entry ? color.new(color.green, 90) : na)

// === ENTRY MARKER (SINGLE LINE) ===
plotshape(entry, title="PRISM Entry", location=location.belowbar, color=color.lime, style=shape.triangleup, size=size.small)

// === ALERT CONDITION (SINGLE LINE) ===
alertcondition(entry, title="PRISM Entry Alert", message="PRISM entry triggered on {{ticker}}")

---

That’s it — no other PineScripts are currently active in VOLT’s public allocation model.  
As PRISM matures, this section will evolve to include additional variants (sector-tuned models, live-tuned versions, etc).

Stay sharp.  
—— cavpatrol
