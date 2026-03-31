---
name: 技能性能优化器
identifier: SkillPerformanceOptimizer
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 性能优化
  - 技能优化
  - 性能分析
  - 元技能
  - 成本优化
---

# 技能性能优化器

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能性能优化器 |
| **英文标识名** | `SkillPerformanceOptimizer` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **技能性能分析** 与 **优化** 的能力，使其能够：
1. 分析技能执行性能瓶颈
2. 优化技能的提示词和工具调用
3. 减少 token 消耗和执行时间
4. 提供并行化和缓存策略优化
5. 降低技能执行成本

## 🎯 适用场景

- ✅ **性能分析**：分析技能性能瓶颈
- ✅ **执行时间优化**：减少技能执行时间
- ✅ **成本优化**：降低 token 消耗
- ✅ **大规模优化**：批量优化多个技能
- ✅ **性能调优**：持续性能改进
- ✅ **资源优化**：优化资源使用效率

### 不适用场景
- ❌ 技能功能开发（应使用 development-engineer）
- ❌ 技能测试（应使用 SkillTesting）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 核心组件

```
SkillPerformanceOptimizer (性能优化核心)
├── PerformanceAnalyzer (性能分析器)
│   ├── BottleneckDetector (瓶颈检测)
│   ├── Profiler (性能分析器)
│   └── MetricCollector (指标收集器)
├── OptimizationEngine (优化引擎)
│   ├── PromptOptimizer (提示词优化)
│   ├── ToolCallOptimizer (工具调用优化)
│   └── CacheOptimizer (缓存优化)
├── CostAnalyzer (成本分析器)
│   ├── TokenCalculator (Token 计算器)
│   ├── CostEstimator (成本估算)
│   └── ROICalculator (ROI 计算器)
└── SuggestionGenerator (建议生成器)
    ├── OptimizationSuggester (优化建议)
    ├── PriorityRanker (优先级排序)
    └── ImpactEstimator (影响估算)
```

## 🔄 工作流程

```
性能分析 → 瓶颈识别 → 优化方案 → 实施优化 → 效果验证 → 持续监控
    ↓          ↓          ↓          ↓          ↓          ↓
[性能数据] [瓶颈列表] [优化方案] [执行优化] [对比结果] [性能监控]
```

## ⚙️ 执行模式

### Mode A: 分析模式
- 深度分析技能性能
- 识别瓶颈和问题
- 耗时：5-10 分钟

### Mode B: 优化模式
- 实施优化建议
- 自动优化技能
- 耗时：10-20 分钟

### Mode C: 成本优化模式
- 专注于降低 token 消耗
- 优化成本效益
- 耗时：5-15 分钟

### Mode D: 批量优化模式
- 批量优化多个技能
- 规模化改进
- 耗时：取决于技能数量

## 👥 性能优化策略引擎

### 瓶颈检测算法

```python
def detect_bottlenecks(performance_metrics):
    """
    检测性能瓶颈
    """
    bottlenecks = []
    
    # 提示词瓶颈
    if performance_metrics.prompt_tokens > 2000:
        bottlenecks.append({
            "type": "prompt_too_long",
            "severity": "high",
            "current": performance_metrics.prompt_tokens,
            "threshold": 2000,
            "suggestion": "简化提示词，移除冗余描述"
        })
    
    # 执行时间瓶颈
    if performance_metrics.avg_execution_time > 5000:
        bottlenecks.append({
            "type": "slow_execution",
            "severity": "high",
            "current_ms": performance_metrics.avg_execution_time,
            "threshold_ms": 5000,
            "suggestion": "优化处理逻辑，减少不必要步骤"
        })
    
    # Token 效率瓶颈
    if performance_metrics.output_input_ratio < 0.3:
        bottlenecks.append({
            "type": "low_token_efficiency",
            "severity": "medium",
            "ratio": performance_metrics.output_input_ratio,
            "threshold": 0.3,
            "suggestion": "优化输出格式，减少冗余"
        })
    
    return bottlenecks
```

### 优化建议生成规则

```python
def generate_optimization_suggestions(bottlenecks, skill_config):
    """
    生成优化建议
    """
    suggestions = []
    
    for bottleneck in bottlenecks:
        if bottleneck['type'] == 'prompt_too_long':
            suggestions.append({
                "category": "prompt",
                "priority": "high",
                "title": "简化提示词",
                "description": "当前提示词过长，建议：",
                "actions": [
                    "移除冗余的背景描述",
                    "精简示例数量（保留 1-2 个典型示例）",
                    "使用结构化格式替代长文本",
                    "将通用说明移到系统提示"
                ],
                "expected_improvement": "执行时间减少 20-30%，token 消耗减少 25-35%",
                "effort": "medium",
                "risk": "low"
            })
        
        elif bottleneck['type'] == 'slow_execution':
            suggestions.append({
                "category": "execution",
                "priority": "high",
                "title": "优化执行流程",
                "description": "执行时间过长，建议：",
                "actions": [
                    "识别并消除串行瓶颈",
                    "并行化独立的操作",
                    "使用增量处理替代全量处理",
                    "添加缓存机制"
                ],
                "expected_improvement": "执行时间减少 30-50%",
                "effort": "high",
                "risk": "medium"
            })
    
    return suggestions
```

### 成本效益分析算法

```python
def calculate_roi(optimization_plan, current_metrics):
    """
    计算优化投资回报率
    """
    total_effort = sum(action['effort_score'] for action in optimization_plan)
    total_savings = sum(action['monthly_savings'] for action in optimization_plan)
    
    roi = {
        "total_effort_hours": total_effort,
        "monthly_cost_savings": total_savings,
        "payback_months": total_effort * 100 / total_savings if total_savings > 0 else float('inf'),
        "annual_roi_percent": (total_savings * 12 - total_effort * 100) / (total_effort * 100) * 100,
        "break_even_point": "立即" if total_savings > total_effort * 100 else f"{total_effort * 100 / total_savings:.1f}个月"
    }
    
    return roi
```

## 📋 输入输出规范

### 输入格式

```json
{
  "skill_identifier": "类型：string，说明：技能标识名",
  "optimization_config": {
    "type": "object",
    "description": "优化配置",
    "properties": {
      "focus_area": "类型：string，说明：优化重点（performance/cost/balanced）",
      "target_improvement": "类型：number，说明：目标改进百分比",
      "max_effort": "类型：string，说明：最大工作量（low/medium/high）",
      "include_breaking_changes": "类型：boolean，说明：是否允许破坏性变更"
    }
  },
  "performance_data": {
    "type": "object",
    "description": "性能数据",
    "properties": {
      "metrics": "类型：object，说明：性能指标",
      "time_range": "类型：string，说明：数据时间范围",
      "sample_size": "类型：number，说明：样本数量"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "analysis_summary": {
    "skill_identifier": "技能标识名",
    "analysis_duration_seconds": "分析耗时（秒）",
    "bottlenecks_found": "发现的瓶颈数",
    "optimization_suggestions": "优化建议数"
  },
  "current_performance": {
    "avg_execution_time_ms": "平均执行时间（毫秒）",
    "p95_execution_time_ms": "P95 执行时间（毫秒）",
    "avg_token_consumption": "平均 token 消耗",
    "cost_per_execution": "单次执行成本",
    "success_rate": "成功率"
  },
  "bottlenecks": [
    {
      "type": "瓶颈类型",
      "severity": "严重程度",
      "description": "描述",
      "impact": "影响",
      "current_value": "当前值",
      "threshold": "阈值"
    }
  ],
  "optimization_plan": [
    {
      "id": "优化项 ID",
      "category": "类别",
      "title": "标题",
      "priority": "优先级",
      "description": "描述",
      "actions": ["具体行动"],
      "effort": "工作量",
      "expected_improvement": "预期改进",
      "risk": "风险等级"
    }
  ],
  "roi_analysis": {
    "total_effort_hours": "总工作量（小时）",
    "estimated_monthly_savings": "预估月节省",
    "payback_period": "回收周期",
    "annual_roi": "年度 ROI"
  }
}
```

## ✅ 质量门禁

### 分析质量检查

- [ ] 性能数据样本充足（>100 次执行）
- [ ] 瓶颈识别准确
- [ ] 影响评估客观
- [ ] 建议具体可操作

### 优化效果检查

- [ ] 性能提升达到目标
- [ ] 无破坏性变更（如不允许）
- [ ] 优化可回滚
- [ ] 文档已更新

### 成本效益检查

- [ ] ROI 为正
- [ ] 回收周期<6 个月
- [ ] 长期收益>短期成本

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_INSUFFICIENT_DATA | 数据不足 | 性能数据样本太少 | 积累更多数据 |
| ERR_ANALYSIS_FAILED | 分析失败 | 指标异常或格式错误 | 检查数据格式 |
| ERR_OPTIMATION_INVALID | 优化无效 | 优化方案不可行 | 重新设计方案 |
| ERR_ROI_NEGATIVE | ROI 为负 | 成本高于收益 | 调整优化方案 |

### 异常处理流程

```
检测到异常
    ↓
分类异常类型（数据问题/分析问题/优化问题）
    ↓
可恢复？→ 是 → 尝试自动修复
    ↓           ↓
    否      成功？→ 是 → 继续优化
    ↓           ↓
记录异常    失败 → 回滚并上报
    ↓
生成异常报告
```

### 重试策略

- **最大重试次数**: 2 次
- **重试条件**: 临时故障、资源不足
- **重试间隔**: 3 秒

## 📚 最佳实践

### 推荐做法

- ✅ **数据驱动**：基于实际性能数据做决策
- ✅ **渐进优化**：小步快跑，持续改进
- ✅ **监控验证**：优化后验证效果
- ✅ **文档记录**：记录优化过程和结果
- ✅ **成本优先**：优先优化高成本技能
- ✅ **平衡质量**：不牺牲质量换取性能

### 避免做法

- ❌ **盲目优化**：没有数据支持的优化
- ❌ **过度优化**：优化到边际效益递减
- ❌ **忽视监控**：优化后不验证效果
- ❌ **破坏兼容**：未经同意的破坏性变更
- ❌ **单一指标**：只关注一个性能指标

### 优化原则

遵循性能优化原则：
- **测量优先**：先测量后优化
- **瓶颈优先**：优先解决关键瓶颈
- **简单优先**：优先选择简单的方案
- **验证必须**：优化后必须验证

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
OPTIMIZER_PATH=./optimizer
ENABLE_OPTIMIZATION=true

# 可选配置
DEFAULT_FOCUS=balanced
TARGET_IMPROVEMENT=30
MAX_EFFORT=medium
INCLUDE_BREAKING_CHANGES=false
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_performance_optimizer_config.yaml
skill_performance_optimizer:
  version: 1.0.0
  
  paths:
    reports: "./performance-reports"
    cache: "./optimizer-cache"
  
  analysis:
    min_sample_size: 100
    time_range_days: 7
    confidence_level: 0.95
  
  optimization:
    default_focus: "balanced"
    target_improvement_percent: 30
    max_effort: "medium"
    allow_breaking_changes: false
  
  cost_analysis:
    enabled: true
    token_cost_per_1k: 0.002
    execution_cost_per_sec: 0.0001
  
  caching:
    enabled: true
    ttl_hours: 24
    max_size_mb: 100
  
  reporting:
    auto_generate: true
    formats:
      - markdown
      - json
    include_roi: true
  
  logging:
    level: info
    file: "./logs/skill_performance_optimizer.log"
    max_size: "10MB"
    retention_days: 30
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的分析过程
- **INFO**: 关键步骤信息
- **WARN**: 优化警告
- **ERROR**: 优化失败

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 优化成功率 | 成功优化比例 | < 80% |
| 平均性能提升 | 平均改进幅度 | < 20% |
| ROI | 投资回报率 | < 0 |
| 优化覆盖率 | 已优化技能比例 | < 50% |

## 🧪 测试用例

### 单元测试

#### 测试用例 1：瓶颈检测

```yaml
输入:
  metrics:
    prompt_tokens: 2500
    avg_execution_time: 6000
    output_input_ratio: 0.25
预期输出:
  bottlenecks_count: 3
  types: ["prompt_too_long", "slow_execution", "low_token_efficiency"]
结果: ✅ 通过
```

#### 测试用例 2：优化建议生成

```yaml
输入:
  bottleneck:
    type: "prompt_too_long"
    severity: "high"
预期输出:
  suggestions_count: 1
  category: "prompt"
  priority: "high"
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整优化流程

**测试步骤**:
1. 收集性能数据
2. 分析瓶颈
3. 生成优化建议
4. 计算 ROI
5. 生成优化计划

**预期结果**: 
- 分析成功
- 建议合理
- ROI 为正

## 📖 示例

### 示例 1：提示词优化

**场景**: 优化过长的提示词

**执行命令**:
```bash
skill-performance-optimizer optimize --skill=CodeReviewer --focus=performance
```

**优化报告**:
```markdown
# 性能优化报告

## 当前性能
- 平均执行时间：8500ms
- P95 执行时间：12000ms
- 平均 token 消耗：3500
- 单次成本：$0.007

## 识别瓶颈
1. ⚠️ 提示词过长（2200 tokens）
2. ⚠️ 执行时间超过阈值

## 优化方案

### 优化 1：简化提示词
- **当前长度**: 2200 tokens
- **目标长度**: 1500 tokens
- **行动**:
  1. 移除冗余背景描述
  2. 精简示例从 5 个到 2 个
  3. 使用表格替代段落

- **预期收益**: 
  - 执行时间：-25%
  - token 消耗：-32%
  - 成本：-32%

### 优化 2：添加缓存
- **缓存策略**: 缓存重复代码模式的分析结果
- **预期命中率**: 60%
- **预期收益**:
  - 执行时间：-40%（缓存命中时）
  - token 消耗：-50%（缓存命中时）

## 总体预期
- 执行时间：8500ms → 4500ms (-47%)
- token 消耗：3500 → 2000 (-43%)
- 月度成本节省：$150
- ROI: 320%
```

## 🔗 相关资源

### 前置技能
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析
- [SkillOrchestrator](../SkillOrchestrator/SKILL.md) - 技能组合编排器

### 参考资料
- [性能优化最佳实践](链接)
- [Token 效率指南](链接)
- [成本优化策略](链接)

## ❓ FAQ

### Q1: 如何确定优化优先级？

**问题**: 有很多优化项，如何确定优先级？

**解答**: 
1. **按影响排序**: 优先优化影响最大的瓶颈
2. **按成本排序**: 优先优化成本最高的技能
3. **按难度排序**: 优先实施简单的优化
4. **综合评分**: 使用 RICE 评分法（Reach, Impact, Confidence, Effort）

### Q2: 优化后性能下降怎么办？

**问题**: 实施优化后性能反而下降。

**解答**: 
1. **立即回滚**: 恢复到优化前版本
2. **分析原因**: 找出性能下降的根本原因
3. **重新设计**: 基于分析重新设计优化方案
4. **小步测试**: 下次小步优化，逐步验证

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本 |
| 1.0.1 | 2026-03-31 | AI Assistant | 扩充性能优化策略引擎、输入输出规范等章节 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.1  
**状态**: 🟢 稳定

## 🔗 相关资源

### 前置技能
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析
- [SkillOrchestrator](../SkillOrchestrator/SKILL.md) - 技能组合编排器

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.0  
**状态**: 🟢 稳定
