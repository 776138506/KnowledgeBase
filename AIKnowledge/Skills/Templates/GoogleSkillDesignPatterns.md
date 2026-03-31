# Google Skill 设计模式总结

> 基于 Google Cloud Tech 提出的 5 种 Skill 设计模式实战指南

## 📖 概述

同一个模型、同样的 SKILL.md 格式规范，为什么有些 Agent 干活干净利落，有些却像没睡醒？

**格式只是皮囊，内容设计才是灵魂。**

现在超过 30 个 Agent 工具（Claude Code、Gemini CLI、Cursor 等）都统一了 SKILL.md 布局，格式问题基本解决了。但规范只告诉你"怎么包装"，没告诉你"里面该怎么设计"。

本文档提炼出了 5 种经过实战验证的设计模式，帮你从"会用格式"进阶到"设计得好"。

## 🎯 五种设计模式速览

| 模式 | 名称 | 核心问题 | 解决方案 | 适用场景 |
|------|------|----------|----------|----------|
| **模式一** | Tool Wrapper（工具包装器） | 团队规范难以落地 | 将最佳实践包装成 Skill，按需加载 | 编码规范、库的最佳实践 |
| **模式二** | Generator（生成器） | 输出结构不一致 | 模板驱动生成，内容与结构分离 | 文档生成、报告编写 |
| **模式三** | Reviewer（审查器） | 检查规则硬编码 | 模块化检查清单，动态加载 | 代码审查、安全审计 |
| **模式四** | Inversion（反转模式） | Agent 爱猜、爱跳步 | Agent 面试用户，先问再做 | 需求收集、项目规划 |
| **模式五** | Pipeline（流水线） | 多步骤任务易出错 | 严格流水线，硬检查点控制 | 文档生成、数据处理 |

## 📊 模式选择决策树

```
只需要让 Agent 懂某个库？
    ↓ 是 → Tool Wrapper
    ↓ 否
需要输出固定格式？
    ↓ 是 → Generator
    ↓ 否
需要检查、评审？
    ↓ 是 → Reviewer
    ↓ 否
需求复杂、容易理解错？
    ↓ 是 → Inversion
    ↓ 否
任务多步骤、不能跳步？
    ↓ 是 → Pipeline
```

---

## 模式一：Tool Wrapper（工具包装器）

### 核心理念

与其把某个库的最佳实践硬编码到系统提示词里，不如包装成一个 Skill，让 Agent 在需要时才加载。

### 优势

- ✅ 系统提示词保持精简
- ✅ 上下文按需加载，省 token
- ✅ 团队的编码规范可以"即插即用"

### 实现要点

1. **references/ 目录**：存放详细的规范文档
2. **SKILL.md**：告诉 Agent"什么时候加载"以及"加载后怎么用"

### 目录结构

```
skills/api-expert/
├── SKILL.md
└── references/
    └── conventions.md
```

### 示例代码

```markdown
# skills/api-expert/SKILL.md
---
name: api-expert
description: FastAPI development best practices and conventions.
  Use when building, reviewing, or debugging FastAPI applications.
---

You are an expert in FastAPI development.

## Core Conventions

Load 'references/conventions.md' for the complete list of best practices.

## When Reviewing Code
1. Load the conventions reference
2. Check code against each convention
3. For violations, cite the rule and suggest the fix

## When Writing Code
1. Load the conventions reference
2. Follow every convention exactly
3. Add type annotations to all function signatures
```

### 最佳实践

- 💡 这是最简单也最实用的模式
- 💡 如果你团队有内部编码规范，用 Tool Wrapper 分发给每个开发者
- 💡 比写一万个 Notion 文档都有用——因为 Agent 真的会去读、去执行

---

## 模式二：Generator（生成器）

### 核心理念

解决"每次输出结构都不一样"的问题。把"内容"和"结构"分离。模板管结构，Agent 管内容填充。

### 优势

- ✅ 输出结构一致
- ✅ 复用性强，换模板就能产出不同类型文档
- ✅ Agent 按步骤执行，不会遗漏

### 实现要点

1. **assets/ 目录**：放输出模板
2. **references/ 目录**：放风格指南
3. **SKILL.md**：充当"项目经理"，指挥 Agent 按步骤填空

### 目录结构

```
skills/report-generator/
├── SKILL.md
├── assets/
│   └── report-template.md
└── references/
    └── style-guide.md
```

### 示例代码

```markdown
# skills/report-generator/SKILL.md
---
name: report-generator
description: Generates structured technical reports in Markdown.
---

You are a technical report generator. Follow these steps exactly:

Step 1: Load 'references/style-guide.md' for tone and formatting rules.

Step 2: Load 'assets/report-template.md' for the required structure.

Step 3: Ask the user for missing information:
- Topic or subject
- Key findings or data points
- Target audience

Step 4: Fill the template following the style guide.

Step 5: Return the completed report.
```

### 设计亮点

- 换个模板就能产出完全不同类型的文档，复用性极强
- Agent 按步骤执行，不会跳过关键环节

---

## 模式三：Reviewer（审查器）

### 核心理念

把"查什么"和"怎么查"分开。与其在系统提示词里写一长串检查项，不如把这些规则放到 references/review-checklist.md 里，让 Agent 动态加载。

### 优势

- ✅ 规则模块化，易于维护
- ✅ 基础设施不变，换清单就能变工具
- ✅ 审查过程标准化

### 实现要点

1. **references/review-checklist.md**：详细的检查清单
2. **SKILL.md**：定义审查流程和输出格式

### 目录结构

```
skills/code-reviewer/
├── SKILL.md
└── references/
    └── review-checklist.md
```

### 示例代码

```markdown
# skills/code-reviewer/SKILL.md
---
name: code-reviewer
description: Reviews Python code for quality, style, and bugs.
---

You are a Python code reviewer. Follow this protocol exactly:

Step 1: Load 'references/review-checklist.md' for review criteria.

Step 2: Read the user's code carefully.

Step 3: Apply each rule. For every violation:
- Note the line number
- Classify severity: error / warning / info
- Explain WHY it's a problem
- Suggest a specific fix

Step 4: Produce structured output:
- **Summary**: What the code does, overall assessment
- **Findings**: Grouped by severity
- **Score**: Rate 1-10 with justification
- **Top 3 Recommendations**
```

### 设计亮点

- 把 Python 风格检查清单换成 OWASP 安全清单，同一个 Skill 瞬间变成安全审计工具
- 基础设施完全不变，只是换了个参考文档

---

## 模式四：Inversion（反转模式）

### 核心理念

把"用户驱动 Agent"变成"Agent 面试用户"。Agent 天生爱"猜"，但在复杂场景下，猜错了比不回答更可怕。

### 优势

- ✅ 避免理解偏差
- ✅ 强制 Agent 慢下来，把需求搞清楚
- ✅ 像心理咨询——先倾听，后诊断

### 关键设计

1. **明确的"门禁"指令**：比如"DO NOT start building until all phases are complete"
2. **分阶段提问**：每个阶段必须等用户回答完才能进入下一阶段
3. **最后才输出结果**

### 目录结构

```
skills/project-planner/
├── SKILL.md
└── assets/
    └── plan-template.md
```

### 示例代码

```markdown
# skills/project-planner/SKILL.md
---
name: project-planner
description: Plans software projects by gathering requirements through
  structured questions before producing a plan.
---

You are conducting a requirements interview.
DO NOT start building until all phases are complete.

## Phase 1 — Problem Discovery (ask one question at a time)

Ask in order. Do not skip any.
- Q1: "What problem does this project solve for its users?"
- Q2: "Who are the primary users? What is their technical level?"
- Q3: "What is the expected scale?"

## Phase 2 — Technical Constraints (only after Phase 1 is complete)

- Q4: "What deployment environment will you use?"
- Q5: "Do you have technology stack preferences?"
- Q6: "What are the non-negotiable requirements?"

## Phase 3 — Synthesis (only after all questions answered)

1. Load 'assets/plan-template.md'
2. Fill in every section using gathered requirements
3. Present the plan
4. Ask: "Does this capture your requirements?"
5. Iterate until user confirms
```

### 设计亮点

- 这个模式有点像心理咨询——先倾听，后诊断
- 很多失败的 Agent 项目，问题就出在"答得太快"
- Inversion 强制 Agent 慢下来，把需求搞清楚再动手

---

## 模式五：Pipeline（流水线）

### 核心理念

有些任务，一步都不能少。比如生成 API 文档，必须先解析代码、再生成文档字符串、再组装、再检查。跳过任何一步，结果都可能出问题。

### 优势

- ✅ 流程完整，不会跳步
- ✅ 质量可控，有检查点
- ✅ 每步可验证

### 关键设计

1. **执行顺序**：Execute each step in order. Do NOT skip steps.
2. **用户确认**：关键步骤后设置"门禁"，必须等用户确认
3. **质量检查**：最后一步进行质量验证

### 目录结构

```
skills/doc-pipeline/
├── SKILL.md
├── assets/
│   └── api-doc-template.md
└── references/
    ├── docstring-style.md
    └── quality-checklist.md
```

### 示例代码

```markdown
# skills/doc-pipeline/SKILL.md
---
name: doc-pipeline
description: Generates API documentation from Python source code.
---

You are running a documentation pipeline.
Execute each step in order. Do NOT skip steps.

## Step 1 — Parse & Inventory

Analyze the code to extract all public classes and functions.
Ask: "Is this the complete public API you want documented?"

## Step 2 — Generate Docstrings

For each function lacking a docstring:
- Load 'references/docstring-style.md' for format
- Generate docstrings following the style guide
- Present each for user approval

**Do NOT proceed to Step 3 until user confirms.**

## Step 3 — Assemble Documentation

Load 'assets/api-doc-template.md' for output structure.
Compile all symbols into a single API reference document.

## Step 4 — Quality Check

Review against 'references/quality-checklist.md':
- Every public symbol documented
- Every parameter has type and description
- At least one usage example per function

Report results. Fix issues before final delivery.
```

### 设计亮点

- 注意 Step 2 那句"Do NOT proceed to Step 3 until user confirms"——这就是钻石门禁
- Agent 不能自己跳过，必须等人工确认
- 这对保证质量至关重要

---

## 🎨 模式组合使用

这五种模式不是互斥的，而是可以组合使用。

### 组合示例

1. **Pipeline + Reviewer**：在 Pipeline 最后加一个 Reviewer 步骤，自己检查自己的工作
2. **Generator + Inversion**：先用 Inversion 模式收集必要信息，再填充模板
3. **Tool Wrapper + Pipeline**：在 Pipeline 的某些步骤加载 Tool Wrapper 获取专业知识

### ADK 的优势

ADK 的 SkillToolset 和渐进式上下文加载机制，让 Agent 只在需要的时候才加载对应的 Skill。这意味着组合使用不会炸 token——该用哪个就用哪个。

---

## 💡 设计感悟

### 第一，格式已死，设计永生

SKILL.md 的 YAML、目录结构，这些已经标准化了，再卷也卷不出花。真正的竞争力在于：**你能不能把业务逻辑抽象成合适的设计模式**。

### 第二，每种模式都在对抗 Agent 的"本能"

Agent 天生爱猜、爱跳步、爱一次性输出。这五种模式，本质上都是"约束"——约束 Agent 按规矩办事。

**好的设计，就是好的约束。**

### 第三，组合才是王道

单一模式能解决的问题有限。真正复杂的生产场景，往往是 Pipeline + Reviewer + Tool Wrapper 的组合拳。

把 Atomic Skill 设计好，让它们能灵活编排，这才是架构师的价值。

---

## 📝 总结

| 设计原则 | 说明 |
|---------|------|
| **按需加载** | 不要把所有规则硬编码到系统提示词 |
| **结构分离** | 模板管结构，Agent 管内容 |
| **模块化** | 把"查什么"和"怎么查"分开 |
| **先问再做** | 复杂场景强制 Agent 慢下来 |
| **流程控制** | 多步骤任务设置硬检查点 |
| **组合使用** | 灵活组合多种模式解决复杂问题 |

---

## 🔗 参考资料

- [5 Agent Skill design patterns every ADK developer should know - Google Cloud Tech](https://cloud.google.com/blog/products/ai-machine-learning/agent-skill-design-patterns)
- [Agent Development Kit (ADK) - Google](https://cloud.google.com/vertex-ai/docs/adk/introduction)

---

**版本**: 1.0.0  
**创建日期**: 2026-03-31  
**基于**: Google Cloud Tech - 5 Agent Skill design patterns
