---
name: 技能遗忘与清理
identifier: SkillForgetting
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 技能维护
  - 技能清理
  - 知识管理
  - 元技能
  - 技能进化
---

# 技能遗忘与清理

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能遗忘与清理 |
| **英文标识名** | `SkillForgetting` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **技能遗忘** 与 **智能清理** 的能力，使其能够：
1. 根据使用频率自动识别低价值技能（使用频率过低则建议废弃）
2. 根据遗忘时间自动识别过时技能（长期未使用则建议遗忘）
3. 确保遗忘后相关联的技能不会失效（关联保护机制）
4. 支持精细化的 CRUD 操作（行级修改，而非简单的文件创建与删除）
5. 维护技能库的精简性和高效性

## 🎯 适用场景

- ✅ **低频技能清理**：识别并清理使用频率极低的技能
- ✅ **过时技能遗忘**：遗忘长期未使用的技能
- ✅ **技能关联保护**：确保删除技能后相关技能仍能正常工作
- ✅ **技能精细化维护**：对技能内容进行行级修改和更新
- ✅ **技能库优化**：保持技能库精简，避免技能膨胀
- ✅ **技能生命周期管理**：管理技能从创建到遗忘的全生命周期

### 不适用场景
- ❌ 高频核心技能的删除
- ❌ 未经用户确认的自动删除
- ❌ 破坏技能关联的删除操作
- ❌ 简单粗暴的文件删除（不使用行级修改）

## 🏗️ 技能架构

### 架构图

```
SkillForgetting (技能遗忘核心)
├── UsageTracker (使用追踪器)
│   ├── FrequencyAnalyzer (频率分析器)
│   ├── RecencyCalculator (新鲜度计算器)
│   └── ValueEstimator (价值评估器)
├── RelationshipProtector (关联保护器)
│   ├── DependencyScanner (依赖扫描器)
│   ├── ImpactAnalyzer (影响分析器)
│   └── MigrationPlanner (迁移规划器)
├── ForgettingStrategy (遗忘策略)
│   ├── ThresholdEvaluator (阈值评估器)
│   ├── PriorityCalculator (优先级计算器)
│   └── DecisionEngine (决策引擎)
└── CRUDExecutor (CRUD 执行器)
    ├── LineLevelEditor (行级编辑器)
    ├── ContentUpdater (内容更新器)
    └── SafeDeleter (安全删除器)
```

### 组件说明

| 组件名称 | 角色 | 职责 | 工具 |
|---------|------|------|------|
| UsageTracker | 使用追踪器 | 追踪技能使用频率、时间、价值 | 日志分析、统计分析 |
| RelationshipProtector | 关联保护器 | 分析技能关联、评估影响、规划迁移 | 图分析、依赖分析 |
| ForgettingStrategy | 遗忘策略 | 制定遗忘策略、计算优先级、生成决策 | 决策树、规则引擎 |
| CRUDExecutor | CRUD 执行器 | 执行行级修改、内容更新、安全删除 | 文件操作、文本编辑 |

## 🔄 工作流程

### 主工作流程

```
技能扫描 → 使用分析 → 关联检查 → 遗忘决策 → 用户确认 → 迁移准备 → 执行遗忘 → 关联验证
    ↓          ↓          ↓          ↓          ↓          ↓          ↓          ↓
[全量技能] [频率/时间] [依赖分析] [废弃/遗忘] [用户审批] [内容迁移] [行级修改] [验证通过]
```

### 详细步骤

#### 步骤 1：技能扫描与使用分析

**目标**: 全面扫描技能库，分析每个技能的使用情况

**输入**: 
- 技能目录路径
- 使用日志记录

**处理过程**:
1. **扫描技能库**：
   - 遍历所有技能文件夹
   - 读取 SKILL.md 文件的元数据
   - 提取 identifier、version、updated 等信息

2. **分析使用频率**：
   - 统计每个技能的使用次数
   - 计算单位时间内的使用频率（次/周）
   - 识别使用趋势（上升/下降/稳定）

3. **计算新鲜度**：
   - 计算最后使用时间距今天数
   - 计算最后更新时间距今天数
   - 评估技能活跃程度

4. **评估技能价值**：
   - 综合使用频率、新鲜度、关联度
   - 计算技能价值评分（0-100）
   - 标记低价值技能（评分<30）

**输出**: 
- 技能使用统计报告
- 技能价值评分列表
- 低价值技能候选列表

**质量标准**:
- [ ] 使用统计准确率 100%
- [ ] 价值评分客观合理
- [ ] 候选列表完整

**示例**:
```
技能使用分析报告
==================
技能总数：25

高频使用技能（>5 次/周）：8
- CodeReviewer: 12 次/周
- DocumentationEngineer: 10 次/周

中频使用技能（1-5 次/周）：10
- QualityValidator: 3 次/周

低频使用技能（<1 次/周）：7
- OldComponent: 0.2 次/周 ⚠️
- LegacyAPI: 0.1 次/周 ⚠️

长期未使用技能（>90 天）：3
- DeprecatedTool: 120 天未使用 ⚠️
- OldWorkflow: 95 天未使用 ⚠️
```

#### 步骤 2：关联关系检查

**目标**: 分析技能间的依赖关系，确保遗忘不会影响其他技能

**输入**: 技能清单、技能关系图

**处理过程**:
1. **扫描依赖关系**：
   - 读取每个技能的"前置技能"和"后续技能"章节
   - 分析技能间的工具共享关系
   - 识别技能组合关系

2. **构建依赖图**：
   - 创建技能依赖图（DAG）
   - 标记每个节点的入度和出度
   - 识别关键节点（被多个技能依赖）

3. **影响分析**：
   - 对于每个候选遗忘技能，分析删除后的影响
   - 计算影响范围（影响的技能数量）
   - 评估影响程度（轻微/中等/严重）

4. **迁移规划**：
   - 对于有依赖的技能，规划迁移方案
   - 识别需要更新的相关技能
   - 生成内容迁移计划

**输出**: 
- 技能依赖关系图
- 影响分析报告
- 迁移方案列表

**质量标准**:
- [ ] 依赖关系识别准确率 100%
- [ ] 影响评估客观准确
- [ ] 迁移方案可行

**示例**:
```
关联影响分析
============
候选遗忘技能：OldComponent

依赖分析:
- 被依赖：2 个技能
  * ComponentGenerator (引用了 OldComponent 作为示例)
  * LegacyIntegration (依赖 OldComponent 的接口)
- 依赖其他技能：0 个

影响评估:
- 影响程度：中等
- 影响范围：2 个技能

迁移方案:
1. 更新 ComponentGenerator 的示例代码
2. 将 LegacyIntegration 的依赖迁移到新组件
3. 在 OldComponent 中添加废弃说明和迁移指引
```

#### 步骤 3：遗忘策略与决策

**目标**: 根据使用分析和关联检查结果，生成遗忘决策

**输入**: 使用统计、关联分析报告

**处理过程**:
1. **阈值评估**：
   - 使用频率阈值：< 0.5 次/周（可调整）
   - 遗忘时间阈值：> 90 天未使用（可调整）
   - 价值评分阈值：< 30 分（可调整）

2. **优先级计算**：
   - 综合多个维度计算遗忘优先级
   - 优先级 = f(使用频率，新鲜度，价值评分，影响程度)
   - 排序候选列表

3. **决策生成**：
   - 生成三种决策类型：
     * **保留**：高频使用或关键技能
     * **观察**：低频但有价值，继续观察
     * **废弃**：长期未使用且无价值
     * **遗忘**：已废弃且无关联影响

4. **生成建议**：
   - 为每个决策生成详细说明
   - 提供预期收益
   - 给出实施计划

**输出**: 
- 遗忘决策列表
- 优先级排序
- 详细建议报告

**质量标准**:
- [ ] 决策合理性强
- [ ] 优先级排序客观
- [ ] 建议具体可操作

**示例**:
```
遗忘决策报告
============

### 建议遗忘（优先级：高）

**技能 1**: DeprecatedTool
- **最后使用**: 120 天前
- **使用频率**: 0 次/周
- **价值评分**: 15/100
- **关联影响**: 无依赖
- **建议**: 直接遗忘（删除文件）
- **预期收益**: 减少技能库复杂度，提高检索效率

**技能 2**: OldWorkflow
- **最后使用**: 95 天前
- **使用频率**: 0.1 次/周
- **价值评分**: 22/100
- **关联影响**: 轻微（1 个技能引用）
- **建议**: 迁移引用后遗忘
- **预期收益**: 精简技能库

### 建议废弃（优先级：中）

**技能 3**: LegacyAPI
- **最后使用**: 60 天前
- **使用频率**: 0.2 次/周
- **价值评分**: 28/100
- **关联影响**: 中等（2 个技能依赖）
- **建议**: 标记为废弃，添加迁移指引
- **预期收益**: 提醒用户迁移，逐步淘汰

### 建议观察（优先级：低）

**技能 4**: NicheUtility
- **最后使用**: 45 天前
- **使用频率**: 0.3 次/周
- **价值评分**: 35/100
- **关联影响**: 轻微
- **建议**: 继续观察 30 天
- **原因**: 虽然低频但有独特价值

### 建议保留

**技能 5**: CodeReviewer
- **最后使用**: 1 天前
- **使用频率**: 12 次/周
- **价值评分**: 95/100
- **建议**: 保留并持续优化
```

#### 步骤 4：用户确认

**目标**: 获得用户对遗忘决策的审批

**输入**: 遗忘决策列表

**处理过程**:
1. **展示决策报告**：
   - 按优先级排序展示
   - 提供详细说明和预期收益
   - 展示关联影响和迁移方案

2. **等待用户确认**：
   - 用户可以批准、拒绝或修改决策
   - 记录用户决策和反馈

3. **调整决策**：
   - 根据用户反馈调整决策
   - 重新评估被拒绝的决策

**输出**: 
- 用户确认的决策列表
- 用户修改的意见
- 被拒绝的决策及原因

**质量标准**:
- [ ] 决策展示清晰
- [ ] 用户决策记录完整
- [ ] 调整及时准确

#### 步骤 5：迁移准备与内容更新

**目标**: 在遗忘前完成必要的迁移和内容更新

**输入**: 用户确认的决策

**处理过程**:
1. **内容迁移**：
   - 识别需要迁移的内容
   - 将重要内容迁移到其他技能
   - 更新引用该技能的其他技能

2. **行级修改**：
   - 对于需要更新而非删除的技能
   - 精确定位到需要修改的行
   - 执行行级替换、插入或删除

3. **添加废弃说明**：
   - 对于建议废弃的技能
   - 在文件顶部添加废弃标记
   - 添加迁移指引和替代方案

**输出**: 
- 迁移完成报告
- 内容更新记录
- 废弃技能标记

**质量标准**:
- [ ] 迁移完整
- [ ] 行级修改准确
- [ ] 废弃说明清晰

**示例**:
```
迁移与更新执行
==============

### 内容迁移

**从**: OldComponent
**迁移到**: ComponentGenerator

迁移内容:
1. ✅ 关键接口定义已迁移
2. ✅ 使用示例已更新
3. ✅ 依赖关系已重新映射

### 行级修改

**文件**: ComponentGenerator/SKILL.md
**修改位置**: 第 125-130 行
**修改内容**:
- 旧内容：参考 OldComponent 的实现
- 新内容：参考 NewComponent 的实现（已迁移）

**文件**: LegacyIntegration/SKILL.md
**修改位置**: 第 45 行
**修改内容**:
- 旧内容：依赖：OldComponent
- 新内容：依赖：NewComponent (迁移自 OldComponent)

### 废弃标记

**文件**: OldComponent/SKILL.md
**添加内容** (文件顶部):
```markdown
> ⚠️ **已废弃** (2026-03-31)
> 
> 此技能已废弃，请使用 [NewComponent](../NewComponent/SKILL.md) 替代。
> 
> **迁移指引**: [迁移文档](链接)
```
```

#### 步骤 6：执行遗忘与验证

**目标**: 执行遗忘操作并验证关联技能未受影响

**输入**: 迁移完成的技能库

**处理过程**:
1. **执行遗忘**：
   - 对于确认遗忘的技能
   - 移动到归档目录或直接删除
   - 更新技能注册中心

2. **关联验证**：
   - 检查所有相关技能的引用是否有效
   - 验证依赖关系是否已正确迁移
   - 确保没有断链的引用

3. **生成报告**：
   - 记录遗忘的技能清单
   - 统计收益（技能库大小减少、检索效率提升等）
   - 提供后续建议

**输出**: 
- 遗忘执行报告
- 验证结果
- 技能库更新统计

**质量标准**:
- [ ] 遗忘执行准确
- [ ] 关联验证通过
- [ ] 报告完整详细

**示例**:
```
遗忘执行完成
============

### 已遗忘技能

1. **DeprecatedTool**
   - 操作：已删除文件
   - 归档位置：Archived/DeprecatedTool/
   - 影响：无

2. **OldWorkflow**
   - 操作：已删除文件
   - 归档位置：Archived/OldWorkflow/
   - 影响：2 个技能已更新引用

### 验证结果

✅ 所有关联验证通过
✅ 无断链引用
✅ 依赖关系完整

### 技能库统计

- 遗忘前技能数：25
- 遗忘后技能数：23
- 减少：2 个 (8%)
- 归档技能：2 个

### 预期收益

- 📉 技能库复杂度降低
- 🔍 检索效率提升约 5%
- 💾 存储空间节省：15KB
- ⚡ 技能加载速度提升
```

## 👥 遗忘策略引擎

### 使用频率评估规则

```python
def evaluate_usage_frequency(skill_stats):
    """
    评估技能使用频率并给出建议
    """
    frequency_per_week = skill_stats.usage_count / (skill_stats.days_tracked / 7)
    
    if frequency_per_week >= 5:
        return "high", "保留", "高频使用技能"
    elif frequency_per_week >= 1:
        return "medium", "保留", "中频使用技能"
    elif frequency_per_week >= 0.5:
        return "low", "观察", "低频使用，继续观察"
    else:
        return "very_low", "建议废弃", "使用频率过低"
```

### 遗忘时间评估规则

```python
def evaluate_recency(skill_stats):
    """
    评估技能新鲜度并给出建议
    """
    days_since_last_use = skill_stats.last_used_days_ago
    
    if days_since_last_use <= 7:
        return "recent", "保留", "最近使用过"
    elif days_since_last_use <= 30:
        return "moderate", "保留", "使用正常"
    elif days_since_last_use <= 60:
        return "stale", "观察", "较长时间未使用"
    elif days_since_last_use <= 90:
        return "old", "建议废弃", "长期未使用"
    else:
        return "very_old", "建议遗忘", "过时技能"
```

### 关联影响评估规则

```python
def evaluate_impact(skill, dependency_graph):
    """
    评估技能遗忘的影响程度
    """
    # 获取依赖该技能的技能列表
    dependent_skills = dependency_graph.get_dependents(skill.identifier)
    
    impact_count = len(dependent_skills)
    
    if impact_count == 0:
        return "none", "无影响", "可以直接遗忘"
    elif impact_count <= 1:
        return "minor", "轻微影响", "需更新 1 个相关技能"
    elif impact_count <= 3:
        return "moderate", "中等影响", "需更新多个相关技能"
    else:
        return "severe", "严重影响", "关键技能，谨慎遗忘"
```

### 综合决策规则

```python
def make_forgetting_decision(skill_analysis):
    """
    综合多个维度做出遗忘决策
    """
    usage_level, usage_suggestion, usage_reason = evaluate_usage_frequency(skill_analysis)
    recency_level, recency_suggestion, recency_reason = evaluate_recency(skill_analysis)
    impact_level, impact_suggestion, impact_reason = evaluate_impact(skill_analysis)
    
    # 计算综合评分
    score = calculate_composite_score(skill_analysis)
    
    # 决策逻辑
    if impact_level == "severe":
        return "保留", "关键技能，即使低频也需保留"
    
    if usage_level == "very_low" and recency_level == "very_old":
        if impact_level == "none":
            return "遗忘", "低频、过时且无关联影响"
        else:
            return "废弃", "低频过时，但需先处理关联"
    
    if score < 30:
        return "建议废弃", f"价值评分过低 ({score}/100)"
    elif score < 50:
        return "观察", f"价值评分中等 ({score}/100)，继续观察"
    else:
        return "保留", f"价值评分良好 ({score}/100)"
```

## ⚙️ 执行模式

### Mode A: 审查模式（Audit Mode）

- **描述**: 仅扫描和分析，不执行遗忘
- **包含阶段**: 技能扫描 → 使用分析 → 关联检查 → 生成报告
- **使用场景**: 定期体检、了解技能库状态
- **预计耗时**: 短（5-10 分钟）
- **输出**: 技能库健康报告和遗忘建议

### Mode B: 建议模式（Suggestion Mode）

- **描述**: 分析并生成详细的遗忘建议
- **包含阶段**: 技能扫描 → 使用分析 → 关联检查 → 遗忘决策 → 生成建议
- **使用场景**: 主动优化技能库、寻找清理机会
- **预计耗时**: 中等（10-20 分钟）
- **输出**: 遗忘建议列表（按优先级排序）

### Mode C: 执行模式（Execution Mode）

- **描述**: 执行用户确认的遗忘操作
- **包含阶段**: 技能扫描 → 使用分析 → 关联检查 → 遗忘决策 → 用户确认 → 迁移准备 → 执行遗忘 → 验证
- **使用场景**: 实际清理技能库
- **预计耗时**: 长（取决于遗忘范围）
- **输出**: 遗忘执行报告和更新后的技能库

### Mode D: 行级编辑模式（Line-Level Edit Mode）

- **描述**: 专注于技能的精细化 CRUD 操作
- **包含阶段**: 内容分析 → 定位修改点 → 行级修改 → 验证
- **使用场景**: 技能内容更新、示例代码替换、引用更新
- **预计耗时**: 中等（取决于修改复杂度）
- **输出**: 修改记录和更新后的技能文件

## 🚀 快速开始

### 前置条件

- [ ] 技能库中至少有 3 个技能
- [ ] 有技能使用日志记录（可选，但推荐）
- [ ] 有写入权限

### 基本用法

```bash
# 模式 1：审查模式（定期体检）
skill-forgetting audit

# 模式 2：建议模式（寻找清理机会）
skill-forgetting suggest

# 模式 3：执行模式（实际清理）
skill-forgetting execute --auto-approve=false

# 模式 4：行级编辑模式
skill-forgetting edit --file="SkillName/SKILL.md" --line=125 --operation=replace
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `--mode` | string | 否 | "suggest" | 执行模式（audit/suggest/execute/edit） |
| `--auto-approve` | boolean | 否 | false | 是否自动批准建议（仅 execute 模式） |
| `--frequency-threshold` | number | 否 | 0.5 | 使用频率阈值（次/周） |
| `--recency-threshold` | number | 否 | 90 | 遗忘时间阈值（天） |
| `--value-threshold` | number | 否 | 30 | 价值评分阈值（0-100） |
| `--file` | string | 否 | - | 目标文件路径（仅 edit 模式） |
| `--line` | number | 否 | - | 目标行号（仅 edit 模式） |
| `--operation` | string | 否 | - | 操作类型（replace/insert/delete）（仅 edit 模式） |

## 📋 输入输出规范

### 输入格式

```json
{
  "mode": "类型：string，说明：执行模式",
  "skills_path": "类型：string，说明：技能库路径",
  "config": {
    "type": "object",
    "description": "配置选项",
    "properties": {
      "frequency_threshold": "类型：number，说明：使用频率阈值",
      "recency_threshold": "类型：number，说明：遗忘时间阈值",
      "value_threshold": "类型：number，说明：价值评分阈值",
      "auto_approve": "类型：boolean，说明：是否自动批准"
    }
  },
  "edit_params": {
    "type": "object",
    "description": "行级编辑参数（仅 edit 模式）",
    "properties": {
      "file": "类型：string，说明：文件路径",
      "line": "类型：number，说明：行号",
      "operation": "类型：string，说明：操作类型",
      "content": "类型：string，说明：新内容（replace/insert 操作）"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "audit_report": {
    "total_skills": "技能总数",
    "high_usage": "高频使用数",
    "low_usage": "低频使用数",
    "stale_skills": "过时技能数"
  },
  "suggestions": [
    {
      "type": "forget|archive|observe|retain",
      "priority": "high|medium|low",
      "skill_identifier": "技能标识名",
      "reason": "建议原因",
      "impact": "影响评估",
      "migration_plan": "迁移方案"
    }
  ],
  "execution_result": {
    "forgotten_skills": ["已遗忘技能列表"],
    "updated_skills": ["已更新技能列表"],
    "verification_passed": "验证是否通过"
  },
  "edit_result": {
    "file": "修改的文件",
    "lines_modified": "修改的行数",
    "operations": ["执行的操作列表"]
  }
}
```

## ✅ 质量门禁

### 检查清单

#### 完整性检查
- [ ] 技能库扫描覆盖率 100%
- [ ] 使用分析覆盖所有技能
- [ ] 关联检查完整
- [ ] 遗忘决策全面

#### 准确性检查
- [ ] 使用统计准确率 100%
- [ ] 关联识别准确率>95%
- [ ] 决策合理性评分>0.8
- [ ] 行级修改准确率 100%

#### 安全性检查
- [ ] 遗忘前关联验证通过
- [ ] 迁移方案可行
- [ ] 用户确认记录完整
- [ ] 可回滚（有备份）

### 验收标准

- [ ] 能正确识别低频技能（<0.5 次/周）
- [ ] 能正确识别过时技能（>90 天未使用）
- [ ] 遗忘决策合理且具体
- [ ] 关联保护机制有效
- [ ] 行级修改准确无误
- [ ] 遗忘操作不破坏现有功能

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_NO_LOGS | 无使用日志记录 | 未启用日志或日志丢失 | 使用默认值或手动标记 |
| ERR_DEPENDENCY_CYCLE | 检测到循环依赖 | 技能间形成循环引用 | 手动打破循环后再遗忘 |
| ERR_MIGRATION_FAILED | 迁移失败 | 目标位置不可写或内容冲突 | 检查权限和冲突原因 |
| ERR_LINE_NOT_FOUND | 行号不存在 | 文件行数不足或行号错误 | 检查文件内容和行号 |
| ERR_EDIT_CONFLICT | 编辑冲突 | 文件已被其他进程修改 | 重新加载后重试 |

### 异常处理流程

```
检测到异常
    ↓
分类异常类型（可恢复/不可恢复）
    ↓
可恢复？→ 是 → 尝试自动修复（最多 2 次）
    ↓           ↓
    否      成功？→ 是 → 继续执行
    ↓           ↓
记录异常    失败 → 回滚并上报
    ↓
生成异常报告
```

### 重试策略

- **最大重试次数**: 2 次
- **重试间隔**: 指数退避（1s, 2s, 4s）
- **重试条件**: 文件锁定、编辑冲突等临时错误

## 📚 最佳实践

### 推荐做法

- ✅ **定期审查**: 每月至少执行一次审查模式
- ✅ **渐进清理**: 优先处理无关联影响的技能
- ✅ **归档而非删除**: 重要技能归档而非直接删除
- ✅ **用户确认**: 所有遗忘操作需用户确认
- ✅ **行级修改**: 优先使用行级修改而非整文件替换
- ✅ **关联保护**: 遗忘前必须验证关联技能

### 避免做法

- ❌ **大规模删除**: 避免一次性删除多个技能
- ❌ **破坏性遗忘**: 避免影响其他技能的遗忘
- ❌ **未经确认**: 不要未经用户确认自动遗忘
- ❌ **粗暴删除**: 避免不使用行级修改的直接删除
- ❌ **忽视关联**: 不要忽视技能间的关联关系

### 性能优化

- 使用缓存存储技能元数据
- 增量分析而非全量分析
- 并行处理独立的遗忘操作
- 定期清理日志文件

### 安全建议

- 所有遗忘前创建 Git 提交点
- 重要技能遗忘需用户确认
- 保留遗忘历史记录
- 定期备份技能库

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
SKILLS_PATH=./AIKnowledge/Skills

# 可选配置
FREQUENCY_THRESHOLD=0.5
RECENCY_THRESHOLD=90
VALUE_THRESHOLD=30
AUTO_APPROVE_THRESHOLD=0.95
MAX_FORGETTING_PER_RUN=5
ENABLE_AUTO_ARCHIVE=true
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_forgetting_config.yaml
skill_forgetting:
  version: 1.0.0
  
  paths:
    skills: "./AIKnowledge/Skills"
    archive: "./AIKnowledge/Skills/Archived"
    
  thresholds:
    frequency_per_week: 0.5  # 低于此值标记为低频
    days_since_last_use: 90  # 超过此天数标记为过时
    value_score: 30  # 低于此分数建议废弃
    
  audit:
    schedule: "monthly"  # weekly, monthly, quarterly
    include_archived: false
    
  impact_analysis:
    enabled: true
    max_impact_skills: 3  # 最多影响 3 个技能可接受
    
  migration:
    auto_migrate: false  # 是否自动迁移
    backup_before_migrate: true
    
  line_editing:
    enabled: true
    backup_before_edit: true
    verify_after_edit: true
    
  versioning:
    auto_increment: true
    semantic_versioning: true
    
  logging:
    level: info
    file: "./logs/skill_forgetting.log"
    max_size: "10MB"
    retention_days: 30
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的分析和决策过程
- **INFO**: 关键步骤信息（扫描完成、建议生成、遗忘执行等）
- **WARN**: 警告信息（低频技能、关联影响等）
- **ERROR**: 错误信息（迁移失败、编辑冲突等）

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 技能健康度 | 健康技能占比 | < 70% |
| 平均技能年龄 | 技能平均未使用天数 | > 90 天 |
| 低频技能比例 | 低频技能占总技能比例 | > 30% |
| 遗忘接受率 | 用户接受的遗忘建议比例 | < 50% |
| 行级修改准确率 | 行级修改成功率 | < 95% |

### 监控仪表板示例

```
技能遗忘监控仪表板
=====================================
技能库概览:
- 技能总数：25
- 健康技能：18 (72%)
- 低频使用：5
- 过时技能：3
- 已归档：4

使用统计:
- 高频使用（>5 次/周）：8
- 中频使用（1-5 次/周）：10
- 低频使用（<1 次/周）：7

遗忘统计:
- 本月建议：5
- 用户接受：3
- 已执行遗忘：3
- 已归档：3

质量指标:
- 技能健康度：72% ⚠️
- 平均技能年龄：45 天
- 行级修改准确率：98%

告警:
- ⚠️ 技能健康度低于 70%
- ⚠️ 5 个技能使用频率过低
```

## 🧪 测试用例

### 单元测试

#### 测试用例 1：低频技能识别

```yaml
输入:
  skill:
    identifier: OldComponent
    usage_count: 2
    days_tracked: 60
    last_used_days_ago: 45
预期输出:
  frequency_level: "very_low"
  suggestion: "建议废弃"
  reason: "使用频率过低 (0.23 次/周)"
结果: ✅ 通过
```

#### 测试用例 2：关联影响评估

```yaml
输入:
  skill:
    identifier: CoreUtility
    dependents: ["SkillA", "SkillB", "SkillC"]
预期输出:
  impact_level: "moderate"
  impact_count: 3
  suggestion: "需先更新 3 个相关技能"
结果: ✅ 通过
```

#### 测试用例 3：行级修改

```yaml
输入:
  file: "ComponentGenerator/SKILL.md"
  line: 125
  operation: "replace"
  old_content: "参考 OldComponent 的实现"
  new_content: "参考 NewComponent 的实现"
预期输出:
  success: true
  lines_modified: 1
  file_updated: "ComponentGenerator/SKILL.md"
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整遗忘流程

**测试步骤**:
1. 执行技能库扫描
2. 识别出 3 个低频技能
3. 分析关联影响（1 个无影响，2 个有轻微影响）
4. 生成遗忘建议
5. 用户确认其中 2 个
6. 执行迁移（更新相关技能引用）
7. 执行遗忘（移动文件到归档目录）
8. 验证关联技能未受影响

**预期结果**: 
- 扫描完整
- 建议合理
- 迁移成功
- 遗忘成功
- 验证通过

**实际结果**: [待填写]

### 测试覆盖率要求

- 语句覆盖率：≥ 85%
- 分支覆盖率：≥ 80%
- 函数覆盖率：≥ 95%

## 📖 示例

### 示例 1：定期技能库审查

**场景**: 每月底进行技能库健康检查

**执行命令**:
```bash
skill-forgetting audit --output-format=markdown
```

**输出报告**:
```markdown
# 技能库健康报告 - 2026 年 3 月

## 概览
- 技能总数：25
- 健康技能：18 (72%)
- 需要关注：7

## 低频使用技能

### 1. DeprecatedTool (优先级：高)
- **使用频率**: 0 次/周
- **最后使用**: 120 天前
- **价值评分**: 15/100
- **关联影响**: 无
- **建议**: 直接遗忘（删除文件）

### 2. OldWorkflow (优先级：高)
- **使用频率**: 0.1 次/周
- **最后使用**: 95 天前
- **价值评分**: 22/100
- **关联影响**: 轻微（1 个技能引用）
- **建议**: 迁移引用后遗忘

### 3. LegacyAPI (优先级：中)
- **使用频率**: 0.2 次/周
- **最后使用**: 60 天前
- **价值评分**: 28/100
- **关联影响**: 中等（2 个技能依赖）
- **建议**: 标记为废弃，添加迁移指引

## 行动建议
1. 优先遗忘 DeprecatedTool（无关联影响）
2. 迁移 OldWorkflow 的引用后遗忘
3. 标记 LegacyAPI 为废弃状态
```

### 示例 2：行级修改技能内容

**场景**: 更新技能中的过时示例代码

**执行命令**:
```bash
skill-forgetting edit --file="ComponentGenerator/SKILL.md" --line=125 --operation=replace --content="参考 NewComponent 的实现（已迁移）"
```

**Agent 执行**:
```
✅ **行级修改成功**

**文件**: ComponentGenerator/SKILL.md
**操作**: 替换第 125 行
**修改前**: 参考 OldComponent 的实现
**修改后**: 参考 NewComponent 的实现（已迁移）

**验证**:
✅ 文件已保存
✅ 语法检查通过
✅ 引用有效性验证通过

**版本更新**:
- 版本号：1.0.0 → 1.0.1
- 更新日期：2026-03-31
```

### 示例 3：遗忘技能并迁移关联

**场景**: 遗忘一个被其他技能引用的低频技能

**执行命令**:
```bash
skill-forgetting execute --skill=OldComponent --migrate=true
```

**Agent 主动建议**:
```
🔍 **遗忘分析与建议**

**技能**: OldComponent

**使用分析**:
- 使用频率：0.2 次/周 ⚠️
- 最后使用：95 天前 ⚠️
- 价值评分：22/100 ⚠️

**关联分析**:
- 被 2 个技能引用：
  * ComponentGenerator (第 125 行)
  * LegacyIntegration (第 45 行)
- 影响程度：中等

**迁移方案**:
1. 更新 ComponentGenerator 的引用 → NewComponent
2. 更新 LegacyIntegration 的依赖 → NewComponent
3. 将 OldComponent 移动到归档目录

**预期收益**:
- 📉 技能库精简 1 个技能
- 🔍 检索效率提升
- 💾 存储空间节省

**风险**:
- ⚠️ 需要更新 2 个相关技能
- ⚠️ 需验证迁移后引用有效

是否执行此遗忘操作？
```

**用户确认**:
```
是的，执行遗忘
```

**Agent 执行**:
```
✅ **遗忘执行成功**

**步骤 1：迁移关联引用**
- ✅ 更新 ComponentGenerator/SKILL.md (第 125 行)
- ✅ 更新 LegacyIntegration/SKILL.md (第 45 行)

**步骤 2：归档技能**
- ✅ 移动 OldComponent 到 Archived/OldComponent/
- ✅ 更新技能注册中心

**步骤 3：验证**
- ✅ 所有引用验证通过
- ✅ 依赖关系完整
- ✅ 无断链引用

**遗忘完成**:
- 已遗忘技能：OldComponent
- 已更新技能：2 个
- 归档位置：Archived/OldComponent/
```

## 🔗 相关资源

### 前置技能
- [SkillEvolution](../SkillEvolution/SKILL.md) - 技能进化与关联
- [MetaCognitiveSelfExpansion](../MetaCognitiveSelfExpansion/SKILL.md) - 元认知与自我扩展

### 后续技能
- [SkillDeployment](链接) - 技能部署与发布
- [SkillMetrics](链接) - 技能度量与分析

### 参考资料
- [知识管理最佳实践](链接)
- [技能生命周期管理](链接)
- [依赖关系分析](链接)
- [行级编辑技术](链接)

### 工具依赖
- [文件操作库](https://nodejs.org/api/fs.html) - 文件和目录操作
- [文本编辑库](https://github.com/occultery/line-reader) - 行级文本编辑
- [图算法库](https://networkx.org/) - 依赖关系分析
- [版本管理](https://git-scm.com/) - 版本控制和回滚

## ❓ FAQ

### Q1: 如何避免误删重要技能？

**问题**: 担心遗忘技能时误删仍然重要的技能。

**解答**: 
1. **多重验证**: 遗忘前进行使用频率、新鲜度、关联影响三重验证
2. **用户确认**: 所有遗忘操作必须经用户确认
3. **归档机制**: 优先归档而非直接删除，可恢复
4. **回滚机制**: 保留 Git 提交点，可随时回滚

```yaml
safety_measures:
  require_user_confirmation: true
  archive_before_delete: true
  create_git_commit_before: true
  backup_retention_days: 30
```

**相关资源**: [安全遗忘指南](链接)

### Q2: 行级修改和整文件替换有什么区别？

**问题**: 不理解行级修改的优势。

**解答**: 

**整文件替换**:
- 读取整个文件
- 替换全部内容
- 风险高，可能丢失重要内容
- 无法追踪具体修改

**行级修改**:
- 精确定位到特定行
- 只修改目标行，保留其他内容
- 风险低，影响范围小
- 修改记录清晰

**示例**:
```bash
# 整文件替换（不推荐）
write_file("Skill/SKILL.md", new_content)

# 行级修改（推荐）
edit_line("Skill/SKILL.md", line=125, operation="replace", content="新内容")
```

**相关资源**: [行级编辑最佳实践](链接)

### Q3: 如何处理技能的关联依赖？

**问题**: 技能间有关联关系，如何安全遗忘？

**解答**: 
1. **依赖扫描**: 扫描所有技能的依赖关系
2. **影响评估**: 评估遗忘对依赖技能的影响
3. **迁移规划**: 规划依赖迁移方案
4. **执行迁移**: 更新依赖技能的引用
5. **验证**: 验证迁移后引用有效

**流程**:
```
识别依赖 → 评估影响 → 规划迁移 → 执行迁移 → 验证 → 遗忘
```

**示例**:
```yaml
skill: OldComponent
dependents:
  - ComponentGenerator (引用示例)
  - LegacyIntegration (依赖接口)

迁移方案:
1. ComponentGenerator: 更新示例 → NewComponent
2. LegacyIntegration: 更新依赖 → NewComponent
3. 验证引用有效
4. 遗忘 OldComponent
```

**相关资源**: [依赖管理指南](链接)

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的技能遗忘与清理能力 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)  
**文档**: [完整文档](链接)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.0  
**状态**: 🟢 稳定
