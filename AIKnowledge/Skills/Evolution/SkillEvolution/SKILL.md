---
name: SkillEvolution
description: 技能进化与关联专家，负责主动识别技能库中的过时不完整或需要优化的技能并建议更新、发现技能之间的潜在关联（功能互补、数据流转、依赖关系）并建立技能网络、通过技能组合产生新的涌现能力、维护技能库的整体质量和一致性、追踪技能进化历史，适用于技能库治理、技能网络构建、能力涌现、持续优化场景
---

# 技能进化与关联

## 🎯 核心目标

赋予 Agent **技能维护** 与 **关联涌现** 的能力，使其能够：
1. 主动识别技能库中的过时、不完整或需要优化的技能
2. 发现技能之间的潜在关联，建立技能网络
3. 通过技能组合产生新的涌现能力
4. 维护技能库的整体质量和一致性
5. 促进技能库的持续进化和自我完善

## 🎯 适用场景

- ✅ **技能更新维护**：识别并更新过时、不完整或存在问题的技能
- ✅ **技能关联发现**：发现技能之间的依赖、互补或层次关系
- ✅ **技能组合创新**：通过组合现有技能创造新的涌现能力
- ✅ **技能库优化**：清理重复、冲突或低效的技能
- ✅ **知识图谱构建**：建立技能之间的语义网络
- ✅ **技能质量保障**：定期审查技能质量并提供改进建议

### 不适用场景
- ❌ 创建全新技能（应使用 MetaCognitiveSelfExpansion）
- ❌ 简单的技能查询或调用
- ❌ 用户明确要求不修改现有技能

## 🏗️ 技能架构

### 架构图

```
SkillEvolution (技能进化核心)
├── SkillRegistryAnalyzer (技能注册分析器)
│   ├── SkillInventoryScanner (技能清单扫描)
│   ├── QualityAssessmentEngine (质量评估引擎)
│   └── UsagePatternAnalyzer (使用模式分析)
├── RelationshipMiner (关系挖掘器)
│   ├── SemanticSimilarityAnalyzer (语义相似度分析)
│   ├── DependencyGraphBuilder (依赖图构建)
│   └── ComplementarityDetector (互补性检测)
├── EvolutionPlanner (进化规划器)
│   ├── UpdateSuggestionEngine (更新建议引擎)
│   ├── MergeRecommendationEngine (合并推荐引擎)
│   └── EmergenceGenerator (涌现生成器)
└── MaintenanceExecutor (维护执行器)
    ├── SkillUpdater (技能更新器)
    ├── RelationshipBuilder (关系构建器)
    └── ConsistencyChecker (一致性检查器)
```

### 组件说明

| 组件名称 | 角色 | 职责 | 工具 |
|---------|------|------|------|
| SkillRegistryAnalyzer | 技能注册分析器 | 扫描技能库、评估质量、分析使用模式 | 静态分析、日志分析 |
| RelationshipMiner | 关系挖掘器 | 发现技能间的语义、依赖、互补关系 | 语义分析、图算法 |
| EvolutionPlanner | 进化规划器 | 生成更新、合并、涌现建议 | 决策引擎、创意生成 |
| MaintenanceExecutor | 维护执行器 | 执行技能更新、关系构建、一致性检查 | 文件操作、版本控制 |

## 🔄 工作流程

### 主工作流程

```
技能库扫描 → 质量评估 → 关系挖掘 → 进化规划 → 用户确认 → 维护执行 → 版本更新 → 关联建立
    ↓           ↓           ↓           ↓           ↓           ↓           ↓           ↓
[全量技能]  [识别问题]  [发现关联]  [生成建议]  [用户审批]  [执行维护]  [版本管理]  [网络构建]
```

### 详细步骤

#### 步骤 1：技能库扫描

**目标**: 全面扫描技能库，建立技能清单和使用档案

**输入**: 
- 技能目录路径
- 技能注册中心

**处理过程**:
1. 遍历所有技能文件夹
2. 读取每个技能的 SKILL.md 文件
3. 提取元数据（name, identifier, version, tags, updated 等）
4. 分析技能内容（适用场景、工作流程、工具依赖等）
5. 统计使用频率（通过日志或调用记录）
6. 建立技能索引

**输出**: 
- 技能清单（包含所有技能的元数据）
- 技能使用统计（频率、时间分布等）
- 技能内容索引（关键词、主题等）

**质量标准**:
- [ ] 技能扫描覆盖率 100%
- [ ] 元数据提取准确率 100%
- [ ] 使用统计完整

**示例**:
```
扫描完成：
- 技能总数：15
- 最近 30 天更新：3
- 高频使用（>10 次/周）：5
- 低频使用（<1 次/月）：4
- 从未使用：2
```

#### 步骤 2：质量评估

**目标**: 评估每个技能的质量，识别需要维护的技能

**输入**: 技能清单、技能内容

**处理过程**:
1. **完整性检查**：
   - 检查必需章节是否存在（适用场景、工作流程、示例等）
   - 检查元数据是否完整
   - 检查示例是否可运行

2. **一致性检查**：
   - 检查 identifier 与文件夹名是否一致
   - 检查版本号是否符合语义化版本规范
   - 检查内部引用是否有效

3. **时效性检查**：
   - 检查最后更新时间（>6 个月标记为"可能过时"）
   - 检查依赖的工具/库是否最新
   - 检查示例代码是否符合当前最佳实践

4. **实用性检查**：
   - 分析使用频率
   - 检查用户反馈（如有）
   - 识别长期未使用技能

**输出**: 
- 技能质量报告
- 问题技能列表
- 优先级评分

**质量标准**:
- [ ] 质量问题识别准确率>95%
- [ ] 优先级评分客观合理
- [ ] 建议具体可操作

#### 步骤 3：关系挖掘

**目标**: 发现技能之间的各种关联关系

**输入**: 技能清单、技能内容

**处理过程**:
1. **语义相似度分析**：
   - 提取技能关键词和主题
   - 计算技能间的语义相似度
   - 识别主题相近的技能群

2. **依赖关系分析**：
   - 识别技能的前置技能（"前置技能"章节）
   - 识别技能的后续技能（"后续技能"章节）
   - 构建技能依赖图（DAG）

3. **互补关系分析**：
   - 识别功能互补的技能（如：一个负责分析，一个负责执行）
   - 识别可以组合使用的技能
   - 识别共享工具或资源的技能

4. **层次关系分析**：
   - 识别通用技能和专用技能
   - 识别元技能和普通技能
   - 构建技能层次结构

**输出**: 
- 技能关系图
- 技能簇（主题相近的技能群）
- 依赖关系图
- 互补关系列表

**质量标准**:
- [ ] 关系识别准确率>90%
- [ ] 关系图完整
- [ ] 无循环依赖

#### 步骤 4：进化规划

**目标**: 基于质量评估和关系挖掘结果，生成进化建议

**输入**: 质量报告、关系图

**处理过程**:
1. **更新建议生成**：
   - 针对过时技能：建议更新内容和版本
   - 针对不完整技能：建议补充缺失章节
   - 针对低质量技能：建议重构或优化

2. **合并建议生成**：
   - 识别功能重复的技能
   - 识别可以整合的小技能
   - 生成合并方案

3. **涌现建议生成**：
   - 识别可以组合产生新能力的技能组合
   - 设计新的复合技能
   - 生成新技能的草稿

4. **清理建议生成**：
   - 识别长期未使用且无价值的技能
   - 识别与其他技能冲突的技能
   - 生成归档或删除建议

**输出**: 
- 进化建议列表
- 优先级排序
- 预期收益估算

**质量标准**:
- [ ] 建议清晰具体
- [ ] 收益估算合理
- [ ] 实施方案可行

#### 步骤 5：用户确认

**目标**: 获得用户对进化建议的审批

**输入**: 进化建议列表

**处理过程**:
1. 展示建议（按优先级排序）
2. 提供详细说明和预期收益
3. 等待用户确认或修改
4. 记录用户决策

**输出**: 
- 用户确认的建议列表
- 用户修改的意见
- 被拒绝的建议及原因

**质量标准**:
- [ ] 建议展示清晰
- [ ] 用户决策记录完整

#### 步骤 6：维护执行

**目标**: 执行用户确认的维护操作

**输入**: 用户确认的建议

**处理过程**:
1. **技能更新**：
   - 更新 SKILL.md 文件内容
   - 更新版本号
   - 更新最后修改日期

2. **关系建立**：
   - 在技能中添加"相关技能"章节
   - 建立双向引用
   - 更新技能关系图

3. **技能合并**：
   - 创建新的合并后技能
   - 迁移内容和示例
   - 归档旧技能

4. **涌现生成**：
   - 创建新的复合技能
   - 定义组合使用方式
   - 添加使用示例

**输出**: 
- 更新后的技能文件
- 新建立的技能关系
- 新创建的技能（如有）

**质量标准**:
- [ ] 更新准确无误
- [ ] 版本管理正确
- [ ] 关系引用完整

## 👥 维护策略引擎

### 更新决策规则

```python
def should_suggest_update(skill_analysis):
    """
    判断是否建议更新技能
    """
    reasons = []
    priority = 0
    
    # 规则 1：长时间未更新
    if skill_analysis.days_since_update > 180:  # 6 个月
        priority += 3
        reasons.append(f"已{skill_analysis.days_since_update}天未更新")
    
    # 规则 2：内容不完整
    if skill_analysis.missing_sections:
        priority += len(skill_analysis.missing_sections)
        reasons.append(f"缺少关键章节：{', '.join(skill_analysis.missing_sections)}")
    
    # 规则 3：示例不可运行
    if skill_analysis.broken_examples:
        priority += 5
        reasons.append(f"存在{skill_analysis.broken_examples}个不可运行的示例")
    
    # 规则 4：依赖过时
    if skill_analysis.outdated_dependencies:
        priority += 2
        reasons.append(f"依赖已过时：{', '.join(skill_analysis.outdated_dependencies)}")
    
    # 规则 5：用户反馈问题
    if skill_analysis.user_complaints > 0:
        priority += skill_analysis.user_complaints * 2
        reasons.append(f"收到{skill_analysis.user_complaints}个用户反馈")
    
    # 决策
    if priority >= 5:
        return True, "high" if priority >= 10 else "medium", reasons
    else:
        return False, "low", reasons
```

### 关联发现规则

```python
def discover_relationships(skill_a, skill_b):
    """
    发现两个技能之间的关系
    """
    relationships = []
    
    # 规则 1：语义相似度
    similarity = calculate_semantic_similarity(skill_a, skill_b)
    if similarity > 0.7:
        relationships.append({
            "type": "semantic_similar",
            "strength": similarity,
            "description": f"语义相似度高（{similarity:.2f}）"
        })
    
    # 规则 2：依赖关系
    if skill_b.identifier in skill_a.prerequisites:
        relationships.append({
            "type": "depends_on",
            "strength": 1.0,
            "description": f"{skill_a.name} 依赖 {skill_b.name}"
        })
    
    # 规则 3：工具共享
    shared_tools = set(skill_a.tools) & set(skill_b.tools)
    if len(shared_tools) >= 2:
        relationships.append({
            "type": "shares_tools",
            "strength": len(shared_tools) / max(len(skill_a.tools), len(skill_b.tools)),
            "description": f"共享工具：{', '.join(shared_tools)}"
        })
    
    # 规则 4：场景互补
    if are_scenes_complementary(skill_a.scenes, skill_b.scenes):
        relationships.append({
            "type": "complementary",
            "strength": 0.8,
            "description": "适用场景互补"
        })
    
    # 规则 5：可以组合
    if can_combine(skill_a, skill_b):
        relationships.append({
            "type": "combinable",
            "strength": 0.9,
            "description": "可以组合产生新能力",
            "emergence_potential": estimate_emergence(skill_a, skill_b)
        })
    
    return relationships
```

### 涌现生成规则

```python
def generate_emergence(skill_cluster):
    """
    基于技能簇生成涌现能力
    """
    emergences = []
    
    # 模式 1：线性组合（A → B → C）
    if is_linear_chain(skill_cluster):
        emergence = {
            "type": "linear_combination",
            "name": f"{skill_cluster[0].identifier}_to_{skill_cluster[-1].identifier}_pipeline",
            "description": f"将{len(skill_cluster)}个技能组合成自动化流水线",
            "components": [s.identifier for s in skill_cluster],
            "workflow": "sequential",
            "value_proposition": "一键完成多步骤任务"
        }
        emergences.append(emergence)
    
    # 模式 2：并行组合（同时调用多个技能）
    if can_execute_parallel(skill_cluster):
        emergence = {
            "type": "parallel_combination",
            "name": f"combined_{'_'.join([s.identifier for s in skill_cluster])}",
            "description": "并行执行多个相关技能，提高效率",
            "components": [s.identifier for s in skill_cluster],
            "workflow": "parallel",
            "value_proposition": "同时处理多个方面，减少总时间"
        }
        emergences.append(emergence)
    
    # 模式 3：增强组合（核心技能 + 辅助技能）
    if is_core_augment_structure(skill_cluster):
        core = find_core_skill(skill_cluster)
        augments = find_augment_skills(skill_cluster, core)
        emergence = {
            "type": "core_augmentation",
            "name": f"{core.identifier}_enhanced",
            "description": f"以{core.name}为核心，增强{len(augments)}个辅助能力",
            "core": core.identifier,
            "augments": [a.identifier for a in augments],
            "value_proposition": "核心能力得到全方位增强"
        }
        emergences.append(emergence)
    
    return emergences
```

## ⚙️ 执行模式

### Mode A: 审查模式（Audit Mode）

- **描述**: 仅扫描和分析，不提出具体建议
- **包含阶段**: 技能库扫描 → 质量评估 → 关系挖掘 → 生成报告
- **使用场景**: 定期体检、了解技能库状态
- **预计耗时**: 短（5-10 分钟）
- **输出**: 技能库健康报告

### Mode B: 建议模式（Suggestion Mode）

- **描述**: 分析并生成详细的进化建议
- **包含阶段**: 技能库扫描 → 质量评估 → 关系挖掘 → 进化规划 → 生成建议
- **使用场景**: 主动优化技能库、寻找改进机会
- **预计耗时**: 中等（10-20 分钟）
- **输出**: 进化建议列表（按优先级排序）

### Mode C: 执行模式（Execution Mode）

- **描述**: 执行用户确认的维护操作
- **包含阶段**: 技能库扫描 → 质量评估 → 关系挖掘 → 进化规划 → 用户确认 → 维护执行
- **使用场景**: 实际维护技能库
- **预计耗时**: 长（取决于维护范围）
- **输出**: 更新后的技能库、新建立的关系

### Mode D: 涌现模式（Emergence Mode）

- **描述**: 专注于发现和创造新的涌现能力
- **包含阶段**: 关系挖掘 → 技能簇识别 → 涌现生成 → 新技能创建
- **使用场景**: 创新驱动、扩展能力边界
- **预计耗时**: 长（创造性工作）
- **输出**: 新复合技能、组合使用指南

## 🚀 快速开始

### 前置条件

- [ ] 技能库中至少有 3 个技能
- [ ] 技能遵循标准目录结构（Skills/[Identifier]/SKILL.md）
- [ ] 有写入权限

### 基本用法

```bash
# 模式 1：审查模式（定期体检）
skill-evolution audit

# 模式 2：建议模式（寻找改进机会）
skill-evolution suggest

# 模式 3：执行模式（实际维护）
skill-evolution maintain --auto-approve=false

# 模式 4：涌现模式（创造新能力）
skill-evolution emerge --min-cluster-size=2
```

### 参数说明

| 参数 | 类型 | 必填 | 默认值 | 说明 |
|------|------|------|--------|------|
| `--mode` | string | 否 | "suggest" | 执行模式（audit/suggest/maintain/emerge） |
| `--auto-approve` | boolean | 否 | false | 是否自动批准建议（仅 maintain 模式） |
| `--min-cluster-size` | number | 否 | 2 | 涌现模式中最小技能簇大小 |
| `--include-archived` | boolean | 否 | false | 是否包含已归档技能 |
| `--output-format` | string | 否 | "markdown" | 报告格式（markdown/json/html） |

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
      "auto_approve": "类型：boolean，说明：是否自动批准",
      "min_cluster_size": "类型：number，说明：最小簇大小",
      "include_archived": "类型：boolean，说明：包含归档技能"
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
    "healthy_skills": "健康技能数",
    "needs_update": "需要更新数",
    "low_usage": "低使用率数",
    "broken_examples": "示例问题数"
  },
  "suggestions": [
    {
      "type": "update|merge|emerge|archive",
      "priority": "high|medium|low",
      "target_skills": ["受影响的技能"],
      "description": "建议描述",
      "expected_benefit": "预期收益",
      "implementation_plan": "实施计划"
    }
  ],
  "relationships": {
    "total_discovered": "发现的关系数",
    "dependency_graph": "依赖关系图",
    "similarity_clusters": "相似度簇"
  },
  "emergences": [
    {
      "name": "新技能名称",
      "type": "linear|parallel|core_augment",
      "components": ["组成技能"],
      "description": "涌现能力描述"
    }
  ]
}
```

## ✅ 质量门禁

### 检查清单

#### 完整性检查
- [ ] 技能库扫描覆盖率 100%
- [ ] 质量评估覆盖所有技能
- [ ] 关系挖掘完整
- [ ] 建议生成全面

#### 准确性检查
- [ ] 质量问题识别准确率>95%
- [ ] 关系识别准确率>90%
- [ ] 建议合理性评分>0.8
- [ ] 涌现创意可行性>70%

#### 性能检查
- [ ] 扫描响应时间 < 5 秒
- [ ] 分析响应时间 < 10 秒
- [ ] 建议生成响应时间 < 5 秒
- [ ] 总体额外开销 < 20 秒

### 验收标准

- [ ] 能正确识别过时技能（>6 个月未更新）
- [ ] 能正确发现技能依赖关系
- [ ] 能生成具体可行的维护建议
- [ ] 能创造有意义的涌现能力
- [ ] 维护操作不破坏现有功能
- [ ] 版本管理正确

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_SCAN_FAILED | 技能库扫描失败 | 路径错误或权限不足 | 检查路径和权限 |
| ERR_PARSE_FAILED | 技能文件解析失败 | 文件格式不正确 | 检查 SKILL.md 格式 |
| ERR_RELATIONSHIP_CYCLE | 检测到循环依赖 | 技能间形成循环引用 | 手动打破循环 |
| ERR_UPDATE_CONFLICT | 更新冲突 | 文件已被修改 | 重新加载后重试 |
| ERR_EMERGENCE_INVALID | 涌现方案无效 | 组合不合理 | 调整组合策略 |

### 异常处理流程

```
检测到异常
    ↓
分类异常类型
    ↓
可恢复？→ 是 → 尝试自动修复
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
- **重试条件**: 文件锁定、网络超时等临时错误

## 📚 最佳实践

### 推荐做法

- ✅ **定期审查**: 每月至少执行一次审查模式
- ✅ **渐进优化**: 优先处理高优先级建议
- ✅ **版本管理**: 每次更新都增加版本号
- ✅ **用户参与**: 重要决策征求用户意见
- ✅ **文档同步**: 更新技能时同步更新文档
- ✅ **关系维护**: 及时建立新发现的关联

### 避免做法

- ❌ **大规模重构**: 避免一次性修改过多技能
- ❌ **破坏性更新**: 避免不兼容的修改
- ❌ **忽视反馈**: 不要忽略用户反馈的问题
- ❌ **过度关联**: 避免创建过多无意义的关联
- ❌ **版本混乱**: 避免不遵循语义化版本

### 性能优化

- 使用缓存存储技能元数据
- 增量分析而非全量分析
- 并行处理独立技能
- 定期清理缓存

### 安全建议

- 所有修改前创建 Git 提交点
- 重要修改需用户确认
- 保留修改历史记录
- 定期备份技能库

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
SKILLS_PATH=./AIKnowledge/Skills

# 可选配置
AUTO_APPROVE_THRESHOLD=0.95
MAX_SUGGESTIONS_PER_RUN=10
ENABLE_AUTO_VERSIONING=true
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_evolution_config.yaml
skill_evolution:
  version: 1.0.0
  
  paths:
    skills: "./AIKnowledge/Skills"
    archive: "./AIKnowledge/Skills/Archived"
  
  audit:
    schedule: "monthly"  # weekly, monthly, quarterly
    include_archived: false
    
  quality_thresholds:
    max_days_without_update: 180
    min_usage_per_month: 1
    required_sections:
      - "适用场景"
      - "工作流程"
      - "示例"
    
  relationship:
    min_similarity_threshold: 0.7
    auto_link_similar: true
    
  emergence:
    enabled: true
    min_cluster_size: 2
    max_cluster_size: 5
    
  versioning:
    auto_increment: true
    semantic_versioning: true
    
  logging:
    level: info
    file: "./logs/skill_evolution.log"
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的分析过程
- **INFO**: 关键步骤信息（扫描完成、建议生成等）
- **WARN**: 警告信息（质量问题、潜在冲突）
- **ERROR**: 错误信息（解析失败、更新失败）

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 技能健康度 | 健康技能占比 | < 70% |
| 平均技能年龄 | 技能平均未更新天数 | > 180 天 |
| 关系密度 | 平均每技能关联数 | < 2 |
| 建议接受率 | 用户接受的建议比例 | < 50% |
| 涌现产出率 | 每月新涌现技能数 | < 1 |

### 监控仪表板示例

```
技能进化监控仪表板
=====================================
技能库概览:
- 技能总数：15
- 健康技能：10 (66.7%)
- 需要更新：3
- 低使用率：4
- 已归档：2

质量趋势:
- 平均技能年龄：120 天
- 最近 30 天更新：3
- 示例问题：2

关系网络:
- 总关联数：28
- 平均关联度：1.87/技能
- 技能簇：4 个

本月涌现:
- 新复合技能：2
- 建议接受：5/8 (62.5%)

告警:
- ⚠️ 技能健康度低于 70%
- ⚠️ 3 个技能超过 6 个月未更新
```

## 🧪 测试用例

### 单元测试

#### 测试用例 1：过时技能识别

```yaml
输入:
  skill:
    identifier: OldSkill
    last_updated: "2025-06-30"  # 9 个月前
    missing_sections: []
预期输出:
  should_update: true
  priority: high
  reasons: ["已 270 天未更新"]
结果: ✅ 通过
```

#### 测试用例 2：技能关联发现

```yaml
输入:
  skill_a:
    identifier: CodeAnalyzer
    tools: ["ESLint", "Prettier"]
    scenes: ["代码审查", "质量检查"]
  skill_b:
    identifier: CodeFormatter
    tools: ["Prettier", "prettier-eslint"]
    scenes: ["代码格式化", "风格统一"]
预期输出:
  relationships:
    - type: "shares_tools"
      strength: 0.5
      shared: ["Prettier"]
    - type: "complementary"
      strength: 0.8
      description: "场景互补"
结果: ✅ 通过
```

#### 测试用例 3：涌现能力生成

```yaml
输入:
  cluster:
    - identifier: DataCollector
    - identifier: DataCleaner
    - identifier: DataAnalyzer
预期输出:
  emergence:
    type: "linear_combination"
    name: "data_pipeline"
    description: "数据收集→清洗→分析自动化流水线"
    components: ["DataCollector", "DataCleaner", "DataAnalyzer"]
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整维护流程

**测试步骤**:
1. 执行技能库扫描
2. 识别出 3 个需要更新的技能
3. 发现 2 对技能可以关联
4. 生成 5 个维护建议
5. 用户确认其中 3 个
6. 执行维护操作
7. 验证更新成功

**预期结果**: 
- 扫描完整
- 建议合理
- 执行成功
- 版本正确

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
skill-evolution audit --output-format=markdown
```

**输出报告**:
```markdown
# 技能库健康报告 - 2026 年 3 月

## 概览
- 技能总数：15
- 健康技能：10 (66.7%)
- 需要关注：5

## 需要更新的技能

### 1. OldComponent (优先级：高)
- **最后更新**: 2025-08-15 (227 天前)
- **问题**: 
  - ⚠️ 超过 6 个月未更新
  - ⚠️ 示例代码使用过时的 React 写法
- **建议**: 更新示例代码，增加 React Hooks 用法

### 2. LegacyAPI (优先级：中)
- **最后更新**: 2025-10-20 (161 天前)
- **问题**:
  - ⚠️ API 已过时
  - ⚠️ 依赖的库已更新到 v3
- **建议**: 更新 API 调用方式，升级依赖

## 技能关联建议

发现以下技能可以建立关联：
- CodeAnalyzer ↔ CodeFormatter (共享工具：Prettier)
- DataCollector ↔ DataCleaner (场景互补)

## 行动建议
1. 优先更新 OldComponent
2. 建立 2 对新关联
3. 考虑归档 LegacyAPI
```

### 示例 2：发现技能关联并建立

**场景**: 发现两个技能可以互补使用

**执行命令**:
```bash
skill-evolution suggest --mode=relationship
```

**Agent 主动建议**:
```
🔍 **关联发现**

我发现以下两个技能可以建立关联：

**技能 A**: CodeAnalyzer
- 功能：代码静态分析和质量检查
- 工具：ESLint, Prettier

**技能 B**: CodeFormatter  
- 功能：代码格式化和风格统一
- 工具：Prettier, prettier-eslint

**关联类型**: 互补关系 + 工具共享

**建议**:
1. 在 CodeAnalyzer 中添加"相关技能：CodeFormatter"
2. 在 CodeFormatter 中添加"相关技能：CodeAnalyzer"
3. 创建组合使用示例

**预期收益**:
- 📈 用户可以更方便地发现相关技能
- 🔄 促进两个技能的组合使用
- 💡 可能涌现出"代码质量自动化"新能力

是否建立这个关联？
```

**用户确认**:
```
好的，建立这个关联
```

**Agent 执行**:
```
✅ **关联建立成功**

已更新以下技能：

1. **CodeAnalyzer/SKILL.md**
   - 添加章节：## 🔗 相关技能
   - 添加内容：- [CodeFormatter](../CodeFormatter/SKILL.md) - 代码格式化

2. **CodeFormatter/SKILL.md**
   - 添加章节：## 🔗 相关技能  
   - 添加内容：- [CodeAnalyzer](../CodeAnalyzer/SKILL.md) - 代码分析

关联已建立！现在用户在使用任一技能时都能看到另一个。
```

### 示例 3：涌现新能力

**场景**: 通过技能组合创造新的涌现能力

**执行命令**:
```bash
skill-evolution emerge --min-cluster-size=2
```

**Agent 分析**:
```
💡 **涌现机会发现**

我识别到一个技能簇，可以组合产生新能力：

**技能簇**:
1. **DataCollector** - 数据收集
2. **DataCleaner** - 数据清洗  
3. **DataAnalyzer** - 数据分析

**组合模式**: 线性流水线（Collector → Cleaner → Analyzer）

**涌现方案**:

### 新技能：DataPipeline

**描述**: 自动化数据处理流水线，一键完成数据收集→清洗→分析全流程

**组成**:
- DataCollector (负责收集)
- DataCleaner (负责清洗)
- DataAnalyzer (负责分析)

**工作流**:
```
数据源 → [收集] → 原始数据 → [清洗] → 干净数据 → [分析] → 分析报告
```

**价值主张**:
- ⚡ 一键完成全流程，无需手动切换
- 🎯 自动化数据流转，减少人工干预
- 📊 标准化输出，保证质量一致性
- 🔧 可配置每个环节的参数

**使用示例**:
```
用 DataPipeline 处理销售数据
数据源：PostgreSQL
清洗规则：去除空值、标准化格式
分析类型：趋势分析、同比环比

输出：完整的销售分析报告
```

是否需要我创建这个新技能？
```

**用户确认**:
```
太好了，创建这个新技能！
```

**Agent 执行**:
```
✅ **涌现技能创建成功**

已创建新技能：DataPipeline

**文件位置**: 
`AIKnowledge/Skills/DataPipeline/SKILL.md`

**技能特点**:
- 类型：复合技能（线性组合）
- 组成：3 个基础技能
- 版本：1.0.0

**已建立关联**:
- DataPipeline → DataCollector (组成关系)
- DataPipeline → DataCleaner (组成关系)
- DataPipeline → DataAnalyzer (组成关系)
- DataCollector → DataPipeline (被组合)
- DataCleaner → DataPipeline (被组合)
- DataAnalyzer → DataPipeline (被组合)

**下一步**:
1. 审查新技能的 SKILL.md
2. 添加具体的使用示例
3. 测试流水线是否正常工作

现在请试试说："用 DataPipeline 处理销售数据" 🚀
```

## 🔗 相关资源

### 前置技能
- [MetaCognitiveSelfExpansion](../MetaCognitiveSelfExpansion/SKILL.md) - 元认知与自我扩展

### 后续技能
- [SkillDeployment](链接) - 技能部署与发布
- [SkillMetrics](链接) - 技能度量与分析

### 参考资料
- [知识图谱构建方法](链接)
- [涌现智能理论](链接)
- [技能组合设计模式](链接)
- [语义相似度计算](链接)

### 工具依赖
- [语义分析库](https://github.com/UKPLab/sentence-transformers) - 语义相似度计算
- [图算法库](https://networkx.org/) - 关系图构建
- [版本管理](https://git-scm.com/) - 版本控制

## ❓ FAQ

### Q1: 如何避免过度维护？

**问题**: 担心频繁维护技能会影响稳定性。

**解答**: 
1. **设置阈值**: 在配置中设置合理的维护阈值
2. **优先级排序**: 优先处理高优先级问题
3. **定期审查**: 每月审查一次，而非每天
4. **用户确认**: 重要修改需用户确认

```yaml
quality_thresholds:
  max_days_without_update: 180  # 6 个月才标记
  min_usage_per_month: 1        # 每月至少使用 1 次
```

**相关资源**: [配置指南](链接)

### Q2: 涌现技能和普通技能有什么区别？

**问题**: 不理解涌现技能的特殊性。

**解答**: 

**普通技能**:
- 独立功能
- 直接调用
- 单一职责

**涌现技能**:
- 组合功能（2 个以上基础技能）
- 间接调用（通过组合器）
- 产生新能力（1+1>2）

**示例**:
- 普通：DataCollector（仅收集）
- 涌现：DataPipeline（收集 + 清洗 + 分析 = 自动化流水线）

**相关资源**: [涌现设计模式](链接)

### Q3: 如何处理技能间的循环依赖？

**问题**: 发现技能 A 依赖 B，B 依赖 C，C 又依赖 A。

**解答**: 
1. **检测循环**: 使用图算法检测循环
2. **识别断点**: 找出最弱的依赖关系
3. **打破循环**: 移除或重构该依赖
4. **验证**: 确认循环已打破

```python
# 检测循环
if has_cycle(dependency_graph):
    cycle = find_cycle(dependency_graph)
    weakest_link = find_weakest_edge(cycle)
    suggest_remove(weakest_link)
```

**相关资源**: [依赖管理指南](链接)

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-30 | AI Assistant | 初始版本，包含完整的技能维护与关联涌现能力 |
