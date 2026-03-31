---
name: 技能冲突检测与解决
identifier: SkillConflictResolver
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 冲突检测
  - 技能治理
  - 冲突解决
  - 元技能
  - 技能优化
---

# 技能冲突检测与解决

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能冲突检测与解决 |
| **英文标识名** | `SkillConflictResolver` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **技能冲突检测** 与 **解决** 的能力，使其能够：
1. 检测技能间的功能重叠和冲突
2. 识别技能命名冲突
3. 提供冲突解决方案
4. 技能合并和重构建议
5. 维护技能库的清晰边界

## 🎯 适用场景

- ✅ **新技能检查**：创建新技能前的冲突检查
- ✅ **技能库治理**：定期清理技能库冲突
- ✅ **技能合并**：合并功能重叠的技能
- ✅ **技能拆分**：拆分职责不清的技能
- ✅ **边界澄清**：明确技能职责边界
- ✅ **重构优化**：重构冲突技能

### 不适用场景
- ❌ 技能功能开发（应使用 development-engineer）
- ❌ 技能部署（应使用 SkillDeployment）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 核心组件

```
SkillConflictResolver (冲突解决核心)
├── ConflictDetector (冲突检测器)
│   ├── NamingConflictDetector (命名冲突检测)
│   ├── FunctionOverlapDetector (功能重叠检测)
│   └── DependencyConflictDetector (依赖冲突检测)
├── AnalysisEngine (分析引擎)
│   ├── SimilarityAnalyzer (相似度分析)
│   ├── ImpactAnalyzer (影响分析)
│   └── CostBenefitAnalyzer (成本效益分析)
├── ResolutionEngine (解决引擎)
│   ├── MergeSuggester (合并建议器)
│   ├── SplitSuggester (拆分建议器)
│   └── RefactorSuggester (重构建议器)
└── BoundaryDefiner (边界定义器)
    ├── ResponsibilityMapper (职责映射器)
    ├── InterfaceDefiner (接口定义器)
    └── ContractGenerator (契约生成器)
```

## 🔄 工作流程

```
技能扫描 → 冲突检测 → 影响分析 → 解决方案 → 执行解决 → 边界定义 → 验证
    ↓          ↓          ↓          ↓          ↓          ↓          ↓
[全量扫描] [识别冲突] [评估影响] [生成方案] [执行方案] [明确边界] [验证通过]
```

## ⚙️ 执行模式

### Mode A: 检测模式
- 扫描技能库
- 识别冲突
- 耗时：5-10 分钟

### Mode B: 分析模式
- 深度分析冲突
- 评估影响
- 耗时：10-20 分钟

### Mode C: 解决模式
- 执行解决方案
- 合并/拆分/重构
- 耗时：20-60 分钟

### Mode D: 预防模式
- 新技能冲突检查
- 预防冲突产生
- 耗时：2-5 分钟

## 👥 冲突解决策略引擎

### 相似度分析算法

```python
def calculate_skill_similarity(skill1, skill2):
    """
    计算技能相似度
    """
    # 名称相似度
    name_similarity = string_similarity(skill1.name, skill2.name)
    
    # 功能描述相似度
    desc_similarity = semantic_similarity(skill1.description, skill2.description)
    
    # 工具重叠度
    tools_overlap = len(set(skill1.tools) & set(skill2.tools)) / max(len(skill1.tools), len(skill2.tools))
    
    # 综合相似度
    overall_similarity = (
        name_similarity * 0.2 +
        desc_similarity * 0.5 +
        tools_overlap * 0.3
    )
    
    return {
        "name_similarity": name_similarity,
        "desc_similarity": desc_similarity,
        "tools_overlap": tools_overlap,
        "overall": overall_similarity,
        "conflict_level": "high" if overall_similarity > 0.7 else "medium" if overall_similarity > 0.4 else "low"
    }
```

### 解决方案生成规则

```python
def generate_resolution(conflict_analysis):
    """
    生成冲突解决方案
    """
    solutions = []
    
    if conflict_analysis['type'] == 'function_overlap':
        if conflict_analysis['overlap_percent'] > 70:
            solutions.append({
                "type": "merge",
                "title": "合并技能",
                "description": f"合并{conflict_analysis['skill1']}和{conflict_analysis['skill2']}",
                "effort": "high",
                "benefit": "消除重复，降低维护成本",
                "risk": "需要更新所有引用"
            })
        elif conflict_analysis['overlap_percent'] > 40:
            solutions.append({
                "type": "boundary_clarification",
                "title": "明确边界",
                "description": "更新文档明确职责边界",
                "effort": "low",
                "benefit": "减少用户困惑",
                "risk": "低"
            })
    
    elif conflict_analysis['type'] == 'naming_conflict':
        solutions.append({
            "type": "rename",
            "title": "重命名技能",
            "description": f"将{conflict_analysis['skill2']}重命名为更具体的名称",
            "effort": "medium",
            "benefit": "消除命名混淆",
            "risk": "需要更新引用"
        })
    
    return solutions
```

## 📋 输入输出规范

### 输入格式

```json
{
  "scope": "类型：string，说明：检测范围（all/new_skill）",
  "new_skill": "类型：object，说明：新技能定义（仅新技能检查）",
  "config": {
    "type": "object",
    "description": "配置选项",
    "properties": {
      "similarity_threshold": "类型：number，说明：相似度阈值",
      "auto_resolve": "类型：boolean，说明：是否自动解决"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "conflicts_found": "发现冲突数",
  "conflicts": [
    {
      "id": "冲突 ID",
      "type": "冲突类型",
      "skills": ["技能 1", "技能 2"],
      "similarity": "相似度",
      "severity": "严重程度",
      "solutions": ["解决方案"]
    }
  ],
  "resolution_plan": {
    "total_conflicts": "总冲突数",
    "resolved": "已解决",
    "pending": "待解决"
  }
}
```

## ✅ 质量门禁

### 检测质量检查

- [ ] 扫描覆盖率 100%
- [ ] 冲突识别准确率>90%
- [ ] 误报率<5%

### 解决质量检查

- [ ] 解决方案可行
- [ ] 无破坏性变更（如不允许）
- [ ] 文档已更新

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_SCAN_FAILED | 扫描失败 | 技能库无法访问 | 检查路径和权限 |
| ERR_ANALYSIS_FAILED | 分析失败 | 技能定义不完整 | 补充技能定义 |
| ERR_RESOLUTION_FAILED | 解决失败 | 方案不可行 | 重新设计方案 |

## 📚 最佳实践

### 推荐做法

- ✅ **预防为主**: 新技能创建前检查冲突
- ✅ **定期审查**: 每月扫描技能库
- ✅ **渐进解决**: 优先解决高优先级冲突
- ✅ **文档更新**: 解决后更新相关文档

### 避免做法

- ❌ **忽视冲突**: 不要忽视命名和功能冲突
- ❌ **粗暴合并**: 不要不经分析就合并
- ❌ **破坏引用**: 避免破坏现有引用

## 🔧 配置选项

```yaml
skill_conflict_resolver:
  version: 1.0.0
  
  detection:
    similarity_threshold: 0.6
    scan_interval_days: 30
  
  resolution:
    auto_resolve_low_priority: false
    require_approval: true
  
  logging:
    level: info
    file: "./logs/skill_conflict_resolver.log"
```

## 📖 示例

### 完整冲突检测与解决

**场景**: 定期技能库冲突审查

**执行命令**:
```bash
skill-conflict-resolver detect --scope=all
```

**检测报告**:
```markdown
# 冲突检测报告

## 检测范围
- 扫描技能：50 个
- 检测时间：2026-03-31

## 发现的冲突

### 高优先级（2 个）

**冲突 1**: CodeAnalyzer vs CodeReviewer
- 相似度：85%
- 类型：功能重叠
- 建议：合并

**冲突 2**: APIHelper vs APIClient
- 相似度：92%
- 类型：命名冲突
- 建议：重命名

### 中优先级（3 个）
- 略...

## 解决计划
1. 合并 CodeAnalyzer 和 CodeReviewer（预计 2 天）
2. 重命名 APIHelper 为 APIUtility（预计 1 天）
```

## 🔗 相关资源

### 前置技能
- [SkillEvolution](../SkillEvolution/SKILL.md) - 技能进化与关联
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁

### 参考资料
- [技能治理最佳实践](链接)
- [冲突解决策略](链接)

## ❓ FAQ

### Q1: 如何处理功能重叠？

**解答**: 
1. 评估重叠程度
2. >70% 建议合并
3. 40-70% 明确边界
4. <40% 可以接受

### Q2: 合并技能的步骤？

**解答**:
1. 创建新技能
2. 合并功能
3. 更新引用
4. 废弃旧技能
5. 验证功能

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本 |
| 1.0.1 | 2026-03-31 | AI Assistant | 扩充冲突解决策略引擎等章节 |

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
- [SkillEvolution](../SkillEvolution/SKILL.md) - 技能进化与关联
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁

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
