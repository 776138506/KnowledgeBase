---
name: 技能度量与分析
identifier: SkillMetrics
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 技能度量
  - 数据分析
  - 性能监控
  - 元技能
  - 技能优化
---

# 技能度量与分析

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能度量与分析 |
| **英文标识名** | `SkillMetrics` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **数据驱动的技能度量** 与 **分析优化** 的能力，使其能够：
1. 追踪技能使用指标（使用次数、成功率、耗时、token 消耗等）
2. 分析技能性能和用户满意度
3. 生成技能健康报告和趋势分析
4. 基于数据驱动提供技能优化建议
5. 识别低价值技能和问题技能

## 🎯 适用场景

- ✅ **技能监控**：实时监控技能使用情况
- ✅ **性能分析**：识别性能瓶颈和高成本技能
- ✅ **价值评估**：评估技能的价值和 ROI
- ✅ **趋势分析**：分析技能使用趋势和模式
- ✅ **问题诊断**：诊断技能失败和异常
- ✅ **优化建议**：基于数据提供优化建议

### 不适用场景
- ❌ 技能开发阶段（应使用 MetaCognitiveSelfExpansion）
- ❌ 技能部署发布（应使用 SkillDeployment）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 架构图

```
SkillMetrics (度量核心)
├── DataCollector (数据收集器)
│   ├── UsageTracker (使用追踪器)
│   ├── PerformanceMonitor (性能监控器)
│   └── ErrorLogger (错误日志器)
├── MetricsAnalyzer (指标分析器)
│   ├── TrendAnalyzer (趋势分析器)
│   ├── PatternRecognizer (模式识别器)
│   └── AnomalyDetector (异常检测器)
├── ReportGenerator (报告生成器)
│   ├── HealthReport (健康报告)
│   ├── PerformanceReport (性能报告)
│   └── SuggestionEngine (建议引擎)
└── DashboardBuilder (仪表板构建器)
    ├── MetricsVisualization (指标可视化)
    ├── AlertManager (告警管理)
    └── InsightGenerator (洞察生成器)
```

### 组件说明

| 组件名称 | 角色 | 职责 | 工具 |
|---------|------|------|------|
| DataCollector | 数据收集器 | 收集使用数据、性能指标、错误日志 | 日志收集、指标采集 |
| MetricsAnalyzer | 指标分析器 | 分析趋势、识别模式、检测异常 | 统计分析、机器学习 |
| ReportGenerator | 报告生成器 | 生成健康报告、性能报告、优化建议 | 报告模板、数据分析 |
| DashboardBuilder | 仪表板构建器 | 可视化指标、管理告警、生成洞察 | 图表库、告警系统 |

## 🔄 工作流程

### 主工作流程

```
数据收集 → 指标计算 → 趋势分析 → 异常检测 → 报告生成 → 可视化展示 → 优化建议 → 持续监控
    ↓          ↓          ↓          ↓          ↓          ↓          ↓          ↓
[完整数据] [KPI 计算] [趋势识别] [问题检测] [健康报告] [仪表板] [优化建议] [实时监控]
```

### 详细步骤

#### 步骤 1：数据收集

**目标**: 全面收集技能使用数据

**输入**: 
- 技能执行日志
- 性能指标
- 用户反馈

**处理过程**:
1. **使用数据收集**：
   - 记录每次技能调用
   - 统计使用频率和分布
   - 追踪用户满意度

2. **性能数据收集**：
   - 记录执行耗时
   - 统计 token 消耗
   - 监控资源使用

3. **错误数据收集**：
   - 记录失败和异常
   - 分类错误类型
   - 追踪错误频率

**输出**: 
- 原始使用数据
- 性能指标数据
- 错误日志数据

**质量标准**:
- [ ] 数据收集完整率>98%
- [ ] 数据准确率>99%
- [ ] 实时性<1 分钟延迟

#### 步骤 2：指标计算

**目标**: 计算关键性能指标（KPI）

**输入**: 原始数据

**处理过程**:
1. **使用指标**：
   - 总调用次数
   - 日均/周均/月均调用次数
   - 使用频率趋势
   - 用户覆盖率

2. **性能指标**：
   - 平均执行时间
   - P95/P99 执行时间
   - 平均 token 消耗
   - 成功率

3. **价值指标**：
   - 技能价值评分（0-100）
   - ROI（投入产出比）
   - 用户满意度评分
   - 业务影响力

**输出**: 
- KPI 指标列表
- 指标趋势数据
- 对比分析结果

**质量标准**:
- [ ] 指标计算准确
- [ ] 趋势分析合理
- [ ] 对比维度全面

#### 步骤 3：趋势分析与异常检测

**目标**: 识别使用趋势和异常情况

**输入**: KPI 指标数据

**处理过程**:
1. **趋势分析**：
   - 识别上升/下降趋势
   - 检测周期性模式
   - 预测未来趋势

2. **异常检测**：
   - 检测使用量突增/突降
   - 识别性能异常
   - 发现错误率异常

3. **模式识别**：
   - 识别使用高峰时段
   - 发现技能组合模式
   - 识别用户行为模式

**输出**: 
- 趋势分析报告
- 异常检测结果
- 模式识别报告

**质量标准**:
- [ ] 趋势识别准确率>90%
- [ ] 异常检测召回率>85%
- [ ] 模式识别有意义

#### 步骤 4：报告生成与可视化

**目标**: 生成直观的报告和仪表板

**输入**: 分析结果

**处理过程**:
1. **健康报告**：
   - 技能整体健康度
   - 关键指标概览
   - 问题和风险

2. **性能报告**：
   - 性能指标详情
   - 瓶颈分析
   - 优化建议

3. **可视化仪表板**：
   - 指标趋势图
   - 技能对比图
   - 热力图和分布图

**输出**: 
- 技能健康报告
- 性能分析报告
- 可视化仪表板

**质量标准**:
- [ ] 报告清晰易懂
- [ ] 可视化直观
- [ ] 建议具体可操作

## 👥 分析策略引擎

### 技能价值评分规则

```python
def calculate_skill_value_score(skill_metrics):
    """
    计算技能价值评分（0-100）
    """
    # 使用频率得分（0-40 分）
    usage_score = min(40, skill_metrics.usage_frequency * 10)
    
    # 性能得分（0-30 分）
    performance_score = 30 * (1 / (1 + skill_metrics.avg_execution_time / 1000))
    
    # 成功率得分（0-20 分）
    success_score = 20 * skill_metrics.success_rate
    
    # 用户满意度得分（0-10 分）
    satisfaction_score = 10 * skill_metrics.user_satisfaction
    
    total_score = usage_score + performance_score + success_score + satisfaction_score
    return round(total_score, 2)
```

### 异常检测规则

```python
def detect_anomalies(metrics_history, current_metrics):
    """
    检测指标异常
    """
    anomalies = []
    
    # 使用量异常检测
    usage_change = (current_metrics.usage - metrics_history.avg_usage) / metrics_history.std_usage
    if abs(usage_change) > 3:  # 超过 3 个标准差
        anomalies.append({
            "type": "usage_anomaly",
            "severity": "high" if abs(usage_change) > 5 else "medium",
            "message": f"使用量异常：变化{usage_change:.2f}个标准差"
        })
    
    # 性能异常检测
    if current_metrics.avg_time > metrics_history.p95_time * 1.5:
        anomalies.append({
            "type": "performance_anomaly",
            "severity": "high",
            "message": f"性能下降：平均时间{current_metrics.avg_time}ms 远超 P95"
        })
    
    # 错误率异常检测
    if current_metrics.error_rate > metrics_history.avg_error_rate * 2:
        anomalies.append({
            "type": "error_rate_anomaly",
            "severity": "critical",
            "message": f"错误率飙升：{current_metrics.error_rate*100:.2f}%"
        })
    
    return anomalies
```

### 优化建议生成规则

```python
def generate_optimization_suggestions(skill_analysis):
    """
    生成技能优化建议
    """
    suggestions = []
    
    # 性能优化建议
    if skill_analysis.avg_execution_time > 5000:  # >5 秒
        suggestions.append({
            "type": "performance",
            "priority": "high",
            "suggestion": "优化提示词，减少不必要的步骤",
            "expected_improvement": "执行时间减少 30-50%"
        })
    
    # 成本优化建议
    if skill_analysis.avg_token_cost > 1000:
        suggestions.append({
            "type": "cost",
            "priority": "medium",
            "suggestion": "简化输出格式，减少 token 消耗",
            "expected_improvement": "token 消耗减少 20-40%"
        })
    
    # 质量优化建议
    if skill_analysis.success_rate < 0.9:
        suggestions.append({
            "type": "quality",
            "priority": "high",
            "suggestion": "增强错误处理，添加重试机制",
            "expected_improvement": "成功率提升到 95%+"
        })
    
    # 使用频率优化建议
    if skill_analysis.usage_frequency < 0.5:
        suggestions.append({
            "type": "adoption",
            "priority": "medium",
            "suggestion": "改进技能文档，增加使用示例",
            "expected_improvement": "使用频率提升 2-3 倍"
        })
    
    return suggestions
```

## ⚙️ 执行模式

### Mode A: 监控模式（Monitoring Mode）

- **描述**: 实时监控技能指标
- **包含阶段**: 数据收集 → 指标计算 → 异常检测 → 告警
- **使用场景**: 7x24 小时技能监控
- **预计耗时**: 持续运行
- **输出**: 实时指标和告警

### Mode B: 分析模式（Analysis Mode）

- **描述**: 深度分析技能表现
- **包含阶段**: 数据收集 → 趋势分析 → 模式识别 → 报告生成
- **使用场景**: 定期技能审查
- **预计耗时**: 中等（5-15 分钟）
- **输出**: 深度分析报告

### Mode C: 诊断模式（Diagnostic Mode）

- **描述**: 诊断技能问题和异常
- **包含阶段**: 数据收集 → 异常检测 → 根因分析 → 解决建议
- **使用场景**: 技能失败或性能下降
- **预计耗时**: 中等（5-10 分钟）
- **输出**: 诊断报告和建议

### Mode D: 优化模式（Optimization Mode）

- **描述**: 基于数据提供优化建议
- **包含阶段**: 数据分析 → 瓶颈识别 → 建议生成 → 优先级排序
- **使用场景**: 技能性能优化
- **预计耗时**: 中等（10-20 分钟）
- **输出**: 优化建议列表

## 🚀 快速开始

### 前置条件

- [ ] 技能使用日志已启用
- [ ] 有历史数据积累（建议>7 天）
- [ ] 有数据读取权限

### 基本用法

```bash
# 模式 1：监控模式
skill-metrics monitor --real-time=true

# 模式 2：分析模式
skill-metrics analyze --period=last_7_days

# 模式 3：诊断模式
skill-metrics diagnose --skill=SkillName

# 模式 4：优化模式
skill-metrics optimize --skill=SkillName --focus=performance
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `--mode` | string | 否 | "analyze" | 执行模式 |
| `--skill` | string | 否 | "all" | 目标技能 |
| `--period` | string | 否 | "last_7_days" | 分析周期 |
| `--focus` | string | 否 | "all" | 优化重点（performance/cost/quality） |
| `--real-time` | boolean | 否 | false | 是否实时监控 |

## 📋 输入输出规范

### 输入格式

```json
{
  "mode": "类型：string，说明：执行模式",
  "skill_identifier": "类型：string，说明：技能标识名",
  "time_range": {
    "type": "object",
    "description": "时间范围",
    "properties": {
      "start": "类型：string，说明：开始时间",
      "end": "类型：string，说明：结束时间"
    }
  },
  "metrics_config": {
    "type": "object",
    "description": "指标配置",
    "properties": {
      "include_usage": "类型：boolean，说明：包含使用数据",
      "include_performance": "类型：boolean，说明：包含性能数据",
      "include_errors": "类型：boolean，说明：包含错误数据"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "metrics_report": {
    "total_skills": "技能总数",
    "healthy_skills": "健康技能数",
    "warning_skills": "警告技能数",
    "critical_skills": "严重问题技能数"
  },
  "skill_details": [
    {
      "identifier": "技能标识名",
      "usage_metrics": {
        "total_calls": "总调用次数",
        "avg_daily_calls": "日均调用",
        "trend": "趋势（上升/下降/稳定）"
      },
      "performance_metrics": {
        "avg_execution_time": "平均执行时间 (ms)",
        "p95_execution_time": "P95 执行时间 (ms)",
        "success_rate": "成功率",
        "avg_token_cost": "平均 token 消耗"
      },
      "value_score": "价值评分 (0-100)",
      "health_status": "健康状态（healthy/warning/critical）"
    }
  ],
  "suggestions": [
    {
      "skill": "技能标识名",
      "type": "类型（performance/cost/quality/adoption）",
      "priority": "优先级（high/medium/low）",
      "suggestion": "优化建议",
      "expected_improvement": "预期改进"
    }
  ]
}
```

## ✅ 质量门禁

### 检查清单

#### 数据质量检查
- [ ] 数据收集完整率>98%
- [ ] 数据准确率>99%
- [ ] 数据及时性<1 分钟延迟

#### 分析质量检查
- [ ] 指标计算准确率 100%
- [ ] 趋势识别准确率>90%
- [ ] 异常检测召回率>85%

#### 报告质量检查
- [ ] 报告清晰易懂
- [ ] 建议具体可操作
- [ ] 可视化直观

### 验收标准

- [ ] 能正确识别低频技能（使用频率<0.5 次/周）
- [ ] 能准确检测性能异常（>3 个标准差）
- [ ] 价值评分客观合理
- [ ] 优化建议具体可行
- [ ] 报告生成及时

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_NO_DATA | 无可用数据 | 日志未启用或数据丢失 | 检查日志配置 |
| ERR_CALCULATION_FAILED | 指标计算失败 | 数据格式错误 | 验证数据格式 |
| ERR_ANOMALY_UNDETECTED | 异常检测失败 | 历史数据不足 | 积累更多数据 |
| ERR_REPORT_GENERATION_FAILED | 报告生成失败 | 模板错误或数据异常 | 检查模板和数据 |

## 📚 最佳实践

### 推荐做法

- ✅ **持续监控**：7x24 小时不间断监控
- ✅ **定期分析**：每周/每月深度分析
- ✅ **数据驱动**：基于数据做决策
- ✅ **及时告警**：异常及时通知
- ✅ **持续优化**：根据建议持续改进

### 避免做法

- ❌ **忽视数据**：不要凭感觉做决策
- ❌ **过度监控**：避免过多指标造成干扰
- ❌ **延迟响应**：不要忽视告警
- ❌ **数据孤岛**：确保数据完整性

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
METRICS_DATA_PATH=./logs/metrics
ENABLE_METRICS=true

# 可选配置
MONITORING_INTERVAL=60  # 秒
ALERT_THRESHOLD=0.8
RETENTION_DAYS=90
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_metrics_config.yaml
skill_metrics:
  version: 1.0.0
  
  data_collection:
    enabled: true
    interval_seconds: 60
    retention_days: 90
  
  metrics:
    usage:
      enabled: true
      include_frequency: true
      include_trends: true
    performance:
      enabled: true
      include_execution_time: true
      include_token_cost: true
    quality:
      enabled: true
      include_success_rate: true
      include_user_satisfaction: true
  
  analysis:
    trend_detection: true
    anomaly_detection: true
    pattern_recognition: true
  
  alerting:
    enabled: true
    channels:
      - email
      - slack
    thresholds:
      error_rate: 0.05
      execution_time_ms: 10000
      usage_drop_percent: 50
  
  reporting:
    schedule: "weekly"
    formats:
      - markdown
      - json
    recipients:
      - team@example.com
  
  logging:
    level: info
    file: "./logs/skill_metrics.log"
```

## 📊 监控与日志

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 技能健康度 | 健康技能占比 | < 70% |
| 平均成功率 | 所有技能平均成功率 | < 90% |
| 平均执行时间 | 所有技能平均耗时 | > 5000ms |
| 错误率 | 错误调用占比 | > 5% |
| 低价值技能数 | 价值评分<30 的技能数 | > 5 |

## 🧪 测试用例

### 单元测试

#### 测试用例 1：价值评分计算

```yaml
输入:
  skill_metrics:
    usage_frequency: 5.2
    avg_execution_time: 2000
    success_rate: 0.95
    user_satisfaction: 0.9
预期输出:
  value_score: 78.5
  health_status: "healthy"
结果: ✅ 通过
```

#### 测试用例 2：异常检测

```yaml
输入:
  history:
    avg_usage: 100
    std_usage: 10
  current:
    usage: 50
预期输出:
  anomaly_detected: true
  severity: "high"
  message: "使用量下降 5 个标准差"
结果: ✅ 通过
```

## 📖 示例

### 示例 1：生成技能健康报告

**场景**: 每周技能健康检查

**执行命令**:
```bash
skill-metrics analyze --period=last_7_days --output=markdown
```

**输出报告**:
```markdown
# 技能健康报告 - 2026 年第 14 周

## 概览
- 技能总数：30
- 健康技能：22 (73%)
- 警告技能：6 (20%)
- 严重问题：2 (7%)

## Top 5 高价值技能
1. CodeReviewer - 95 分 (使用频率：15 次/天)
2. DocumentationEngineer - 92 分 (使用频率：12 次/天)
3. QualityValidator - 88 分 (使用频率：10 次/天)

## 需要关注的技能

### 1. OldComponent (价值评分：22 分) ⚠️
- 使用频率：0.2 次/天 (下降 80%)
- 成功率：85% (低于平均)
- 建议：考虑归档或重构

### 2. SlowAnalyzer (价值评分：35 分) ⚠️
- 平均执行时间：12000ms (远超平均 3000ms)
- token 消耗：5000 (高于平均 1000)
- 建议：优化性能

## 优化建议
1. 归档 3 个低价值技能
2. 优化 2 个高成本技能
3. 更新 5 个文档不完整的技能
```

## 🔗 相关资源

### 前置技能
- [SkillEvolution](../SkillEvolution/SKILL.md) - 技能进化与关联
- [SkillDeployment](../SkillDeployment/SKILL.md) - 技能部署与发布

### 后续技能
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁
- [SkillPerformanceOptimizer](../SkillPerformanceOptimizer/SKILL.md) - 技能性能优化器

### 参考资料
- [数据驱动决策](链接)
- [技能度量标准](链接)
- [性能分析最佳实践](链接)

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的技能度量与分析能力 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.0  
**状态**: 🟢 稳定
