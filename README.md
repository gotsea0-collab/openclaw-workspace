# Kiwoom Quant Trading System v2.0

Public-safe GitHub edition of the Kiwoom Quant Trading System v2.0 documentation set.

## Scope
This repository is a documentation-first, public-safe release focused on:
- system architecture
- strategy coordination
- oversold rebound execution framework
- execution rules and risk controls

## Excluded from public release
The following are intentionally excluded from this GitHub-safe edition:
- real Kiwoom API keys / secrets
- account numbers
- Telegram bot tokens
- private memory files
- runtime logs
- local automation scratch scripts
- live trading credentials and execution secrets

## Core documents
- `CORE_MODELS_DOCUMENTATION.md`
- `KIWOOM_QUANT_TRADING_SYSTEM_V2_0_REORGANIZED.md`
- `KIWOOM_V2_FINAL_EXECUTION_SHEET.md`
- `strategy_coordination_guide.md`

## Trading discipline
- REAL ONLY in private deployment
- Asia/Seoul as the single market clock
- permanent separation of:
  1. market regime judgment
  2. candidate judgment
  3. news-risk judgment
- oversold rebound universe restricted to:
  - KOSPI200
  - KOSDAQ150

## Publication note
This repo is intended for framework sharing and documentation review. It is not a public dump of a live trading environment.
