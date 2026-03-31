---
name: MetaCognitiveSelfExpansion
description: 元认知与自我扩展专家，负责主动识别重复性任务模式（高频多步骤任务）并建议创建 Skill、识别可独立拆分的子任务（低耦合高内聚）并建议创建 Subagent、识别外部系统交互需求（工具/API/数据源）并建议引入 MCP、在执行任务过程中动态监控并主动提出能力扩展建议，适用于能力边界识别、自动化建议、任务优化、系统扩展场景
---

# 元认知与自我扩展

## 🎯 核心目标

赋予 Agent **元认知（Meta-cognition）** 与 **自我扩展** 的决策逻辑，使其能够：
1. 主动识别重复性任务模式，建议创建 Skill 实现自动化
2. 识别可独立拆分的子任务，建议创建 Subagent 实现并行处理
3. 识别外部系统交互需求，建议引入 MCP 扩展能力边界
4. 在执行任务过程中动态监控，主动提出能力扩展建议

## 🎯 适用场景

- ✅ **重复性多步骤任务**：识别高频重复任务，建议创建 Skill
- ✅ **复杂任务拆分**：识别可独立执行的子任务，建议创建 Subagent
- ✅ **外部系统交互**：识别需要外部工具/数据的任务，建议引入 MCP
- ✅ **上下文优化**：识别上下文压力，建议将任务委派给 Subagent
- ✅ **能力边界识别**：识别当前能力不足，主动请求扩展
- ✅ **任务规划阶段**：在执行前主动评估并提出扩展建议

### 不适用场景
- ❌ 简单一次性任务（步骤<3 且无重复性）
- ❌ 用户明确要求不创建新资源
- ❌ 实验性或探索性任务（模式未定型）

## 🏗️ 技能架构

### 架构图

```
MetaCognitiveSelfExpansion (元认知核心)
├── CapabilityRegistry (能力注册中心)
│   ├── Skills Registry (已有技能清单)
│   ├── Subagents Registry (子代理清单)
│   └── MCP Registry (MCP 连接清单)
├── TaskAnalyzer (任务分析器)
│   ├── PatternRecognizer (模式识别)
│   ├── ComplexityEstimator (复杂度评估)
│   └── ResourceRequirementAnalyzer (资源需求分析)
├── DecisionEngine (决策引擎)
│   ├── SkillSuggestionEngine (Skill 建议引擎)
│   ├── SubagentSuggestionEngine (Subagent 建议引擎)
│   └── MCPSuggestionEngine (MCP 建议引擎)
└── ExpansionGenerator (扩展生成器)
    ├── SkillGenerator (Skill 配置生成)
    ├── SubagentGenerator (Subagent 配置生成)
    └── MCPConfigGenerator (MCP 配置生成)
```

### 组件说明

| 组件名称 | 角色 | 职责 | 工具 |
|---------|------|------|------|
| CapabilityRegistry | 能力注册中心 | 维护所有可用能力清单 | 内存数据库 |
| TaskAnalyzer | 任务分析器 | 分析任务特征、识别模式 | 模式识别算法 |
| DecisionEngine | 决策引擎 | 根据分析结果生成扩展建议 | 决策树、规则引擎 |
| ExpansionGenerator | 扩展生成器 | 生成配置文件和安装指引 | 模板引擎 |

## 🔄 工作流程

### 主工作流程

```
任务接收 → 能力匹配检查 → 任务拆解 → 模式识别 → 决策判断 → 主动建议 → 配置生成 → 用户确认 → 能力注册
    ↓           ↓              ↓          ↓          ↓          ↓          ↓          ↓          ↓
[用户请求]  [检查现有能力]  [分解子任务] [识别重复/复杂] [判断是否扩展] [提出建议] [生成配置] [用户授权] [更新清单]
```

### 详细步骤

#### 步骤 1：能力匹配检查

**目标**: 检查当前任务是否已有对应的 Skill、Subagent 或 MCP 可用

**输入**: 
- 用户任务描述
- 当前能力清单（Skills、Subagents、MCPs）

**处理过程**:
1. 解析任务关键词和意图
2. 在能力注册中心中搜索匹配项
3. 评估匹配度（0-100%）
4. 如果匹配度>80%，直接调用现有能力

**输出**: 
- 匹配结果（已匹配/未匹配）
- 匹配度评分
- 推荐使用的能力列表

**质量标准**:
- [ ] 搜索覆盖率 100%
- [ ] 匹配度评估准确
- [ ] 推荐排序合理

**示例**:
```
输入："创建 UserCard 组件并生成测试"
匹配结果：已匹配
匹配度：85%
推荐使用：create-component Skill
```

#### 步骤 2：任务拆解与分析

**目标**: 将复杂任务分解为可执行的子任务，并分析每个子任务的特征

**输入**: 用户任务

**处理过程**:
1. 使用任务规划算法分解任务
2. 为每个子任务标注：
   - 预计步骤数
   - 预计执行时间
   - 所需工具/资源
   - 是否依赖外部系统
   - 是否可独立执行
3. 识别子任务间的依赖关系

**输出**: 
- 子任务列表
- 任务依赖图（DAG）
- 资源需求清单

**质量标准**:
- [ ] 子任务分解完整
- [ ] 依赖关系正确
- [ ] 资源需求准确

#### 步骤 3：模式识别

**目标**: 识别任务中的重复模式、复杂模式或外部依赖模式

**输入**: 子任务列表、历史任务记录

**处理过程**:
1. **重复模式识别**：
   - 检查当前子任务是否在历史任务中出现≥3 次
   - 计算任务相似度（使用语义相似度算法）
   - 如果相似度>70% 且步骤数>3，标记为"可 Skill 化"

2. **独立性识别**：
   - 检查子任务是否可独立执行（不需要主对话上下文）
   - 评估执行时间（>1 分钟标记为"耗时"）
   - 检查是否需要专用工具

3. **外部依赖识别**：
   - 检查子任务是否需要访问外部系统
   - 识别外部系统类型（数据库、API、文件系统等）
   - 检查是否已有对应的 MCP 连接

**输出**: 
- 模式识别报告
- 建议扩展类型（Skill/Subagent/MCP）
- 优先级评分

**质量标准**:
- [ ] 模式识别准确率>90%
- [ ] 建议合理性高
- [ ] 优先级评分客观

#### 步骤 4：决策判断与建议生成

**目标**: 根据模式识别结果，生成具体的扩展建议

**输入**: 模式识别报告

**处理过程**:
1. 根据扩展类型选择建议引擎
2. 生成建议文本（包含：问题描述、解决方案、预期收益）
3. 估算效率提升（时间节省、质量提升等）
4. 生成配置文件草稿

**输出**: 
- 建议文本
- 配置文件草稿
- 安装/配置指引

**质量标准**:
- [ ] 建议清晰易懂
- [ ] 收益估算合理
- [ ] 配置文件可执行

#### 步骤 5：用户确认与能力注册

**目标**: 获得用户授权后，完成能力扩展

**输入**: 用户确认

**处理过程**:
1. 用户确认建议
2. 保存配置文件到指定目录
3. 执行安装/配置命令（如需要）
4. 更新能力注册中心
5. 生成使用示例

**输出**: 
- 新能力已注册
- 使用文档
- 示例用法

**质量标准**:
- [ ] 配置正确
- [ ] 能力立即可用
- [ ] 文档完整

## 👥 决策规则引擎

### Skill 创建决策规则

```python
def should_suggest_skill(task_analysis):
    """
    判断是否建议创建 Skill
    """
    # 规则 1：重复性任务
    if task_analysis.frequency >= 3 and task_analysis.steps >= 3:
        if not exists_matching_skill(task_analysis):
            return True, "重复性多步骤任务"
    
    # 规则 2：用户表达繁琐
    if detect_user_frustration(task_analysis.user_input):
        # 检测"又得..."、"每次都要..."等信号
        return True, "用户表达流程繁琐"
    
    # 规则 3：复杂度超出单次交互
    if task_analysis.complexity_score > 7 and task_analysis.requires_multiple_confirmations:
        return True, "任务复杂度高，需要一键完成"
    
    return False, None
```

### Subagent 创建决策规则

```python
def should_suggest_subagent(task_analysis, context_state):
    """
    判断是否建议创建 Subagent
    """
    # 规则 1：可独立拆分的子任务
    if task_analysis.can_be_isolated and task_analysis.execution_time > 60:
        if not exists_suitable_subagent(task_analysis):
            return True, "独立子任务，执行时间长"
    
    # 规则 2：上下文容量压力
    if context_state.turn_count > 10 and context_state.token_usage > 8000:
        if task_analysis.can_be_delegated:
            return True, "上下文压力大，适合委派"
    
    # 规则 3：并行需求
    if task_analysis.requires_parallel_execution:
        return True, "需要并行处理多个任务"
    
    return False, None
```

### MCP 引入决策规则

```python
def should_suggest_mcp(task_analysis, mcp_registry):
    """
    判断是否建议引入 MCP
    """
    # 规则 1：需要外部系统数据
    if task_analysis.requires_external_system:
        required_mcp = identify_required_mcp(task_analysis)
        if not mcp_registry.has_mcp(required_mcp):
            if mcp_exists_standard(required_mcp):
                return True, f"需要配置 {required_mcp} MCP"
            else:
                return True, f"需要创建自定义 MCP"
    
    # 规则 2：需要持久化操作
    if task_analysis.requires_persistence:
        target_system = task_analysis.persistence_target
        if not mcp_registry.has_mcp_for(target_system):
            return True, f"需要 {target_system} MCP 支持持久化"
    
    # 规则 3：需要自动化交互
    if task_analysis.requires_automation:
        if task_analysis.trigger_type in ['scheduled', 'event']:
            return True, "需要 MCP 实现定时/事件触发"
    
    return False, None
```

## ⚙️ 执行模式

### Mode A: 被动模式（Passive Mode）

- **描述**: 仅在用户明确询问时提供建议
- **包含阶段**: 任务分析 → 能力匹配 → 执行
- **使用场景**: 用户希望完全控制，不需要主动建议
- **预计耗时**: 最短

### Mode B: 主动建议模式（Active Suggestion Mode）

- **描述**: 在任务规划阶段主动识别扩展需求并提出建议
- **包含阶段**: 任务分析 → 能力匹配 → 模式识别 → 决策判断 → **主动建议** → 用户确认 → 执行
- **使用场景**: 默认模式，平衡主动性和干扰性
- **预计耗时**: 中等

### Mode C: 全自动模式（Full Auto Mode）

- **描述**: 自动识别并创建扩展，无需用户确认（在预设规则内）
- **包含阶段**: 任务分析 → 能力匹配 → 模式识别 → 决策判断 → **自动创建** → 执行 → 事后报告
- **使用场景**: 用户已授权，信任 Agent 判断
- **预计耗时**: 最长（初期），但长期效率最高

## 🚀 快速开始

### 前置条件

- [ ] Agent 已加载 MetaCognitiveSelfExpansion 技能
- [ ] 能力注册中心已初始化
- [ ] 配置文件存储目录已创建

### 基本用法

```bash
# 模式 1：被动模式
使用技能时添加 --mode=passive

# 模式 2：主动建议模式（默认）
使用技能时添加 --mode=active 或不指定

# 模式 3：全自动模式
使用技能时添加 --mode=auto --auto-approve=true
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `--mode` | string | 否 | "active" | 执行模式（passive/active/auto） |
| `--auto-approve` | boolean | 否 | false | 是否自动批准创建（仅 auto 模式有效） |
| `--suggestion-threshold` | number | 否 | 0.7 | 建议触发阈值（0-1，越高越不主动） |
| `--max-suggestions` | number | 否 | 3 | 单次任务最多建议数 |

## 📋 输入输出规范

### 输入格式

```json
{
  "task": "类型：string，说明：用户任务描述",
  "context": {
    "type": "object",
    "description": "当前对话上下文",
    "properties": {
      "turn_count": "类型：number，当前对话轮数",
      "token_usage": "类型：number，已用 token 数",
      "history_tasks": "类型：array，历史任务列表"
    }
  },
  "mode": "类型：string，说明：执行模式（passive/active/auto）",
  "config": {
    "type": "object",
    "description": "配置选项",
    "properties": {
      "suggestion_threshold": "类型：number，建议阈值",
      "max_suggestions": "类型：number，最大建议数"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|suggestion_pending|executing",
  "task_analysis": {
    "subtasks": "子任务列表",
    "complexity_score": "复杂度评分（1-10）",
    "estimated_time": "预计执行时间（秒）",
    "pattern_detected": "识别到的模式"
  },
  "suggestions": [
    {
      "type": "skill|subagent|mcp",
      "priority": "high|medium|low",
      "title": "建议标题",
      "description": "详细描述",
      "expected_benefit": "预期收益",
      "config_draft": "配置草稿",
      "installation_guide": "安装指引"
    }
  ],
  "next_action": "execute|wait_for_confirmation|create_expansion"
}
```

## ✅ 质量门禁

### 检查清单

#### 完整性检查
- [ ] 能力注册中心完整（Skills、Subagents、MCPs）
- [ ] 任务分析完整（所有子任务已识别）
- [ ] 模式识别完整（所有模式已检测）
- [ ] 建议生成完整（所有必要建议已提出）

#### 准确性检查
- [ ] 模式识别准确率>90%
- [ ] 建议合理性评分>0.8
- [ ] 收益估算误差<20%
- [ ] 配置文件可执行率 100%

#### 性能检查
- [ ] 任务分析响应时间 < 2 秒
- [ ] 模式识别响应时间 < 1 秒
- [ ] 建议生成响应时间 < 1 秒
- [ ] 总体额外开销 < 5 秒

### 验收标准

- [ ] 能正确识别重复任务（≥3 次，≥3 步）
- [ ] 能正确识别独立子任务（执行时间>1 分钟）
- [ ] 能正确识别外部依赖需求
- [ ] 建议文本清晰、具体、可操作
- [ ] 生成的配置文件可直接使用
- [ ] 用户确认后能力立即可用

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_NO_PATTERN | 未识别到可扩展模式 | 任务确实无模式或阈值过高 | 降低 suggestion_threshold 或继续观察 |
| ERR_CONFIG_INVALID | 生成的配置文件无效 | 模板错误或参数缺失 | 检查模板，补充必要参数 |
| ERR_MCP_NOT_FOUND | 建议的 MCP 不存在 | MCP 标准协议未定义 | 建议创建自定义 MCP 或寻找替代方案 |
| ERR_REGISTRY_FULL | 能力注册中心已满 | 达到存储上限 | 清理不常用的能力或扩展存储 |

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
记录异常    失败 → 上报用户并请求协助
    ↓
返回错误信息和建议
```

### 重试策略

- **最大重试次数**: 2 次
- **重试间隔**: 指数退避（0.5s, 1s, 2s）
- **重试条件**: 配置生成失败、注册失败等临时错误

## 📚 最佳实践

### 推荐做法

- ✅ **早期介入**: 在任务规划阶段就提出建议，而非执行中
- ✅ **具体明确**: 建议包含具体的配置草稿和预期收益
- ✅ **用户授权**: 创建前必须获得用户明确确认（auto 模式除外）
- ✅ **渐进式扩展**: 优先创建高频、高收益的能力
- ✅ **文档同步**: 创建能力时同步生成使用文档

### 避免做法

- ❌ **过度建议**: 避免对简单任务提出扩展建议
- ❌ **模糊描述**: 避免使用"可能"、"也许"等模糊词汇
- ❌ **先斩后奏**: 避免未经确认自动创建（除非 auto 模式且已授权）
- ❌ **重复建议**: 避免对已拒绝的建议重复提出

### 性能优化

- 使用缓存存储历史任务模式
- 使用增量分析而非全量分析
- 并行执行多个分析引擎
- 定期清理低使用率的能力注册

### 安全建议

- 所有配置文件生成后需用户确认
- 外部 MCP 连接需明确权限范围
- 定期审计已创建的能力使用情况
- 对自动执行的操作保留完整日志

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
CAPABILITY_REGISTRY_PATH=/path/to/registry
SKILL_TEMPLATE_PATH=/path/to/skill/template
SUBAGENT_TEMPLATE_PATH=/path/to/subagent/template
MCP_CONFIG_PATH=/path/to/mcp/config

# 可选配置
SUGGESTION_THRESHOLD=0.7
MAX_SUGGESTIONS_PER_TASK=3
ENABLE_AUTO_MODE=false
LOG_LEVEL=info
```

### 配置文件

```yaml
# meta_cognitive_config.yaml
meta_cognitive:
  version: 1.0.0
  mode: active
  
  capability_registry:
    skills_path: "./AIKnowledge/Skills"
    subagents_path: "./AIKnowledge/SubAgent"
    mcp_config_path: "./.mcp-config"
  
  suggestion_engine:
    threshold: 0.7
    max_suggestions: 3
    min_frequency_for_skill: 3
    min_steps_for_skill: 3
    min_time_for_subagent: 60  # seconds
    max_context_turns: 10
  
  auto_mode:
    enabled: false
    auto_approve_threshold: 0.95  # 只有置信度>95% 才自动批准
    max_auto_creations_per_day: 5
  
  logging:
    level: info
    file: "./logs/meta_cognitive.log"
    max_size: "10MB"
    retention_days: 30
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的分析过程和决策逻辑
- **INFO**: 关键步骤信息（建议提出、用户确认、能力创建）
- **WARN**: 警告信息（建议被拒绝、配置异常）
- **ERROR**: 错误信息（分析失败、创建失败）

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 建议接受率 | 用户接受的建议比例 | < 30% |
| 模式识别准确率 | 识别到模式后确实需要扩展的比例 | < 80% |
| 平均建议数/任务 | 每个任务平均提出的建议数 | > 5 |
| 能力使用率 | 创建的能力中被频繁使用的比例 | < 50% |
| 自动创建成功率 | 自动创建后立即可用的比例 | < 95% |

### 监控仪表板示例

```
元认知与自我扩展 - 监控仪表板
=====================================
今日统计:
- 处理任务数：45
- 提出建议数：12
- 用户接受数：8 (接受率：66.7%)
- 自动创建数：0 (auto 模式未启用)

能力库统计:
- Skills 总数：23 (今日新增：2)
- Subagents 总数：5 (今日新增：0)
- MCPs 总数：8 (今日新增：1)

性能指标:
- 平均分析时间：1.2 秒
- 平均建议生成时间：0.8 秒
- 模式识别准确率：92%

Top 使用技能:
1. create-component (使用次数：15)
2. code-reviewer (使用次数：12)
3. documentation-engineer (使用次数：10)

告警:
- 无
```

## 🧪 测试用例

### 单元测试

#### 测试用例 1：重复任务识别

```yaml
输入:
  task: "创建 UserCard 组件并生成测试"
  context:
    history_tasks:
      - "创建 LoginButton 组件并生成测试"
      - "创建 NavBar 组件并生成测试"
      - "创建 Footer 组件并生成测试"
预期输出:
  suggestions:
    - type: skill
      title: "建议创建 create-component-test Skill"
      priority: high
      expected_benefit: "每次节省约 5 分钟，减少重复操作"
结果: ✅ 通过
```

#### 测试用例 2：Subagent 建议

```yaml
输入:
  task: "对 src/components/ 下的 20 个文件进行代码风格检查"
  context:
    turn_count: 15
    token_usage: 9500
预期输出:
  suggestions:
    - type: subagent
      title: "建议创建 code-style-checker Subagent"
      priority: high
      expected_benefit: "后台并行执行，不占用主对话上下文"
结果: ✅ 通过
```

#### 测试用例 3：MCP 引入建议

```yaml
输入:
  task: "将这份报告写入 PostgreSQL 数据库"
  context:
    mcp_registry: []
预期输出:
  suggestions:
    - type: mcp
      title: "建议引入 PostgreSQL MCP"
      priority: high
      expected_benefit: "获得数据库读写能力，支持 SQL 查询和数据导入"
      installation_guide: "npm install @mcp/postgresql-server"
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整工作流

**测试步骤**:
1. 用户输入："又要创建新组件了，这是本周第三次了"
2. Agent 识别用户表达繁琐
3. Agent 检查历史任务，发现 3 次相似任务
4. Agent 生成 Skill 创建建议
5. 用户确认
6. Agent 生成 skill.yaml 并注册
7. Agent 提供使用示例

**预期结果**: 
- 成功识别重复模式
- 建议合理且具体
- Skill 创建成功并立即可用

**实际结果**: [待填写]

### 测试覆盖率要求

- 语句覆盖率：≥ 85%
- 分支覆盖率：≥ 80%
- 函数覆盖率：≥ 95%

## 📖 示例

### 示例 1：识别重复任务并建议创建 Skill

**场景**: 用户在 1 小时内第三次要求创建组件

**用户输入**:
```
帮我创建 UserCard 组件，需要 TypeScript、React、Jest 测试，然后更新 index 导出
```

**Agent 思考过程**:
```
1. 分析任务：
   - 步骤：创建文件 → 写代码 → 写测试 → 更新导出（4 步）
   - 复杂度：中等
   - 预计时间：8-10 分钟

2. 检查历史任务：
   - 过去 1 小时内：
     * 创建 LoginButton 组件（相似）
     * 创建 NavBar 组件（相似）
   - 任务相似度：85%
   - 频率：3 次/小时

3. 模式识别：
   - ✅ 重复性任务（≥3 次）
   - ✅ 多步骤（≥3 步）
   - ✅ 无对应 Skill

4. 决策判断：
   - 建议类型：Skill
   - 优先级：高
   - 预期收益：每次节省 5-8 分钟

5. 生成建议：
   - Skill 名称：create-component-test
   - 配置草稿：已生成
   - 使用示例：已准备
```

**Agent 主动建议**:
```
🔍 **智能建议**

我注意到这是您在过去 1 小时内第三次要求创建组件了（之前创建了 LoginButton 和 NavBar）。

这个过程包含 4 个步骤：
1. 创建组件文件
2. 编写组件代码
3. 生成 Jest 测试
4. 更新 index 导出

**建议**: 创建一个名为 `create-component-test` 的 Skill 来自动化这个流程。

**预期收益**:
- ⏱️ 每次节省约 5-8 分钟
- 📉 减少重复操作错误
- 🚀 简化为一条命令："用 create-component-test 创建 UserCard"

**配置草稿**已生成，包含：
- 组件模板（支持 TypeScript + React）
- 测试模板（Jest + Testing Library）
- 自动导出逻辑

是否需要我创建这个 Skill？创建后您只需说："用 create-component-test 创建 UserCard"即可。
```

**用户确认**:
```
好的，创建这个 Skill
```

**Agent 执行**:
```
✅ **Skill 创建成功**

已创建 `create-component-test` Skill，配置文件已保存到：
`./AIKnowledge/Skills/create-component-test/skill.yaml`

**使用方法**:
```
用 create-component-test 创建 [组件名]
```

**示例**:
```
用 create-component-test 创建 UserCard
```

这将自动完成：
1. ✅ 创建 UserCard.tsx（使用模板）
2. ✅ 创建 UserCard.test.tsx（使用模板）
3. ✅ 更新 components/index.ts 导出

现在请试试说："用 create-component-test 创建 UserCard" 🚀
```

### 示例 2：识别独立子任务并建议创建 Subagent

**场景**: 用户要求对 20 个文件进行代码审查

**用户输入**:
```
帮我检查 src/components/ 目录下所有文件的代码风格和潜在问题
```

**Agent 主动建议**:
```
🔍 **智能建议**

我检测到 `src/components/` 目录下有 20 个文件需要进行代码风格检查。

**任务分析**:
- 📊 文件数量：20 个
- ⏱️ 预计执行时间：15-20 分钟
- 💾 上下文占用：约 8000 tokens
- 🔄 交互需求：低（检查过程不需要频繁确认）

**建议**: 创建一个名为 `code-style-checker` 的 Subagent 来专门执行这项任务。

**优势**:
- 🚀 **并行执行**: Subagent 在后台独立运行，不影响您继续提问
- 📝 **汇总报告**: 完成后返回结构化汇总报告，而非逐个文件输出
- 💾 **节省上下文**: 避免主对话上下文过快增长
- 🔧 **可复用**: 未来可随时调用此 Subagent 进行代码检查

**Subagent 配置**已生成，包含：
- 提示词：专注于代码风格和问题检测
- 工具：ESLint、Prettier、自定义规则
- 输出：结构化报告（Markdown 格式）

是否需要我创建这个 Subagent？创建后它会在后台运行，完成后通知您。
```

**用户确认**:
```
好的，创建这个 Subagent 并开始检查
```

**Agent 执行**:
```
✅ **Subagent 创建成功并启动**

已创建 `code-style-checker` Subagent，配置已保存到：
`./AIKnowledge/SubAgent/code-style-checker/subagent.yaml`

**执行状态**:
- 🟡 运行中...
- 📂 检查目录：src/components/ (20 个文件)
- ⏱️ 预计完成时间：15-20 分钟

**您可以**:
1. ✅ 继续与我讨论其他问题（Subagent 在后台独立运行）
2. ✅ 随时询问进度："code-style-checker 进度如何？"
3. ⏰ 等待完成通知

Subagent 完成后会返回：
- 📊 总体评分
- 🐛 问题列表（按严重程度分类）
- 💡 改进建议
- 📝 修复示例

需要我帮您准备其他任务吗？
```

### 示例 3：识别外部依赖并建议引入 MCP

**场景**: 用户要求将数据写入数据库

**用户输入**:
```
把这份销售报告写入 PostgreSQL 数据库的 sales 表中
```

**Agent 主动建议**:
```
⚠️ **能力扩展请求**

您希望我将数据写入 PostgreSQL 数据库。目前我没有直接操作数据库的能力。

**需求分析**:
- 🎯 目标系统：PostgreSQL 数据库
- 📝 操作类型：数据写入（INSERT）
- 📊 数据内容：销售报告（结构化数据）
- 🔐 权限需求：写入权限

**建议**: 引入 PostgreSQL MCP（Model Context Protocol）服务器。

**引入后我能**:
- ✅ 执行 SQL 查询（SELECT、INSERT、UPDATE、DELETE）
- ✅ 连接并管理 PostgreSQL 数据库
- ✅ 批量导入/导出数据
- ✅ 执行数据库管理操作

**配置指引**:

1. **安装 MCP 服务器**:
```bash
npm install -g @mcp/postgresql-server
```

2. **创建配置文件** (`mcp.json`):
```json
{
  "mcpServers": {
    "postgresql": {
      "command": "mcp-postgresql-server",
      "args": ["--connection-string", "postgresql://user:password@host:port/database"],
      "env": {
        "DATABASE_URL": "postgresql://user:password@host:port/database"
      }
    }
  }
}
```

3. **替换连接字符串**:
将 `postgresql://user:password@host:port/database` 替换为您的实际连接信息

4. **重启对话**以加载 MCP

**安全提示**:
- 🔐 不要在配置文件中硬编码密码，使用环境变量
- 🔒 建议创建只读/写入分离的数据库用户
- 📝 记录所有数据库操作日志

是否需要我生成完整的 MCP 配置文件？您只需替换连接字符串并安装依赖即可。
```

**用户确认**:
```
好的，生成配置文件
```

**Agent 执行**:
```
✅ **MCP 配置文件已生成**

已创建 `mcp.json` 配置文件，内容如下：

```json
{
  "mcpServers": {
    "postgresql": {
      "command": "mcp-postgresql-server",
      "args": ["--connection-string", "${DATABASE_URL}"],
      "env": {
        "DATABASE_URL": "postgresql://your_user:your_password@your_host:5432/your_database"
      }
    }
  }
}
```

**下一步**:

1. **安装依赖**:
```bash
npm install -g @mcp/postgresql-server
```

2. **设置环境变量**（推荐）:
```bash
export DATABASE_URL="postgresql://your_user:your_password@your_host:5432/your_database"
```

3. **替换配置**中的占位符:
   - `your_user`: 数据库用户名
   - `your_password`: 数据库密码
   - `your_host`: 数据库主机地址
   - `your_database`: 数据库名称

4. **重启对话**以加载 MCP

完成后，您就可以说："把这份销售报告写入 PostgreSQL 数据库的 sales 表中"，我将能够直接执行！🚀

需要我提供更详细的安装指引吗？
```

### 示例 4：上下文优化建议

**场景**: 长对话后继续复杂任务

**用户输入**（在第 15 轮对话后）:
```
现在帮我重构整个项目的代码结构，包括所有组件、工具函数和样式文件
```

**Agent 主动建议**:
```
🔍 **智能建议**

当前对话已达到 15 轮，上下文 token 使用量约为 9500/12000。

**任务分析**:
- 📊 任务规模：重构整个项目（大型任务）
- ⏱️ 预计执行时间：30-45 分钟
- 💾 上下文需求：约 15000 tokens（超出当前剩余容量）
- 🔄 交互需求：中等（需要多次确认）

**建议**: 将重构任务委派给专用的 `project-refactor` Subagent。

**优势**:
- 🚀 **不占用主对话上下文**: Subagent 独立执行，主对话可继续其他任务
- 📝 **结构化输出**: 返回重构计划和执行报告，而非详细过程
- 🔧 **专业优化**: Subagent 专注于重构任务，使用专业工具和最佳实践
- ⏰ **异步执行**: 完成后通知您，无需等待

**Subagent 配置**已生成，包含：
- 提示词：项目重构专家，专注于代码结构优化
- 工具：AST 分析器、代码格式化器、依赖分析器
- 输出：重构报告 + 执行摘要

是否创建此 Subagent 并启动重构任务？
```

## 🔗 相关资源

### 前置技能
- [任务规划与分析](链接)
- [模式识别基础](链接)
- [配置文件生成](链接)

### 后续技能
- [Skill 开发指南](链接)
- [Subagent 设计模式](链接)
- [MCP 集成最佳实践](链接)

### 参考资料
- [元认知理论研究](https://en.wikipedia.org/wiki/Metacognition)
- [自我扩展 AI 系统设计](链接)
- [任务规划与决策引擎](链接)
- [能力注册中心设计规范](链接)

### 工具依赖
- [YAML 解析器](https://github.com/yaml/yaml) - 配置文件解析
- [模板引擎](https://handlebarsjs.com/) - 配置文件生成
- [语义相似度算法](https://github.com/UKPLab/sentence-transformers) - 任务相似度计算
- [决策树引擎](https://scikit-learn.org/) - 决策规则实现

## ❓ FAQ

### Q1: 如何避免 Agent 过度建议？

**问题**: Agent 频繁提出扩展建议，影响正常使用体验。

**解答**: 
1. **调整阈值**: 在配置文件中提高 `suggestion_threshold`（默认 0.7，可调至 0.8-0.9）
2. **限制频率**: 设置 `max_suggestions_per_task`（默认 3，可调至 1-2）
3. **切换模式**: 使用 `--mode=passive` 切换到被动模式
4. **设置免打扰时段**: 在配置中添加 `quiet_hours` 时间段

```yaml
suggestion_engine:
  threshold: 0.85  # 提高阈值
  max_suggestions: 2  # 减少最大建议数
  quiet_hours:
    start: "22:00"
    end: "08:00"
```

**相关资源**: [配置指南](链接)

### Q2: 创建的能力如何管理和清理？

**问题**: 随着时间推移，创建了大量 Skill 和 Subagent，如何管理？

**解答**: 
1. **查看清单**: 使用命令 `list-skills`、`list-subagents` 查看所有能力
2. **使用统计**: 每个能力都有 `last_used` 和 `usage_count` 字段
3. **定期清理**: 删除 30 天未使用且使用次数<5 的能力
4. **归档机制**: 不常用但不想删除的能力可归档

```bash
# 查看所有 Skills 及使用统计
list-skills --stats

# 删除 30 天未使用的 Skill
cleanup-skills --inactive-days=30

# 归档某个 Skill
archive-skill skill-name
```

**相关资源**: [能力管理指南](链接)

### Q3: 自动模式安全吗？如何控制风险？

**问题**: 担心 Auto 模式下 Agent 会创建不必要或有问题的配置。

**解答**: 
1. **置信度阈值**: 设置 `auto_approve_threshold`（默认 0.95，只有 95% 置信度才自动批准）
2. **每日限额**: 设置 `max_auto_creations_per_day`（默认 5 个）
3. **白名单机制**: 只对特定类型的扩展启用自动批准
4. **审计日志**: 所有自动创建的操作都有完整日志，可随时回滚

```yaml
auto_mode:
  enabled: true
  auto_approve_threshold: 0.95  # 高置信度才自动批准
  max_auto_creations_per_day: 5  # 每日限额
  whitelist:
    - "skill"  # 只允许自动创建 Skill
  require_confirmation_for:
    - "subagent"  # Subagent 需要确认
    - "mcp"  # MCP 需要确认
```

**安全建议**: 初期使用 Active 模式，熟悉后再启用 Auto 模式

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-30 | AI Assistant | 初始版本，包含完整的元认知与自我扩展能力 |
| 0.9.0 | 2026-03-29 | AI Assistant | 测试版本，添加核心决策引擎 |
