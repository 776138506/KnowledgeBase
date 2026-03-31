---
name: 技能质量门禁
identifier: SkillQualityGate
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 技能质量
  - 质量门禁
  - 技能审查
  - 元技能
  - 质量保障
---

# 技能质量门禁

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能质量门禁 |
| **英文标识名** | `SkillQualityGate` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **技能质量审查** 与 **门禁控制** 的能力，使其能够：
1. 定义技能质量标准和检查清单
2. 执行技能发布前的质量门禁检查
3. 定期审查技能质量并生成评分
4. 识别质量问题并预警
5. 阻止低质量技能发布或更新

## 🎯 适用场景

- ✅ **技能发布审批**：新技能发布前的质量检查
- ✅ **版本更新审查**：技能更新前的质量验证
- ✅ **定期质量审查**：定期评估技能库整体质量
- ✅ **质量问题诊断**：识别技能质量问题和根因
- ✅ **质量评分**：为技能生成质量评分
- ✅ **质量预警**：识别质量下降趋势并预警

### 不适用场景
- ❌ 技能开发阶段（应使用 MetaCognitiveSelfExpansion）
- ❌ 技能性能优化（应使用 SkillPerformanceOptimizer）
- ❌ 技能测试验证（应使用 SkillTesting）

## 🏗️ 技能架构

### 架构图

```
SkillQualityGate (质量门禁核心)
├── StandardDefiner (标准定义器)
│   ├── QualityCriteria (质量标准)
│   ├── ChecklistGenerator (检查清单生成)
│   └── ThresholdManager (阈值管理)
├── QualityInspector (质量检查器)
│   ├── FormatChecker (格式检查器)
│   ├── ContentReviewer (内容审查器)
│   └── ComplianceValidator (合规验证器)
├── ScoreCalculator (评分计算器)
│   ├── MetricCollector (指标收集器)
│   ├── ScoreEngine (评分引擎)
│   └── RankGenerator (排名生成器)
└── GateKeeper (门禁守卫)
    ├── PreDeployCheck (部署前检查)
    ├── QualityGate (质量关卡)
    └── ApprovalManager (审批管理)
```

### 组件说明

| 组件名称 | 角色 | 职责 | 工具 |
|---------|------|------|------|
| StandardDefiner | 标准定义器 | 定义质量标准、生成检查清单、管理阈值 | 规则引擎、模板系统 |
| QualityInspector | 质量检查器 | 检查格式、审查内容、验证合规性 | 静态分析、规则检查 |
| ScoreCalculator | 评分计算器 | 收集指标、计算评分、生成排名 | 统计算法、评分模型 |
| GateKeeper | 门禁守卫 | 部署前检查、质量关卡控制、审批管理 | 审批流程、门禁系统 |

## 🔄 工作流程

### 主工作流程

```
标准定义 → 质量检查 → 评分计算 → 门禁决策 → 问题反馈 → 改进追踪 → 质量报告
    ↓          ↓          ↓          ↓          ↓          ↓          ↓
[质量标准] [全面检查] [综合评分] [通过/拒绝] [问题清单] [改进计划] [质量报告]
```

### 详细步骤

#### 步骤 1：质量标准定义

**目标**: 定义技能质量标准和检查清单

**处理过程**:
1. **定义质量维度**：
   - 完整性（必需章节、元数据等）
   - 准确性（内容正确、示例可运行等）
   - 一致性（格式统一、命名规范等）
   - 可维护性（结构清晰、文档完整等）

2. **生成检查清单**：
   - 格式检查清单
   - 内容质量清单
   - 合规性清单
   - 最佳实践清单

3. **设置阈值**：
   - 最低通过分数（如 60 分）
   - 警告阈值（如 70 分）
   - 优秀阈值（如 90 分）

**输出**: 
- 质量标准文档
- 检查清单
- 阈值配置

#### 步骤 2：质量检查

**目标**: 全面检查技能质量

**处理过程**:
1. **格式检查**：
   - SKILL.md 文件格式
   - Frontmatter 元数据
   - 目录结构
   - 命名规范

2. **内容审查**：
   - 必需章节完整性
   - 示例代码正确性
   - 文档清晰度
   - 最佳实践遵循

3. **合规验证**：
   - 技能规范遵循
   - 安全合规
   - 依赖合规
   - 许可证合规

**输出**: 
- 格式检查报告
- 内容审查报告
- 合规验证报告

#### 步骤 3：评分计算

**目标**: 计算技能综合质量评分

**处理过程**:
1. **收集指标**：
   - 完整性得分（0-30 分）
   - 准确性得分（0-30 分）
   - 一致性得分（0-20 分）
   - 可维护性得分（0-20 分）

2. **计算综合评分**：
   - 加权平均计算
   - 应用惩罚项（严重问题扣分）
   - 应用奖励项（优秀实践加分）

3. **生成评级**：
   - A 级（90-100 分）：优秀
   - B 级（80-89 分）：良好
   - C 级（70-79 分）：合格
   - D 级（60-69 分）：需改进
   - F 级（<60 分）：不合格

**输出**: 
- 质量评分
- 评级
- 得分详情

#### 步骤 4：门禁决策

**目标**: 基于质量评分做出门禁决策

**处理过程**:
1. **应用门禁规则**：
   - 评分>=60：通过
   - 评分<60：拒绝
   - 有严重问题：拒绝

2. **生成决策报告**：
   - 通过/拒绝决定
   - 决策依据
   - 改进建议

3. **审批流程**（如需要）：
   - 提交审批
   - 等待批准
   - 记录审批结果

**输出**: 
- 门禁决策
- 决策报告
- 审批记录

## 👥 质量评估策略引擎

### 质量评分规则

```python
def calculate_quality_score(skill_analysis):
    """
    计算技能质量评分（0-100）
    """
    # 完整性得分（0-30 分）
    completeness = skill_analysis.required_sections_present / skill_analysis.total_required_sections
    completeness_score = 30 * completeness
    
    # 准确性得分（0-30 分）
    accuracy = skill_analysis.correct_examples / skill_analysis.total_examples
    accuracy_score = 30 * accuracy
    
    # 一致性得分（0-20 分）
    consistency = skill_analysis.format_compliance_rate
    consistency_score = 20 * consistency
    
    # 可维护性得分（0-20 分）
    maintainability = skill_analysis.documentation_quality
    maintainability_score = 20 * maintainability
    
    # 惩罚项
    penalties = 0
    if skill_analysis.has_security_issues:
        penalties += 10
    if skill_analysis.has_broken_links:
        penalties += 5
    
    total_score = completeness_score + accuracy_score + consistency_score + maintainability_score - penalties
    return max(0, min(100, round(total_score, 2)))
```

### 门禁决策规则

```python
def make_gate_decision(quality_score, quality_report):
    """
    基于质量评分做出门禁决策
    """
    if quality_score >= 90:
        return "APPROVED", "优秀技能，直接通过"
    elif quality_score >= 80:
        return "APPROVED", "良好技能，通过"
    elif quality_score >= 70:
        return "APPROVED_WITH_SUGGESTIONS", "合格技能，建议改进"
    elif quality_score >= 60:
        return "CONDITIONAL_APPROVAL", "需改进后通过", generate_improvement_plan()
    else:
        return "REJECTED", "质量不达标，拒绝", generate_improvement_plan()
```

### 质量问题检测规则

```python
def detect_quality_issues(skill_content):
    """
    检测技能质量问题
    """
    issues = []
    
    # 严重问题
    if not skill_content.has_frontmatter:
        issues.append({"severity": "critical", "type": "format", "message": "缺少 Frontmatter 元数据"})
    
    if not skill_content.has_required_sections:
        issues.append({"severity": "critical", "type": "completeness", "message": "缺少必需章节"})
    
    # 警告问题
    if skill_content.has_broken_examples:
        issues.append({"severity": "warning", "type": "accuracy", "message": "示例代码不可运行"})
    
    if skill_content.has_outdated_content:
        issues.append({"severity": "warning", "type": "accuracy", "message": "内容过时"})
    
    # 建议问题
    if len(skill_content.examples) < 2:
        issues.append({"severity": "suggestion", "type": "completeness", "message": "示例过少，建议增加"})
    
    return issues
```

## ⚙️ 执行模式

### Mode A: 发布审查模式（Pre-Release Review）

- **描述**: 技能发布前的质量审查
- **包含阶段**: 质量检查 → 评分计算 → 门禁决策 → 审批
- **使用场景**: 新技能发布、技能版本更新
- **预计耗时**: 中等（5-15 分钟）
- **输出**: 发布审查报告

### Mode B: 定期审查模式（Periodic Review）

- **描述**: 定期审查技能库整体质量
- **包含阶段**: 全量检查 → 评分排名 → 趋势分析 → 质量报告
- **使用场景**: 每周/每月质量审查
- **预计耗时**: 长（15-30 分钟）
- **输出**: 质量审查报告

### Mode C: 诊断模式（Diagnostic Mode）

- **描述**: 诊断特定技能的质量问题
- **包含阶段**: 深度检查 → 问题识别 → 根因分析 → 改进建议
- **使用场景**: 技能质量下降、用户投诉
- **预计耗时**: 中等（10-20 分钟）
- **输出**: 诊断报告和改进计划

### Mode D: 监控模式（Monitoring Mode）

- **描述**: 持续监控技能质量
- **包含阶段**: 实时检查 → 质量预警 → 趋势追踪
- **使用场景**: 7x24 小时质量监控
- **预计耗时**: 持续运行
- **输出**: 质量告警和趋势报告

## 🚀 快速开始

### 前置条件

- [ ] 技能质量标准已定义
- [ ] 检查清单已准备
- [ ] 有技能文件读取权限

### 基本用法

```bash
# 模式 1：发布审查
skill-quality-gate review --skill=SkillName --mode=pre-release

# 模式 2：定期审查
skill-quality-gate audit --period=monthly

# 模式 3：质量诊断
skill-quality-gate diagnose --skill=SkillName

# 模式 4：质量监控
skill-quality-gate monitor --real-time=true
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `--mode` | string | 否 | "pre-release" | 审查模式 |
| `--skill` | string | 否 | "all" | 目标技能 |
| `--period` | string | 否 | "monthly" | 审查周期 |
| `--threshold` | number | 否 | 60 | 最低通过分数 |

## ✅ 质量门禁标准

### 必需检查项（Critical）

- [ ] SKILL.md 文件格式正确
- [ ] Frontmatter 元数据完整
- [ ] identifier 与文件夹名一致
- [ ] 包含必需章节（适用场景、工作流程、示例）
- [ ] 无安全漏洞
- [ ] 无版权风险

### 重要检查项（Important）

- [ ] 示例代码可运行
- [ ] 文档清晰易懂
- [ ] 遵循最佳实践
- [ ] 依赖声明完整
- [ ] 版本信息正确

### 建议检查项（Optional）

- [ ] 包含多个使用示例
- [ ] 有性能优化建议
- [ ] 有故障排除指南
- [ ] 有相关资源链接
- [ ] 有更新日志

## 📊 质量评分标准

### 评分维度

| 维度 | 权重 | 检查项 |
|------|------|--------|
| 完整性 | 30% | 必需章节、元数据、示例数量 |
| 准确性 | 30% | 内容正确、示例可运行、无错误 |
| 一致性 | 20% | 格式统一、命名规范、风格一致 |
| 可维护性 | 20% | 结构清晰、文档完整、易于理解 |

### 评级标准

| 评级 | 分数范围 | 说明 |
|------|---------|------|
| A（优秀） | 90-100 | 远超标准，可作为模板 |
| B（良好） | 80-89 | 超出标准，质量可靠 |
| C（合格） | 70-79 | 符合标准，可接受 |
| D（需改进） | 60-69 | 接近标准，需改进 |
| F（不合格） | <60 | 未达标准，拒绝 |

## 📖 示例

### 示例 1：技能发布审查

**场景**: 新技能发布前的质量审查

**执行命令**:
```bash
skill-quality-gate review --skill=NewSkill --mode=pre-release
```

**输出报告**:
```markdown
# 技能质量审查报告

## 技能信息
- 名称：NewSkill
- 版本：1.0.0
- 审查时间：2026-03-31

## 质量评分
- **总分**: 85/100 (B 级 - 良好)
- 完整性：27/30
- 准确性：28/30
- 一致性：18/20
- 可维护性：12/20

## 检查结果

### ✅ 通过项（15 项）
- SKILL.md 格式正确
- Frontmatter 元数据完整
- 必需章节完整
- 示例代码可运行
- 遵循最佳实践

### ⚠️ 警告项（2 项）
- 示例数量较少（仅 1 个，建议 3 个+）
- 缺少性能优化建议

### ❌ 问题项（0 项）
- 无

## 门禁决策
**结果**: ✅ 通过
**理由**: 技能质量良好，符合发布标准
**建议**: 增加更多使用示例

## 下一步
技能可以发布。建议在下一个版本中增加更多示例。
```

## 🔗 相关资源

### 前置技能
- [SkillEvolution](../SkillEvolution/SKILL.md) - 技能进化与关联
- [SkillDeployment](../SkillDeployment/SKILL.md) - 技能部署与发布

### 后续技能
- [SkillTesting](../SkillTesting/SKILL.md) - 技能测试与验证
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析

### 参考资料
- [技能质量标准](链接)
- [质量门禁最佳实践](链接)
- [代码审查指南](链接)

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的技能质量门禁能力 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.0  
**状态**: 🟢 稳定
