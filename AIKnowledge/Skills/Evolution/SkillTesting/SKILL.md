---
name: SkillTesting
description: 技能测试与验证专家，负责为技能生成单元测试和集成测试（覆盖率≥80%）、验证技能输出质量和一致性、执行回归测试确保向后兼容、进行性能测试和负载测试、生成测试报告和覆盖率分析，适用于新技能测试、发布前验证、回归测试、性能基准测试场景
---

# 技能测试与验证

## 🎯 核心目标

赋予 Agent **技能测试** 与 **质量验证** 的能力，使其能够：
1. 为技能生成单元测试和集成测试
2. 验证技能输出质量和一致性
3. 执行回归测试确保更新不破坏现有功能
4. 进行性能测试和负载测试
5. 生成测试报告和覆盖率分析

## 🎯 适用场景

- ✅ **新技能测试**：新开发技能的测试用例生成和执行
- ✅ **回归测试**：技能更新前的回归测试
- ✅ **性能测试**：技能性能基准测试和负载测试
- ✅ **质量验证**：验证技能输出质量和一致性
- ✅ **测试覆盖率**：分析测试覆盖率和生成补充测试
- ✅ **持续测试**：CI/CD 流水线中的自动化测试

### 不适用场景
- ❌ 技能开发阶段的功能实现（应使用 development-engineer）
- ❌ 技能部署（应使用 SkillDeployment）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 核心组件

```
SkillTesting (测试核心)
├── TestGenerator (测试生成器)
│   ├── UnitTestGenerator (单元测试生成)
│   ├── IntegrationTestGenerator (集成测试生成)
│   └── PerformanceTestGenerator (性能测试生成)
├── TestExecutor (测试执行器)
│   ├── SequentialRunner (顺序执行器)
│   ├── ParallelRunner (并行执行器)
│   └── CoverageAnalyzer (覆盖率分析器)
├── ResultValidator (结果验证器)
│   ├── OutputValidator (输出验证)
│   ├── QualityChecker (质量检查)
│   └── ConsistencyVerifier (一致性验证)
└── ReportGenerator (报告生成器)
    ├── TestReport (测试报告)
    ├── CoverageReport (覆盖率报告)
    └── SuggestionEngine (建议引擎)
```

## 🔄 工作流程

```
测试规划 → 测试生成 → 测试执行 → 结果验证 → 报告生成 → 问题追踪
    ↓          ↓          ↓          ↓          ↓          ↓
[测试策略] [生成用例] [执行测试] [验证结果] [生成报告] [追踪问题]
```

## ⚙️ 执行模式

### Mode A: 单元测试模式
- 生成和执行单元测试
- 验证技能的各个功能点
- 覆盖率分析

### Mode B: 集成测试模式
- 测试技能与其他技能的集成
- 验证端到端流程
- 依赖关系测试

### Mode C: 性能测试模式
- 基准测试
- 负载测试
- 压力测试

### Mode D: 回归测试模式
- 更新前的全面回归测试
- 对比历史结果
- 识别破坏性变更

## 👥 测试策略引擎

### 测试用例生成规则

```python
def generate_test_cases(skill_definition, test_type='all'):
    """
    根据技能定义生成测试用例
    """
    test_cases = []
    
    # 单元测试用例
    if test_type in ['unit', 'all']:
        for function in skill_definition.functions:
            # 正常场景
            test_cases.append({
                "type": "unit",
                "function": function.name,
                "scenario": "normal_case",
                "input": function.example_input,
                "expected_output": function.example_output,
                "assertions": ["输出格式正确", "内容完整", "逻辑合理"]
            })
            
            # 边界场景
            test_cases.append({
                "type": "unit",
                "function": function.name,
                "scenario": "edge_case",
                "input": function.edge_case_input,
                "expected_output": "处理成功或抛出预期异常",
                "assertions": ["边界处理正确"]
            })
            
            # 异常场景
            test_cases.append({
                "type": "unit",
                "function": function.name,
                "scenario": "error_case",
                "input": function.invalid_input,
                "expected_error": function.expected_error_type,
                "assertions": ["错误类型正确", "错误消息清晰"]
            })
    
    # 集成测试用例
    if test_type in ['integration', 'all']:
        for workflow in skill_definition.workflows:
            test_cases.append({
                "type": "integration",
                "workflow": workflow.name,
                "input": workflow.example_input,
                "expected_output": workflow.expected_output,
                "dependencies": workflow.dependencies,
                "assertions": ["端到端流程正确", "数据传递准确"]
            })
    
    return test_cases
```

### 测试执行策略

```python
def execute_tests(test_cases, config):
    """
    执行测试用例
    """
    results = {
        "total": len(test_cases),
        "passed": 0,
        "failed": 0,
        "skipped": 0,
        "details": []
    }
    
    # 并行执行配置
    if config.get('parallel', False):
        test_groups = group_by_dependency(test_cases)
        for group in test_groups:
            parallel_execute(group)
    else:
        for test_case in test_cases:
            result = run_single_test(test_case)
            if result.status == 'passed':
                results['passed'] += 1
            elif result.status == 'failed':
                results['failed'] += 1
            results['details'].append(result)
    
    return results
```

### 覆盖率分析规则

```python
def analyze_coverage(skill_code, executed_tests):
    """
    分析测试覆盖率
    """
    coverage = {
        "statement_coverage": 0,
        "branch_coverage": 0,
        "function_coverage": 0,
        "line_details": [],
        "uncovered_lines": [],
        "partially_covered_branches": []
    }
    
    # 语句覆盖率
    total_statements = count_statements(skill_code)
    covered_statements = count_covered_statements(executed_tests)
    coverage['statement_coverage'] = covered_statements / total_statements * 100
    
    # 分支覆盖率
    total_branches = count_branches(skill_code)
    covered_branches = count_covered_branches(executed_tests)
    coverage['branch_coverage'] = covered_branches / total_branches * 100
    
    # 函数覆盖率
    total_functions = count_functions(skill_code)
    covered_functions = count_covered_functions(executed_tests)
    coverage['function_coverage'] = covered_functions / total_functions * 100
    
    # 识别未覆盖的代码
    coverage['uncovered_lines'] = get_uncovered_lines(skill_code, executed_tests)
    
    return coverage
```

## 📋 输入输出规范

### 输入格式

```json
{
  "skill_identifier": "类型：string，说明：技能标识名",
  "test_config": {
    "type": "object",
    "description": "测试配置",
    "properties": {
      "test_types": "类型：array，说明：测试类型（unit/integration/performance/regression）",
      "coverage_threshold": "类型：number，说明：覆盖率阈值（百分比）",
      "parallel_enabled": "类型：boolean，说明：是否启用并行执行",
      "timeout_per_test": "类型：number，说明：单个测试超时（秒）",
      "retry_failed": "类型：boolean，说明：是否重试失败测试"
    }
  },
  "test_data": {
    "type": "object",
    "description": "测试数据",
    "properties": {
      "custom_test_cases": "类型：array，说明：自定义测试用例",
      "mock_dependencies": "类型：object，说明：依赖模拟配置",
      "environment": "类型：object，说明：测试环境配置"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "test_summary": {
    "total_tests": "总测试数",
    "passed": "通过数",
    "failed": "失败数",
    "skipped": "跳过数",
    "duration_seconds": "执行耗时（秒）",
    "pass_rate": "通过率（百分比）"
  },
  "coverage_report": {
    "statement_coverage": "语句覆盖率",
    "branch_coverage": "分支覆盖率",
    "function_coverage": "函数覆盖率",
    "overall_coverage": "总体覆盖率",
    "meets_threshold": "是否达到阈值"
  },
  "test_details": [
    {
      "test_id": "测试 ID",
      "test_name": "测试名称",
      "type": "测试类型",
      "status": "passed|failed|skipped",
      "duration_ms": "执行耗时（毫秒）",
      "error_message": "错误消息（如果失败）",
      "stack_trace": "堆栈追踪（如果失败）"
    }
  ],
  "failed_tests": [
    {
      "test_id": "测试 ID",
      "test_name": "测试名称",
      "expected": "预期结果",
      "actual": "实际结果",
      "failure_reason": "失败原因",
      "suggestion": "修复建议"
    }
  ],
  "recommendations": ["改进建议列表"]
}
```

## ✅ 质量门禁

### 测试设计检查

- [ ] 测试用例覆盖所有功能点
- [ ] 包含正常、边界、异常场景
- [ ] 测试数据具有代表性
- [ ] 断言清晰明确
- [ ] 测试可重复执行

### 测试执行检查

- [ ] 单元测试覆盖率>80%
- [ ] 分支覆盖率>75%
- [ ] 函数覆盖率>90%
- [ ] 集成测试通过率>95%
- [ ] 性能测试达标

### 测试质量检查

- [ ] 测试独立无依赖
- [ ] 测试执行快速（<10 秒/个）
- [ ] 错误信息清晰
- [ ] 测试结果可重现
- [ ] 测试易于维护

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_TEST_GENERATION_FAILED | 测试生成失败 | 技能定义不完整 | 补充技能定义和示例 |
| ERR_TEST_TIMEOUT | 测试超时 | 测试执行时间过长 | 优化测试或增加超时 |
| ERR_ASSERTION_FAILED | 断言失败 | 实际结果与预期不符 | 检查技能逻辑或更新预期 |
| ERR_DEPENDENCY_MISSING | 依赖缺失 | 测试依赖的技能未安装 | 安装缺失的依赖 |
| ERR_MOCK_SETUP_FAILED | 模拟设置失败 | 模拟配置错误 | 检查模拟配置 |
| ERR_COVERAGE_BELOW_THRESHOLD | 覆盖率低于阈值 | 测试覆盖不足 | 增加测试用例 |

### 异常处理流程

```
测试执行异常
    ↓
分类异常类型（断言失败/超时/错误）
    ↓
断言失败？→ 是 → 记录失败，继续执行
    ↓           ↓
    否      超时？→ 是 → 终止测试，标记超时
    ↓           ↓
记录错误    继续执行下一测试
    ↓
生成测试报告
```

### 重试策略

- **最大重试次数**: 2 次
- **重试条件**: 网络错误、临时故障、资源竞争
- **重试间隔**: 1 秒

## 📚 最佳实践

### 推荐做法

- ✅ **测试先行**：技能开发前先写测试
- ✅ **覆盖全面**：覆盖所有功能点和场景
- ✅ **测试独立**：测试间无依赖关系
- ✅ **快速执行**：保持测试执行快速
- ✅ **清晰断言**：断言明确，错误信息清晰
- ✅ **持续集成**：CI/CD 中自动执行测试
- ✅ **定期审查**：定期审查和更新测试

### 避免做法

- ❌ **测试依赖**：测试间相互依赖
- ❌ **过度模拟**：过度使用 mock
- ❌ **脆弱测试**：测试容易受实现变化影响
- ❌ **慢测试**：测试执行过慢
- ❌ **模糊断言**：断言不清晰
- ❌ **忽视失败**：忽视失败的测试

### 测试设计原则

遵循 FIRST 原则：
- **F**ast（快速）：测试执行快
- **I**ndependent（独立）：测试间独立
- **R**epeatable（可重复）：结果可重现
- **S**elf-validating（自验证）：自动判断成败
- **T**imely（及时）：及时编写和维护

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
TESTS_PATH=./tests
ENABLE_TESTING=true

# 可选配置
DEFAULT_TEST_TYPES=unit,integration
COVERAGE_THRESHOLD=80
PARALLEL_ENABLED=true
TIMEOUT_PER_TEST=30
RETRY_FAILED=false
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_testing_config.yaml
skill_testing:
  version: 1.0.0
  
  paths:
    tests: "./tests"
    reports: "./test-reports"
    coverage: "./coverage"
  
  test_generation:
    auto_generate: true
    include_unit: true
    include_integration: true
    include_performance: false
    generate_edge_cases: true
  
  execution:
    parallel_enabled: true
    max_parallel: 4
    timeout_per_test_seconds: 30
    retry_failed: false
    max_retries: 2
  
  coverage:
    enabled: true
    threshold_percent: 80
    report_formats:
      - html
      - json
      - markdown
    include_details: true
  
  reporting:
    auto_generate: true
    formats:
      - markdown
      - html
    include_failed_details: true
    include_suggestions: true
  
  logging:
    level: info
    file: "./logs/skill_testing.log"
    max_size: "10MB"
    retention_days: 30
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的测试执行过程
- **INFO**: 关键步骤信息（开始、完成、结果）
- **WARN**: 警告信息（慢测试、覆盖率下降等）
- **ERROR**: 错误信息（测试失败、超时等）

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 测试通过率 | 通过测试比例 | < 95% |
| 测试覆盖率 | 代码覆盖比例 | < 80% |
| 平均测试时间 | 测试平均耗时 | > 10 秒 |
| 失败测试数 | 失败测试数量 | > 0 |
| 测试稳定性 | 重复执行一致率 | < 99% |

### 测试仪表板示例

```
技能测试监控仪表板
=====================================
测试概览:
- 总测试数：156
- 通过率：98.7%
- 覆盖率：85.3%
- 执行时间：2.5 分钟

测试分布:
- 单元测试：120 (通过率 99%)
- 集成测试：30 (通过率 97%)
- 性能测试：6 (通过率 100%)

覆盖率趋势:
- 语句覆盖率：85.3% ↑
- 分支覆盖率：78.2% →
- 函数覆盖率：92.1% ↑

失败测试 Top 3:
1. test_edge_case_large_input (失败 3 次)
2. test_integration_workflow_b (失败 2 次)
3. test_performance_under_load (失败 1 次)

告警:
- ⚠️ 分支覆盖率低于阈值 (78.2% < 80%)
- ⚠️ 2 个测试执行时间超过 10 秒
```

## 🧪 测试用例

### 单元测试

#### 测试用例 1：测试生成器

```yaml
输入:
  skill_definition:
    identifier: CodeReviewer
    functions:
      - name: review_code
        example_input: "def hello(): pass"
        example_output: "代码质量良好"
  test_type: "unit"
预期输出:
  test_cases_count: 3
  test_types: ["normal_case", "edge_case", "error_case"]
结果: ✅ 通过
```

#### 测试用例 2：测试执行器

```yaml
输入:
  test_cases:
    - test_id: "test_001"
      input: "valid_code"
      expected: "success"
  config:
    parallel: false
预期输出:
  total: 1
  passed: 1
  failed: 0
结果: ✅ 通过
```

#### 测试用例 3：覆盖率分析器

```yaml
输入:
  skill_code: "def func(): ..."
  executed_tests: [test1, test2, test3]
预期输出:
  statement_coverage: 85.5
  branch_coverage: 78.2
  function_coverage: 92.1
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整测试流程

**测试步骤**:
1. 加载技能定义
2. 生成测试用例（unit + integration）
3. 执行所有测试
4. 分析覆盖率
5. 生成测试报告
6. 验证达到阈值

**预期结果**: 
- 测试生成成功
- 测试执行完成
- 覆盖率达到阈值
- 报告生成成功

### 测试覆盖率要求

- 语句覆盖率：≥ 80%
- 分支覆盖率：≥ 75%
- 函数覆盖率：≥ 90%
- 场景覆盖率：≥ 85%

## 📖 示例

### 示例 1：新技能测试

**场景**: 为新开发的 CodeReviewer 技能生成和执行测试

**执行命令**:
```bash
skill-testing generate-and-run --skill=CodeReviewer --types=unit,integration --coverage=true
```

**执行过程**:
```
🔍 **技能测试执行**

**技能**: CodeReviewer v1.0.0

**步骤 1: 生成测试用例**
✅ 生成 15 个单元测试
✅ 生成 5 个集成测试
✅ 生成 2 个性能测试

**步骤 2: 执行测试**
[1/22] ✅ test_review_simple_function (0.5s)
[2/22] ✅ test_review_complex_class (0.8s)
[3/22] ✅ test_review_with_syntax_error (0.3s)
...
[22/22] ✅ test_performance_under_load (3.2s)

**步骤 3: 覆盖率分析**
- 语句覆盖率：87.5% ✅
- 分支覆盖率：76.3% ✅
- 函数覆盖率：93.2% ✅

**测试结果**:
- 总计：22
- 通过：22
- 失败：0
- 跳过：0
- 通过率：100%
- 总耗时：8.5 秒

✅ 所有测试通过，覆盖率达标
```

### 示例 2：回归测试

**场景**: 技能更新前执行回归测试

**执行命令**:
```bash
skill-testing regression --skill=CodeReviewer --compare-with=1.0.0
```

**测试报告**:
```markdown
# 回归测试报告

## 测试信息
- **技能**: CodeReviewer
- **当前版本**: 1.1.0
- **对比版本**: 1.0.0
- **测试时间**: 2026-03-31

## 测试结果
- **总测试数**: 50
- **通过**: 48
- **失败**: 2
- **跳过**: 0
- **通过率**: 96%

## 失败测试详情

### 1. test_review_async_function
- **失败原因**: 输出格式变化
- **预期**: 包含"async"关键字
- **实际**: 使用"异步"描述
- **影响**: 低（仅描述变化，功能正常）
- **建议**: 更新测试断言

### 2. test_performance_large_file
- **失败原因**: 性能下降
- **预期**: <5 秒
- **实际**: 5.8 秒
- **影响**: 中（性能退化 16%）
- **建议**: 优化大文件处理逻辑

## 破坏性变更检测
✅ 未检测到破坏性变更

## 建议
1. 更新 test_review_async_function 的断言
2. 优化大文件处理性能
3. 可以发布新版本（建议先修复性能问题）
```

### 示例 3：性能测试

**场景**: 测试技能在高负载下的表现

**执行命令**:
```bash
skill-testing performance --skill=CodeReviewer --load=1000 --concurrent=10
```

**性能测试报告**:
```markdown
# 性能测试报告

## 测试配置
- **并发用户数**: 10
- **总请求数**: 1000
- **测试持续时间**: 2 分钟

## 性能指标

### 响应时间
- **平均**: 850ms
- **P50**: 720ms
- **P90**: 1200ms
- **P95**: 1500ms
- **P99**: 2100ms

### 吞吐量
- **请求/秒**: 118 req/s
- **成功请求**: 998
- **失败请求**: 2
- **成功率**: 99.8%

### 资源使用
- **CPU 使用率**: 65%
- **内存使用**: 512MB
- **Token 消耗**: 平均 1200 tokens/请求

## 负载测试结论

### ✅ 通过项
- 成功率>99%
- P95 响应时间<2 秒
- 无内存泄漏

### ⚠️ 警告项
- P99 响应时间>2 秒（2.1 秒）
- 高负载下 CPU 使用率较高

### ❌ 失败项
- 无

## 优化建议
1. 添加缓存机制减少重复计算
2. 优化大文件处理逻辑
3. 考虑异步处理提升并发能力
```

## 🔗 相关资源

### 前置技能
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析
- [SkillDeployment](../SkillDeployment/SKILL.md) - 技能部署与发布

### 后续技能
- [SkillSecurityAuditor](../SkillSecurityAuditor/SKILL.md) - 技能安全审计
- [SkillPerformanceOptimizer](../SkillPerformanceOptimizer/SKILL.md) - 技能性能优化器

### 参考资料
- [测试驱动开发 (TDD)](链接)
- [单元测试最佳实践](链接)
- [测试覆盖率指南](链接)
- [性能测试方法](链接)

### 工具依赖
- [测试框架](https://pytest.org/) - 测试执行框架
- [覆盖率工具](https://coverage.readthedocs.io/) - 覆盖率分析
- [性能测试工具](https://locust.io/) - 负载测试

## ❓ FAQ

### Q1: 如何生成高质量的测试用例？

**问题**: 生成的测试用例质量不高，覆盖不全面。

**解答**: 
1. **提供完整定义**：确保技能定义包含完整的函数说明、输入输出示例
2. **多样化测试数据**：提供多种场景的测试数据（正常、边界、异常）
3. **人工审查**：生成的测试用例需要人工审查和补充
4. **持续改进**：根据测试结果不断改进测试用例

**示例**:
```yaml
# 好的技能定义
functions:
  - name: review_code
    description: 审查代码质量
    input_examples:
      normal: "def hello(): print('Hello')"
      edge: ""  # 空代码
      invalid: "def invalid(: "  # 语法错误
    output_examples:
      normal: "代码质量良好，无问题"
      edge: "代码为空"
      error: "语法错误：..."
```

### Q2: 如何处理测试失败？

**问题**: 测试失败后不知道如何处理。

**解答**: 
1. **分析失败原因**：查看错误消息和堆栈追踪
2. **分类处理**：
   - 技能 bug → 修复技能
   - 测试错误 → 修复测试
   - 预期过时 → 更新预期
3. **重现问题**：单独运行失败测试
4. **回归验证**：修复后运行完整测试集

**流程**:
```
测试失败
    ↓
分析原因（技能 bug/测试错误/预期过时）
    ↓
修复问题
    ↓
重新运行测试
    ↓
验证通过
```

### Q3: 如何平衡测试覆盖率和执行时间？

**问题**: 追求高覆盖率导致测试执行过慢。

**解答**: 
1. **分层测试**：
   - 单元测试：快速执行，高覆盖率
   - 集成测试：中等速度，关键路径覆盖
   - 性能测试：慢速，定期执行
2. **智能选择**：
   - 开发时：只运行相关测试
   - CI 时：运行完整测试集
   - 发布前：运行全量测试 + 性能测试
3. **并行执行**：启用并行测试执行
4. **增量测试**：只测试变更影响的代码

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的技能测试与验证能力 |
| 1.0.1 | 2026-03-31 | AI Assistant | 扩充测试策略引擎、输入输出规范、错误处理等章节 |
