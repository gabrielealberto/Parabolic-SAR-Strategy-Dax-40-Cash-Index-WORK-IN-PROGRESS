# Parabolic-SAR-Strategy-Dax-40-Cash-Index WORK IN PROGRESS
Version: 4.10 (London Session Filter)
Author: Gabriele
Platform: MetaTrader 5 (MQL5)

📋 Overview

Parabolic SAR ADX Risk is a trend-following Expert Advisor (EA) designed for trading the DAX40 (GER40) Cash Index.

The strategy is entirely based on Parabolic SAR market structure, enhanced with:

ADX for volatility and directional strength confirmation

Higher Timeframe Parabolic SAR filter to align trades with the dominant trend

Strict percentage-based risk management

ATR-based Stop Loss

Automated Break-Even at 1R

London session time filter for trade entries

The EA is suitable for ESMA-regulated accounts with limited leverage (e.g. 1:33).

⚙️ Broker & Instrument Requirements

Instrument: DAX40 / GER40 Cash Index

Timeframe: H1 (1-hour chart)

Broker: Any broker offering DAX (tested on ActivTrades)

Leverage: Compatible with 1:33 due to strict risk calculation

🚀 Strategy Logic
1. Entry Conditions

A new position is opened only when all conditions below are met:

⏱️ Time Filter (London Session)

New trades are allowed only if server time is between:

StartHour = 09:00

EndHour = 17:00

Position management remains active outside trading hours

📈 Main Trigger (H1 – Parabolic SAR)

A Parabolic SAR flip occurs on the main timeframe:

Buy: SAR switches from above price to below price

Sell: SAR switches from below price to above price

🌪️ Volatility & Directional Strength (ADX)

ADX (Period 19) > AdxThreshold (default: 28.0)

Direction confirmation:

Buy: ADX+ > ADX-

Sell: ADX- > ADX+

🧭 Higher Timeframe Trend Filter (Optional)

Uses Parabolic SAR on a secondary timeframe

Independent SAR settings (SarStep_1, SarMax_1)

Trades are allowed only in the direction of the higher timeframe trend

Example:
If H1 generates a Buy signal but the higher timeframe SAR indicates a downtrend, the trade is skipped.

2. Exit Strategy

Trades are closed when any of the following conditions occur:

🔄 Parabolic SAR Reversal (H1)

The position is closed immediately when the Parabolic SAR on H1 flips against the trade direction

🛑 Stop Loss (ATR-Based)

Stop Loss is dynamically calculated as:

Stop Loss = ATR × ATRMultiplier


ATR is measured on the main timeframe

🎯 Take Profit

No fixed Take Profit (default = 0)

Positions are allowed to run with the trend

3. Position Management
🔁 Break Even at 1R

When UseBreakEven = true:

Stop Loss is moved to entry price

Triggered once price reaches 1R (initial risk)

⏱️ Always Active Logic

Break Even and exit management are active 24/7

Only new trade entries are restricted by the session filter

📊 Input Parameters
💰 Money Management
Parameter	Default	Description
RiskPercent	2.0	Percentage of account balance risked per trade
ATRPeriod	14	ATR period used for volatility calculation
ATRMult	1.5	ATR multiplier for Stop Loss distance
📐 Strategy & Indicators (Main)
Parameter	Default	Description
Timeframe	H1	Main signal timeframe
SarStep	0.02	Parabolic SAR acceleration step (H1)
SarMax	0.2	Parabolic SAR maximum acceleration (H1)
AdxPeriod	19	ADX calculation period
AdxThreshold	28.0	Minimum ADX value required to trade
🧭 Trend Filter (Secondary Timeframe)
Parameter	Default	Description
UseTrendFilter	true	Enables higher timeframe Parabolic SAR filter
FilterTF	H1*	Filter timeframe (recommended: H2 or H4)
SarStep_1	0.04	SAR step for filter timeframe
SarMax_1	0.2	SAR max acceleration for filter timeframe

* Note:
Although the default value may be H1, it is strongly recommended to set FilterTF to a higher timeframe than the chart timeframe.

⏱️ Time Filter (London Session)
Parameter	Default	Description
UseTimeFilter	true	Enables session-based entries
StartHour	9	Trading session start (Server Time)
EndHour	17	Trading session end (Server Time)
