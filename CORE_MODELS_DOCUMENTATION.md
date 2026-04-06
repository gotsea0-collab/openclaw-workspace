# 核心交易模型文档
## Kiwoom Quant Trading System v1.0-beta-final & 超跌反弹股模型

**创建日期**: 2026年3月29日  
**最后更新**: 2026年3月29日 20:43  
**状态**: ✅ 生产就绪

---

## 🎯 **模型概览**

### **1. Kiwoom Quant Trading System v1.0-beta-final**
- **类型**: 综合量化交易系统
- **状态**: ✅ 已完成16个核心模块
- **原则**: REAL ONLY (禁止模拟数据)
- **用途**: 主要交易模型，长期持仓管理

### **2. 超跌反弹股模型**
- **类型**: KOSPI200 / KOSDAQ150 隔夜超跌修复策略
- **状态**: ✅ 长期规则已固化
- **特点**: 15:00 观察，15:20-15:28 买入，次日 +5% 先卖 50%，12:00 前全部卖掉
- **用途**: 增强收益模型，隔夜到次日中午交易

---

## 📁 **文件结构**

### **核心目录** (`core_models/`)
```
core_models/
├── config.json                    # 系统配置文件
├── kiwoom_quant_system.py        # 主系统入口
├── core/                         # 16个核心模块
│   ├── token_manager.py
│   ├── safe_api_call.py
│   ├── account_service.py
│   ├── market_data_service.py
│   ├── market_snapshot_builder.py
│   ├── stock_filter.py
│   ├── scoring_engine.py
│   ├── strategy_engine.py
│   ├── risk_manager.py
│   ├── order_manager.py
│   ├── order_state_machine.py
│   ├── execution_engine.py
│   ├── position_manager.py
│   ├── performance_monitor.py
│   ├── memory_manager.py
│   └── scheduler.py
└── README.md                     # 核心模型文档
```

### **临时脚本** (`temp_scripts/`)
- 测试脚本、临时分析脚本、一次性执行脚本
- 可随时清理，不影响核心功能

### **备份目录** (`backup_20260329/`)
- 历史版本备份
- 重要修改前的快照

---

## 🔧 **核心配置**

### **账户配置** (`config.json`)
```json
{
  "environment": "real",
  "account": {
    "account_id": "4000602111",
    "base_url": "https://api.kiwoom.com",
    "app_key": "I4Qz5MMGg1f5hZpxF57_qOqdbDRtJG1-shhQhRRCZFc",
    "app_secret": "U7mJ8Y07gFLMMk3f9pAy3C7OMRpyt624W77yIY8-EE8"
  },
  "trading": {
    "max_position_per_stock": 0.10,
    "max_strategy_allocation": 0.30,
    "daily_loss_limit": -0.03
  }
}
```

### **策略配置**
```json
{
  "strategies": {
    "oversold_rebound": {
      "name": "超跌反弹股模型",
      "risk_management": {
        "stop_loss_pct": -0.02,
        "take_profit_pct": 0.035,
        "prev_day_drop_pct": -0.10
      },
      "buy_conditions": {
        "rebound_min": 0.015,
        "volume_min": 800000
      }
    }
  }
}
```

---

## ⚙️ **Kiwoom Quant Trading System v1.0-beta-final**

### **核心特性**
1. **REAL ONLY原则**: 所有数据来自实盘API，禁止模拟
2. **16模块架构**: 完整的企业级交易系统
3. **风险优先**: 严格的风险控制体系
4. **自动化执行**: 支持计划任务和实时监控

### **模块功能**
| 模块 | 功能 | 状态 |
|------|------|------|
| token_manager | API令牌管理 | ✅ |
| safe_api_call | 安全API调用 | ✅ |
| account_service | 账户查询服务 | ✅ |
| market_data_service | 市场数据服务 | ✅ |
| market_snapshot_builder | 市场快照 | ✅ |
| stock_filter | 股票筛选 | ✅ |
| scoring_engine | 评分引擎 | ✅ |
| strategy_engine | 策略引擎 | ✅ |
| risk_manager | 风险管理 | ✅ |
| order_manager | 订单管理 | ✅ |
| order_state_machine | 订单状态机 | ✅ |
| execution_engine | 执行引擎 | ✅ |
| position_manager | 持仓管理 | ✅ |
| performance_monitor | 绩效监控 | ✅ |
| memory_manager | 记忆管理 | ✅ |
| scheduler | 任务调度 | ✅ |

---

## 🎯 **KR_Oversold_Rebound_V2 策略详情**

### **策略目标**
针对韩国股市"超跌反弹"机会，执行两套短线交易方案。

### **两套执行方案**
#### **方案一：尾盘买入，次日13:00前卖出**
- 时间: 前一交易日 15:00~15:30 买入
- 卖出: 次日 13:00 前全部平仓
- 适用: A类优先，B类次之

#### **方案二：早盘确认买入，13:00前卖出**
- 时间: 次日 09:05~09:25 买入
- 卖出: 当日 13:00 前全部平仓
- 适用: 市场环境确认后执行

### **股票分类**
#### **A类 = 错杀股**
- 跌幅: -8% ~ -5%
- 市值: ≥1000亿韩元
- 股价: ≥1000韩元
- 成交额: ≥50亿韩元
- 技术指标: RSI14≤40, bias20≤-5, ma20≥ma60
- 基本面: 无风险标志

#### **B类 = 超跌博弈股**
- 跌幅: ≤-10%
- 市值: ≥1000亿韩元
- 股价: ≥1000韩元
- 成交额: ≥50亿韩元
- 基本面: 无风险标志

#### **C类 = 禁止交易**
- 审计问题、管理种目、财务恶化等

### **市场决策层**
```python
def market_score(us_change, kr_preopen, vix_change):
    score = 0
    if us_change > 1: score += 1
    elif us_change < -1: score -= 1
    if kr_preopen > 0.5: score += 1
    elif kr_preopen < -0.5: score -= 1
    if vix_change > 5: score -= 1
    return score

def should_trade(market_score_value):
    return market_score_value >= 0
```

### **仓位与风控**
1. **总仓位控制**: 超跌反弹策略总持仓 ≤ 总资产30%
2. **单票仓位上限**: 
   - A类 ≤ 15%
   - B类 ≤ 10%
   - C类 = 0%
3. **硬风控规则**:
   - 单日最大亏损 ≤ 总资产2%
   - 连续2笔亏损，当天停止交易
   - 不允许亏损加仓
   - 13:00前必须全部平仓

---

## ⚖️ **多策略协同规则**

### **资金分配建议**
```
总资金: 100%
├── Kiwoom Quant System: 70% (主要模型)
├── KR_Oversold_Rebound_V2: 20% (增强模型)
└── 现金储备: 10% (应急缓冲)
```

### **冲突解决优先级**
1. **时间敏感度优先**: 超跌模型 > 主要模型
2. **风险控制优先**: 止损 > 止盈
3. **资金使用优先**: 超跌模型专用资金单独预留

### **协同工作流程**
```
每日流程:
08:50 - 市场环境评估，确定当日策略
09:00 - 开盘监控，检查买入条件
09:05 - 超跌模型执行窗口开始
09:25 - 超跌模型买入完成
09:30 - 主要模型开始运行
11:55 - 超跌模型卖出执行
13:00 - 超跌模型必须全部平仓
15:00 - 主要模型当日操作结束
```

---

## 📊 **绩效监控指标**

### **Kiwoom Quant System**
- 年化收益率目标: 15-20%
- 最大回撤控制: ≤15%
- 胜率目标: ≥55%
- 夏普比率目标: ≥1.2

### **KR_Oversold_Rebound_V2**
- 年化收益率目标: 20-30%
- 单笔胜率目标: ≥60%
- 盈亏比目标: ≥2:1
- 最大连续亏损: ≤3笔

### **组合绩效目标**
- 总年化收益率: 35-50%
- 组合夏普比率: ≥1.5
- 最大回撤: ≤20%
- 资金利用率: 70-80%

---

## 🔄 **维护与更新**

### **日常维护**
1. **每日检查**: 系统状态、API连接、账户余额
2. **每周回顾**: 策略绩效、风险控制效果
3. **每月优化**: 参数调整、策略改进

### **版本控制**
- 重大修改前创建备份
- 核心配置文件版本化管理
- 策略参数变更记录

### **故障处理**
1. **API故障**: 自动重试，失败后暂停交易
2. **系统故障**: 切换到手动模式，优先处理风险仓位
3. **网络故障**: 本地缓存，网络恢复后同步

---

## 🚀 **明日交易准备 (2026年3月30日)**

### **超跌模型目标股票**
1. **011200 HMM** (A类，前日跌幅-12.8%)
   - 目标数量: 73股
   - 预计投资: 1,350,500 KRW
   - 止损: -2% (18,150 KRW)
   - 止盈: +3.5% (19,168 KRW)

2. **010130 고려아연** (A类，前日跌幅-11.5%)
   - 目标数量: 2股
   - 预计投资: 1,040,000 KRW
   - 止损: -2% (511,070 KRW)
   - 止盈: +3.5% (539,753 KRW)

### **资金分配**
```
总可用资金: 13,523,700 KRW
├── 超跌模型专用: 2,700,000 KRW (20%)
├── 主要模型使用: 9,470,000 KRW (70%)
└── 现金储备: 1,353,700 KRW (10%)
```

### **时间安排**
- 08:50: 盘前准备，系统检查
- 09:00: 开盘监控，条件验证
- 09:05: 超跌模型买入执行
- 09:30: 主要模型开始运行
- 11:55: 超跌模型卖出执行
- 13:00: 超跌模型必须全部平仓

---

## 📝 **重要提醒**

### **必须遵守的原则**
1. **REAL ONLY**: 永远使用实盘API和真实账户
2. **风险优先**: 亏损控制比盈利更重要
3. **纪律执行**: 严格遵守时间窗口和条件
4. **策略隔离**: 各策略独立核算，避免混淆

### **禁止行为**
1. ❌ 使用模拟数据或mock API
2. ❌ 超过仓位限制
3. ❌ 违反时间纪律
4. ❌ 忽略风险控制信号

### **成功关键**
1. ✅ 严格的纪律执行
2. ✅ 持续的风险管理
3. ✅ 定期的策略优化
4. ✅ 系统的绩效监控

---

**文档版本**: v1.0  
**创建人**: Kiwoom Quant Trading System  
**下次审查**: 2026年4月5日