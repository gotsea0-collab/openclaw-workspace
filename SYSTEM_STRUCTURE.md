# System Structure

## Core control layers

### 1. market_session_engine.py
Responsible for Korea market session classification under Asia/Seoul.

### 2. strategy_window_router.py
Routes strategies by time window and disallows invalid actions outside their windows.

### 3. execution_gate.py
Applies hard execution checks before any order action.

### 4. orchestration_layer.py
Coordinates market regime, candidate selection, news-risk review, execution, and post-trade management.

## Strategy layers
- main_model
- momentum_strategy
- mean_reversion_strategy
- oversold_rebound_strategy

## Oversold rebound model summary
- Universe restricted to KOSPI200 + KOSDAQ150
- 15:00-15:20 observation / scoring
- 15:20-15:28 execution
- next day +5%: sell 50%
- next day -2%: stop loss
- next day 10:00: primary exit reference
- if KOSPI/KOSDAQ weakens, direct exit allowed

## Permanent separation
1. market regime judgment
2. candidate judgment
3. news-risk judgment
