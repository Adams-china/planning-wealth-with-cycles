# Planning Wealth with Cycles

> A cycle-aware, valuation-conscious and risk-controlled wealth-planning Skill for AI agents.  
> 面向 AI Agent 的周期理财 Skill：用周期判断方向，用估值判断赔率，用仓位控制风险。

![Skill icon](assets/icon.svg)

[中文说明](#中文说明) · [English](#english) · [Install](#安装--installation) · [Examples](#调用示例--usage-examples)

---

## 中文说明

### 这是什么？

`planning-wealth-with-cycles` 是一套供 AI Agent 调用的综合理财分析 Skill。它受到周金涛《人生财富靠康波：涛动周期论》的启发，但**不会把康波周期当作精确预测工具**。

它把长期周期放在一个更完整的决策系统中：

1. 家庭财务安全；
2. 宏观环境与经济周期；
3. 资产估值；
4. 资产或公司质量；
5. 仓位与执行纪律。

核心原则：

> **周期决定风向，估值决定赔率，仓位决定生死。**  
> Use cycles as a map, never as a clock.

### 它能帮助你做什么？

适用于以下问题：

- 家庭资产配置；
- A股、美股和指数基金分析；
- 黄金、债券、现金和房地产配置；
- 单只股票建仓与仓位控制；
- 大宗商品和宏观周期分析；
- 持仓诊断与再平衡；
- 给出明确的“买、等待、持有、减仓或再平衡”结论。

### 它不会做什么？

- 不保证投资收益；
- 不用康波推算某年必然见顶或见底；
- 不建议借钱、加杠杆或挪用应急金投资；
- 不用宏观叙事替代估值、基本面和资产负债表；
- 不把历史预测当作当前市场事实；
- 不在缺乏关键信息时伪造确定性。

### 为什么不能只靠康波投资？

康波理论对技术革命、长期价格波动、资源供给滞后和时代财富机会很有启发，但完整长周期的历史样本非常少，阶段边界也存在争议。

因此，本 Skill 只把康波作为宏观地图。对于单只股票，宏观和周期因素最多只能占投资论证的20%；其余判断必须来自公司质量、盈利、估值和仓位纪律。

---

## 安装 / Installation

### 方法一：通用 Agent Skills 目录

```bash
git clone https://github.com/Adams-china/planning-wealth-with-cycles.git \
  ~/.agents/skills/planning-wealth-with-cycles
```

### 方法二：Codex

```bash
git clone https://github.com/Adams-china/planning-wealth-with-cycles.git \
  ~/.codex/skills/planning-wealth-with-cycles
```

### 方法三：Claude Code

如果你的 Claude Code 环境使用项目级 Skills：

```bash
mkdir -p .claude/skills
git clone https://github.com/Adams-china/planning-wealth-with-cycles.git \
  .claude/skills/planning-wealth-with-cycles
```

### 方法四：不支持自动发现的 Agent

让 Agent 先读取仓库中的 `SKILL.md`，并在回答投资问题前遵循其中的工作流。需要判断宏观环境或比较资产时，再读取：

- [Cycle framework](references/cycle-framework.md)
- [Decision contract](references/decision-contract.md)

> 不同 Agent 产品的目录和调用语法可能不同；请以该产品的 Skills 文档为准。

---

## 调用示例 / Usage Examples

### 家庭资产配置

```text
使用 @planning-wealth-with-cycles 分析我的家庭资产配置。

可投资金额：100,000元
投资期限：5年以上
应急金：已准备12个月生活费
最大可接受回撤：15%
当前持仓：现金70%，A股30%

请给出明确的配置金额、目标比例、分批计划、反方证据和再平衡条件。
```

### 1万元新手方案

```text
使用 @planning-wealth-with-cycles 帮我配置1万元，
覆盖A股、美股、黄金、债券和现金。
我是投资新手，请给出具体金额，不要只给百分比。
```

### 单只股票

```text
使用 @planning-wealth-with-cycles 分析兴业银行。
我可以投入1万元，请明确告诉我：买、不买还是等待，
以及现在买多少、最多持有多少、怎样分批。
```

### 黄金是否追涨

```text
使用 @planning-wealth-with-cycles 判断黄金是否值得买。
我目前没有黄金仓位，计划投入5000元。
请区分组合对冲和追涨，并给出分批方案及停止买入条件。
```

### English example

```text
Use @planning-wealth-with-cycles to review my portfolio.

Budget: USD 20,000
Horizon: 7 years
Emergency fund: 9 months of expenses
Maximum tolerable drawdown: 18%
Current allocation: 60% cash, 40% US equities

Give one explicit action, exact amounts, maximum weights,
a tranche plan, counterarguments, invalidation conditions,
data timestamps and confidence scores.
```

---

## 输出内容 / Output Contract

每次完整分析应依次提供：

1. **明确结论**：买、不买、等待、持有、减仓或再平衡；
2. **金额与仓位**：现在投入多少、最大目标比例；
3. **执行计划**：分几批、在什么条件下执行；
4. **五层证据**：家庭安全、周期、估值、质量、执行适配；
5. **三种情景**：基准、乐观、悲观；
6. **反方证据**：结论最可能错在哪里；
7. **失效条件**：什么数据或事件会改变结论；
8. **置信度**：分项与整体评分；
9. **数据时点**：明确所依据行情和资料的日期。

若整体置信度低于0.80，Skill应降低初始仓位、指出最薄弱环节，并说明需要补充什么证据。

---

## 文件结构 / Repository Structure

```text
planning-wealth-with-cycles/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── assets/
│   └── icon.svg
└── references/
    ├── cycle-framework.md
    └── decision-contract.md
```

- **SKILL.md**：AI Agent必须遵循的核心工作流和风险护栏。
- **cycle-framework.md**：周期层级、经济环境和资产倾向。
- **decision-contract.md**：最终建议的固定输出结构。
- **openai.yaml**：Skill显示信息与默认调用提示。
- **icon.svg**：Skill图标。

---

## English

### What is this?

`planning-wealth-with-cycles` is an Agent Skill for household allocation, cross-asset comparison, position sizing and investment decision support. It is inspired by Zhou Jintao's work on Kondratiev waves, but it does not treat long cycles as a deterministic market clock.

The Skill applies five gates in order:

1. household financial safety;
2. macro regime and cycles;
3. valuation;
4. asset or company quality;
5. position sizing and execution.

### Supported decisions

- household portfolio allocation;
- A-shares, US equities and index funds;
- gold, bonds, cash, property and commodities;
- single-stock entry plans;
- portfolio diagnosis and rebalancing;
- explicit buy, wait, hold, reduce or rebalance decisions.

### Safety design

The Skill forbids leverage for beginners, protects emergency funds, requires current-data verification, limits cycle reasoning in single-stock analysis, and forces the Agent to provide counterarguments, invalidation conditions and confidence scores.

---

## Important Disclaimer / 重要声明

This project is for education and decision support only. It does not provide guaranteed returns, personalized regulated financial advice, tax advice or legal advice.

本项目仅用于投资教育和辅助决策，不承诺收益，也不能替代持牌金融顾问、税务顾问或法律专业人士。任何资产都可能亏损。实际投资前，请结合你的债务、应急金、收入稳定性、投资期限和风险承受能力独立判断。

## Source and attribution / 理论来源

The cycle component is inspired by Zhou Jintao's *Life Wealth Depends on Kondratiev Waves: Theory of Cyclical Fluctuations*（周金涛《人生财富靠康波：涛动周期论》）. This repository contains an original operational framework and does not reproduce the book's full text.

## License

No explicit open-source license has been selected yet. The repository is publicly readable, but reuse and redistribution rights remain reserved until the owner adds a license.
