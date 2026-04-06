# Kiwoom Quant Trading System v2.0

Public-safe GitHub edition of the Kiwoom Quant Trading System v2.0.

## What this repository contains
This repository is a documentation-first, public-safe release focused on:
- system architecture
- strategy coordination
- oversold rebound execution framework
- execution rules and risk controls
- publishable project structure for review and collaboration

## Core principles
- REAL ONLY in private deployment
- Asia/Seoul as the single market clock
- permanent separation of:
  1. market regime judgment
  2. candidate judgment
  3. news-risk judgment
- oversold rebound universe restricted to:
  - KOSPI200
  - KOSDAQ150

## Included files
- `CORE_MODELS_DOCUMENTATION.md`
- `KIWOOM_QUANT_TRADING_SYSTEM_V2_0_REORGANIZED.md`
- `KIWOOM_V2_FINAL_EXECUTION_SHEET.md`
- `SYSTEM_STRUCTURE.md`
- `strategy_coordination_guide.md`
- `config.example.json`
- `tomorrow_trading_checklist.md`

## Public-safe publication policy
The following are intentionally excluded from this public repository:
- real Kiwoom API keys / secrets
- account numbers
- Telegram bot tokens
- private memory files
- runtime logs
- local automation scratch scripts
- live trading credentials and execution secrets
- sensitive internal workspace files

## Suggested next code modules for public refactor
If you want to evolve this repo into a cleaner public engineering project, the next recommended modules are:
- `market_session_engine.py`
- `strategy_window_router.py`
- `execution_gate.py`
- `orchestration_layer.py`

These should be published only after credential stripping and local-path cleanup.

## Publication note
This repository is intended for framework sharing, documentation review, and future collaboration. It is not a raw dump of a live trading environment.
