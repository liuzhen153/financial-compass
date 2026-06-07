# Financial Compass · 金融指南针

> 个人长期投资研究伙伴 — 用产业链瓶颈理论 + 贝叶斯估值，帮你建立判断能力。

## 定位

```
Compass Scout          Financial Compass      Compass Trader
（指南针侦察兵）        （金融指南针）           （指南针交易者）
      │                      │                      │
  发现热门赛道         深度分析标的           执行模拟交易
  识别爆发前夜         估值+风险+对比         绩效追踪+反思
      │                      │                      │
  WHAT to buy           SHOULD I buy           WHEN & HOW
      │                      │                      │
      └── 赛道委托 ──→ 赛道扫描+选股            ↑
                              │                  │
                              └── 交易参数 ──→ 执行+追踪
                                                 │
                                        绩效反馈 ──┘
```

Financial Compass 处于投资流程的**中间层** — 接收上游 Scout 的赛道委托，输出交易参数给下游 Trader。

## 核心能力

| 模块 | 功能 |
|------|------|
| **股票深度分析** | 产业链 L0-L6 定位 → 14 条卡点判据 → 治理质量评估 → 贝叶斯内在估值 → 反向 DCF → 三情景估值 → Benchmark 三重对比 → 股东回报分析 → 宏观校准 → Adversarial Review |
| **基金穿透分析** | 分类识别 → 底层持仓穿透（前 10 大重仓股用股票引擎分析）→ 经理评估 → 业绩归因 → 费率 20 年侵蚀 → 定投回测 |
| **赛道扫描** | 周期判断 → 供应链栈 L0-L6 → 卡点层定位 → 候选标的筛选 → 逐只反向 DCF → 数据置信度总览 → A 股信号 → 剩余不对称地图 |
| **对比分析** | 双标的并行深度分析 → 逐维度对比表 → 分维度胜负 → 综合推荐 |
| **组合风险分析** | 逐只穿透 → 行业热力图 → 相关性矩阵 → 集中度风险 → 风格暴露 → 优化建议 |
| **可转债分析** | 定性分类（偏股/平衡/偏债）→ 正股评估 → 债底安全 → 条款博弈（强赎/下修/回售） |
| **对抗验证** | 强制输出 Bull case + Bear case + 回应 bear 最强 3 论点 |
| **交易参数输出** | 估值结论为"低估/合理偏低"时，自动输出仓位/止损/止盈/清仓条件给 Compass Trader |

### 贝叶斯估值引擎

以行业均值 + 公司历史增速为锚，设定 H0-H5 六档 CAGR 先验概率，计算加权内在增速 vs 市场隐含增速，输出三情景估值（Base 60% / Bull 20% / Bear 20%）。

### 双引擎搜索

```
AnySearch（行业全景 ~60%）←→ WebSearch（结构化财务 ~40%）
         ↓                            ↓
   batch_search 5 路并行          市值/PE/营收/净利/毛利率/ROE
         交叉验证差异 >20% → 第 3 轮定向复核
```

## 快速开始

在 Claude Code 中：

```
# 股票分析
分析 [股票代码/名称]                # 单股深度分析
[标的] 估值                          # 聚焦估值
[标的] 风险 / 什么会推翻这个判断      # 聚焦证伪条件
[标的] 现在适合买吗                  # 综合分析含时机判断

# 基金分析
分析 [基金代码/名称]                # 基金持仓穿透分析
定投方案 [基金]                      # 定投回测+建议

# 赛道分析
扫描 [板块/赛道]                     # 赛道产业链扫描
[赛道] 有哪些机会                    # 赛道机会扫描

# 对比分析
[A] vs [B] / [A] 和 [B] 对比        # 双标的对比分析

# 组合分析
帮我看看持仓 / 组合分析              # 组合风险分析

# 可转债
分析 [可转债代码/名称]               # 可转债分析

# 交易衔接
一键交易 [标的] / 生成交易参数       # 输出 Trader 交易参数
一键交易 S 级标的                     # 批量输出交易参数

# 复盘
复盘 [标的]                          # 历史判断 vs 实际走势
```

## 输出格式

每次完整分析输出一个 `.md` 文件，含 YAML 元信息和三级置信度标注：

```
个股分析：个股-[股票简称]-[代码后6位]-[YYYYMMDD].md
基金分析：基金-[基金简称]-[代码后6位]-[YYYYMMDD].md
赛道扫描：赛道-[板块名称]-[YYYYMMDD].md
对比分析：对比-[标的A]-vs-[标的B]-[YYYYMMDD].md
组合分析：组合-[组合名称]-[YYYYMMDD].md
```

### 置信度标注

| 级别 | 条件 |
|:--:|------|
| 🟢 | 两个独立来源交叉确认 |
| 🟡 | 单一来源，方向可信 |
| 🔴 | 间接推断 |

### 输出前强制验证

写入文件前逐项检查 14 项清单：数据完整性、估值完整性、数字合理性、分析完整性、文件规范。任一 ❌ 禁止写文件。

## 前置依赖

| 依赖 | 说明 |
|------|------|
| [AnySearch MCP](https://api.anysearch.com/mcp) | 行业全景搜索（必需，否则财务数据覆盖率显著下降） |
| [Compass Scout](https://github.com/liuzhen153/compass-scout) | 上游赛道发现（可选，独立使用 FC 也完全可用） |
| [Compass Trader](https://github.com/liuzhen153/compass-trader) | 下游交易执行（可选，FC 可独立输出估值结论） |
| Claude Code | 运行环境 |

## 安装

```bash
git clone https://github.com/liuzhen153/financial-compass.git ~/.claude/skills/financial-compass
```

## 文件结构

```
financial-compass/
├── SKILL.md                          # 主技能文件（v2.1.0）
├── README.md                         # 本文件
├── CHANGELOG.md                      # 版本更新日志
├── LICENSE                           # MIT License
└── references/                       # 方法论参考
    ├── search-strategy.md            # 搜索策略完整指南
    ├── stock-analysis-engine.md      # 股票分析引擎（14条判据/贝叶斯/反向DCF）
    ├── sector-scanning.md            # 赛道扫描完整模板与搜索方案
    ├── fund-analysis-guide.md        # 基金分析 + 组合风险分析
    ├── verification-checklist.md     # 验证清单与质量保证
    ├── a-share-signals.md            # A股信号解读 + 技术面扩展
    └── convertible-bond.md           # 可转债分析指南
```

## 三者分工

| 职责 | Compass Scout | Financial Compass | Compass Trader |
|------|:---:|:---:|:---:|
| 赛道发现+方向判断 | ✅ | — | — |
| 三大映射/五维验证 | ✅ | — | — |
| 产业链 L0-L6 + 卡点判据 | — | ✅ | — |
| 贝叶斯估值+三情景 | — | ✅ | — |
| 基金穿透+赛道扫描 | — | ✅ | — |
| 可转债分析 | — | ✅ | — |
| 交易参数输出 | — | ✅ | — |
| 模拟盘执行+风控 | — | — | ✅ |
| 策略回测 | — | — | ✅ |
| 绩效追踪+AI反思 | — | — | ✅ |

## 免责声明

本工具是研究辅助工具，不构成投资建议。所有分析输出均为框架性判断，最终决策权在用户手中。投资有风险，入市需谨慎。

*Built by synthesizing the best of 8 open-source financial analysis skills.*

## License

MIT
