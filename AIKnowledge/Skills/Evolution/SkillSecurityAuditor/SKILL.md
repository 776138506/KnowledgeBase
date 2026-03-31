---
name: SkillSecurityAuditor
description: 技能安全审计专家，负责审计技能权限和访问控制配置、检测代码安全漏洞（注入攻击、敏感信息泄露、权限越界）、验证技能操作合规性（数据保护、隐私政策）、评估安全风险等级（低/中/高/严重）、提供安全加固建议和修复方案，适用于安全审查、合规检查、风险评估、安全加固场景
---

# 技能安全审计

## 🎯 核心目标

赋予 Agent **技能安全审计** 与 **风险评估** 的能力，使其能够：
1. 审计技能的权限和访问控制
2. 检测技能中的安全风险（敏感信息泄露、注入攻击等）
3. 验证技能操作的合规性
4. 评估技能的安全风险等级
5. 提供安全加固建议

## 🎯 适用场景

- ✅ **发布前安全检查**：技能发布前的安全审计
- ✅ **定期安全审查**：定期的技能安全审查
- ✅ **敏感操作技能审查**：涉及敏感数据或操作的技能审查
- ✅ **合规性验证**：验证技能符合安全规范
- ✅ **漏洞扫描**：扫描技能中的安全漏洞
- ✅ **安全加固**：提供安全改进建议

### 不适用场景
- ❌ 技能功能开发（应使用 development-engineer）
- ❌ 技能性能优化（应使用 SkillPerformanceOptimizer）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 核心组件

```
SkillSecurityAuditor (安全审计核心)
├── PermissionAnalyzer (权限分析器)
│   ├── AccessControlChecker (访问控制检查)
│   ├── PrivilegeValidator (权限验证)
│   └── ScopeAnalyzer (范围分析器)
├── VulnerabilityScanner (漏洞扫描器)
│   ├── InjectionDetector (注入检测)
│   ├── DataLeakDetector (数据泄露检测)
│   └── ConfigScanner (配置扫描)
├── ComplianceChecker (合规检查器)
│   ├── PolicyValidator (策略验证)
│   ├── StandardChecker (标准检查)
│   └── AuditLogger (审计日志器)
└── RiskAssessor (风险评估器)
    ├── RiskCalculator (风险计算器)
    ├── ImpactAnalyzer (影响分析)
    └── SuggestionEngine (建议引擎)
```

## 🔄 工作流程

```
权限分析 → 漏洞扫描 → 合规检查 → 风险评估 → 报告生成 → 加固建议
    ↓          ↓          ↓          ↓          ↓          ↓
[权限清单] [漏洞列表] [合规状态] [风险等级] [审计报告] [加固方案]
```

## ⚙️ 执行模式

### Mode A: 快速扫描模式
- 快速扫描常见安全问题
- 适合日常检查
- 耗时：1-3 分钟

### Mode B: 深度审计模式
- 全面深入的安全审计
- 适合发布前审查
- 耗时：10-20 分钟

### Mode C: 合规检查模式
- 验证符合特定安全标准
- 适合合规审查
- 耗时：5-15 分钟

### Mode D: 持续监控模式
- 7x24 小时安全监控
- 实时告警
- 持续运行

## 👥 安全审计策略引擎

### 漏洞检测规则

```python
def detect_vulnerabilities(skill_content):
    """
    检测技能中的安全漏洞
    """
    vulnerabilities = []
    
    # 敏感信息泄露检测
    sensitive_patterns = [
        r'password\s*=\s*["\'][^"\']+["\']',
        r'api_key\s*=\s*["\'][^"\']+["\']',
        r'secret\s*=\s*["\'][^"\']+["\']',
        r'token\s*=\s*["\'][^"\']+["\']'
    ]
    
    for pattern in sensitive_patterns:
        matches = re.findall(pattern, skill_content, re.IGNORECASE)
        if matches:
            vulnerabilities.append({
                "type": "sensitive_data_leak",
                "severity": "critical",
                "pattern": pattern,
                "matches": matches,
                "suggestion": "使用环境变量或密钥管理服务"
            })
    
    # 注入漏洞检测
    injection_patterns = [
        r'eval\s*\([^)]+\)',
        r'exec\s*\([^)]+\)',
        r'sql\s*=\s*f["\'].*\{.*\}.*["\']'
    ]
    
    for pattern in injection_patterns:
        matches = re.findall(pattern, skill_content)
        if matches:
            vulnerabilities.append({
                "type": "injection_vulnerability",
                "severity": "high",
                "pattern": pattern,
                "matches": matches,
                "suggestion": "使用参数化查询或安全的执行方式"
            })
    
    return vulnerabilities
```

### 权限分析规则

```python
def analyze_permissions(skill_definition):
    """
    分析技能的权限配置
    """
    permission_issues = []
    
    # 检查权限声明
    declared_permissions = skill_definition.get('permissions', [])
    required_permissions = extract_required_permissions(skill_definition)
    
    # 权限过多检查
    excessive_permissions = [p for p in declared_permissions if p not in required_permissions]
    if excessive_permissions:
        permission_issues.append({
            "type": "excessive_permissions",
            "severity": "medium",
            "permissions": excessive_permissions,
            "suggestion": "遵循最小权限原则，移除不需要的权限"
        })
    
    # 危险权限检查
    dangerous_permissions = ['admin', 'root', 'sudo', 'delete_all']
    for perm in declared_permissions:
        if perm in dangerous_permissions:
            permission_issues.append({
                "type": "dangerous_permission",
                "severity": "high",
                "permission": perm,
                "suggestion": "评估是否真的需要此危险权限"
            })
    
    return permission_issues
```

### 风险评估算法

```python
def calculate_risk_score(vulnerabilities, permission_issues, compliance_issues):
    """
    计算综合风险评分
    """
    # 基础分（0-100，分数越高风险越高）
    base_score = 0
    
    # 漏洞评分
    severity_weights = {
        "critical": 25,
        "high": 15,
        "medium": 8,
        "low": 3
    }
    
    for vuln in vulnerabilities:
        base_score += severity_weights.get(vuln['severity'], 0)
    
    # 权限问题评分
    for perm_issue in permission_issues:
        base_score += severity_weights.get(perm_issue['severity'], 0)
    
    # 合规问题评分
    base_score += len(compliance_issues) * 5
    
    # 归一化到 0-100
    risk_score = min(100, base_score)
    
    # 风险等级
    if risk_score >= 75:
        risk_level = "critical"
    elif risk_score >= 50:
        risk_level = "high"
    elif risk_score >= 25:
        risk_level = "medium"
    else:
        risk_level = "low"
    
    return {
        "score": risk_score,
        "level": risk_level,
        "breakdown": {
            "vulnerabilities": sum(severity_weights.get(v['severity'], 0) for v in vulnerabilities),
            "permissions": sum(severity_weights.get(p['severity'], 0) for p in permission_issues),
            "compliance": len(compliance_issues) * 5
        }
    }
```

## 📋 输入输出规范

### 输入格式

```json
{
  "skill_identifier": "类型：string，说明：技能标识名",
  "audit_config": {
    "type": "object",
    "description": "审计配置",
    "properties": {
      "audit_mode": "类型：string，说明：审计模式（quick/deep/compliance）",
      "security_standard": "类型：string，说明：安全标准（internal/iso27001/gdpr）",
      "include_dependencies": "类型：boolean，说明：是否包含依赖检查",
      "sensitive_data_patterns": "类型：array，说明：自定义敏感数据模式"
    }
  },
  "skill_content": {
    "type": "object",
    "description": "技能内容",
    "properties": {
      "source_code": "类型：string，说明：技能源代码",
      "configuration": "类型：object，说明：技能配置",
      "dependencies": "类型：array，说明：依赖列表"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "audit_summary": {
    "audit_mode": "审计模式",
    "audit_duration_seconds": "审计耗时（秒）",
    "risk_score": "风险评分（0-100）",
    "risk_level": "风险等级（critical/high/medium/low）",
    "total_issues": "问题总数",
    "critical_issues": "严重问题数",
    "high_issues": "高危问题数",
    "medium_issues": "中危问题数",
    "low_issues": "低危问题数"
  },
  "vulnerabilities": [
    {
      "id": "漏洞 ID",
      "type": "漏洞类型",
      "severity": "严重程度",
      "location": "位置（文件：行号）",
      "description": "描述",
      "evidence": "证据",
      "suggestion": "修复建议",
      "cwe_id": "CWE 编号（如果有）"
    }
  ],
  "permission_issues": [
    {
      "type": "问题类型",
      "severity": "严重程度",
      "permission": "权限名称",
      "description": "描述",
      "suggestion": "建议"
    }
  ],
  "compliance_status": {
    "standard": "安全标准",
    "compliant": "是否合规",
    "violations": [
      {
        "requirement": "要求",
        "status": "pass|fail|partial",
        "evidence": "证据",
        "remediation": "整改措施"
      }
    ]
  },
  "recommendations": [
    {
      "priority": "high|medium|low",
      "category": "类别",
      "title": "标题",
      "description": "描述",
      "effort": "工作量（low/medium/high）",
      "impact": "影响"
    }
  ]
}
```

## ✅ 质量门禁

### 审计覆盖检查

- [ ] 源代码扫描完整
- [ ] 配置文件检查完整
- [ ] 依赖关系检查完整
- [ ] 权限配置检查完整
- [ ] 合规要求覆盖完整

### 漏洞检测检查

- [ ] 严重漏洞检出率 100%
- [ ] 高危漏洞检出率>95%
- [ ] 误报率<5%
- [ ] 漏报率<2%

### 审计质量检查

- [ ] 审计结果可重现
- [ ] 证据链完整
- [ ] 建议具体可操作
- [ ] 风险评级准确

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_SCAN_FAILED | 扫描失败 | 技能内容无法解析 | 检查技能格式 |
| ERR_PATTERN_INVALID | 模式无效 | 正则表达式错误 | 修正正则表达式 |
| ERR_DEPENDENCY_CHECK_FAILED | 依赖检查失败 | 依赖无法访问 | 检查网络连接 |
| ERR_PERMISSION_DENIED | 权限不足 | 无权访问某些文件 | 获取相应权限 |
| ERR_STANDARD_NOT_FOUND | 标准不存在 | 指定的安全标准不存在 | 使用有效的标准名称 |

### 异常处理流程

```
检测到异常
    ↓
分类异常类型（可恢复/不可恢复）
    ↓
可恢复？→ 是 → 尝试自动修复
    ↓           ↓
    否      成功？→ 是 → 继续审计
    ↓           ↓
记录异常    失败 → 跳过该项，继续其他检查
    ↓
生成审计报告（包含异常说明）
```

### 重试策略

- **最大重试次数**: 2 次
- **重试条件**: 网络错误、临时故障、资源锁定
- **重试间隔**: 2 秒

## 📚 最佳实践

### 推荐做法

- ✅ **定期审计**：至少每月进行一次全面审计
- ✅ **发布前必审**：所有技能发布前必须通过安全审计
- ✅ **自动化扫描**：集成到 CI/CD 流水线
- ✅ **最小权限**：遵循最小权限原则
- ✅ **深度防御**：多层安全检查
- ✅ **及时修复**：高危问题 24 小时内修复
- ✅ **审计留痕**：保留所有审计报告

### 避免做法

- ❌ **忽视警告**：不要忽视中低危问题
- ❌ **硬编码密钥**：不要在代码中硬编码敏感信息
- ❌ **过度权限**：不要申请不必要的权限
- ❌ **跳过审计**：不要跳过安全审计
- ❌ **延迟修复**：不要延迟修复高危漏洞
- ❌ **单次审计**：不要只做一次审计

### 安全设计原则

遵循安全设计原则：
- **最小权限**：只授予必要的权限
- **深度防御**：多层安全防护
- **安全默认**：默认配置是安全的
- **完全中介**：检查所有访问
- **开放设计**：安全不依赖隐蔽性
- **权限分离**：分离关键权限
- **最小公共机制**：减少共享机制

## 🔧 配置选项

### 环境变量

```bash
# 必需配置
AUDIT_PATH=./audits
ENABLE_SECURITY_AUDIT=true

# 可选配置
DEFAULT_AUDIT_MODE=deep
SECURITY_STANDARD=internal
INCLUDE_DEPENDENCIES=true
AUTO_FIX_LOW_RISK=false
AUDIT_RETENTION_DAYS=90
LOG_LEVEL=info
```

### 配置文件

```yaml
# skill_security_auditor_config.yaml
skill_security_auditor:
  version: 1.0.0
  
  paths:
    audits: "./audits"
    reports: "./security-reports"
    
  audit:
    default_mode: "deep"
    security_standard: "internal"
    include_dependencies: true
    scan_interval_days: 30
    
  vulnerability_detection:
    enabled: true
    patterns:
      - sensitive_data
      - injection
      - hardcoded_credentials
      - insecure_config
    custom_patterns: []
    
  permission_analysis:
    enabled: true
    dangerous_permissions:
      - admin
      - root
      - sudo
      - delete_all
    require_justification: true
    
  compliance:
    standards:
      - internal
      - iso27001
      - gdpr
    auto_check: true
    
  risk_assessment:
    scoring_model: "weighted"
    thresholds:
      critical: 75
      high: 50
      medium: 25
    
  auto_remediation:
    enabled: false
    low_risk_only: false
    require_approval: true
    
  reporting:
    auto_generate: true
    formats:
      - markdown
      - json
    include_evidence: true
    include_recommendations: true
    
  logging:
    level: info
    file: "./logs/skill_security_auditor.log"
    max_size: "10MB"
    retention_days: 90
```

## 📊 监控与日志

### 日志级别

- **DEBUG**: 详细的扫描过程
- **INFO**: 关键步骤信息（开始、完成、结果）
- **WARN**: 警告信息（中低危问题）
- **ERROR**: 错误信息（高危问题、审计失败）
- **CRITICAL**: 严重问题（严重漏洞）

### 关键指标

| 指标名称 | 说明 | 告警阈值 |
|---------|------|---------|
| 审计覆盖率 | 已审计技能比例 | < 90% |
| 高危问题数 | 高危漏洞数量 | > 0 |
| 平均风险评分 | 所有技能平均风险分 | > 30 |
| 修复率 | 问题修复比例 | < 80% |
| 审计及时率 | 按时审计比例 | < 95% |

### 安全仪表板示例

```
技能安全监控仪表板
=====================================
安全概览:
- 总技能数：50
- 已审计：48 (96%)
- 平均风险分：22 (低)
- 高危问题：0

风险分布:
- 严重风险：0 个技能
- 高风险：2 个技能
- 中风险：8 个技能
- 低风险：40 个技能

问题统计:
- 严重问题：0
- 高危问题：3
- 中危问题：15
- 低危问题：42

Top 风险技能:
1. LegacyAPI (风险分：68，高)
2. OldComponent (风险分：55，高)
3. DataProcessor (风险分：42，中)

趋势:
- 风险技能数：↓ 下降 2 个
- 平均风险分：↓ 下降 5 分
- 修复率：↑ 提升至 85%

告警:
- ⚠️ 2 个技能存在高危漏洞
- ⚠️ LegacyAPI 包含硬编码密钥
```

## 🧪 测试用例

### 单元测试

#### 测试用例 1：敏感信息检测

```yaml
输入:
  skill_content: |
    password = "secret123"
    api_key = "sk-1234567890"
预期输出:
  vulnerabilities_count: 2
  severity: "critical"
  types: ["sensitive_data_leak"]
结果: ✅ 通过
```

#### 测试用例 2：注入漏洞检测

```yaml
输入:
  skill_content: |
    def execute(code):
        eval(code)
预期输出:
  vulnerabilities_count: 1
  severity: "high"
  types: ["injection_vulnerability"]
结果: ✅ 通过
```

#### 测试用例 3：权限分析

```yaml
输入:
  skill_definition:
    permissions: ["read", "write", "admin", "delete"]
    required: ["read", "write"]
预期输出:
  permission_issues_count: 1
  excessive_permissions: ["admin", "delete"]
结果: ✅ 通过
```

### 集成测试

#### 测试场景 1：完整安全审计

**测试步骤**:
1. 加载技能内容和配置
2. 执行漏洞扫描
3. 执行权限分析
4. 执行合规检查
5. 计算风险评分
6. 生成审计报告

**预期结果**: 
- 审计执行成功
- 所有检查完成
- 风险评分准确
- 报告完整

### 测试覆盖率要求

- 漏洞检测覆盖率：≥ 95%
- 权限分析覆盖率：100%
- 合规检查覆盖率：≥ 90%
- 场景覆盖率：≥ 85%

## 📖 示例

### 示例 1：发布前安全审计

**场景**: 新技能发布前的全面安全审计

**执行命令**:
```bash
skill-security-auditor audit --skill=CodeReviewer --mode=deep --standard=internal
```

**审计报告**:
```markdown
# 安全审计报告

## 审计信息
- **技能**: CodeReviewer v1.0.0
- **审计模式**: 深度审计
- **安全标准**: Internal Security Standard v2.0
- **审计时间**: 2026-03-31 14:30:00
- **审计耗时**: 12.5 秒

## 审计结果

### 风险评分
- **风险评分**: 18/100 (低风险) ✅
- **风险等级**: Low

### 问题统计
- **严重问题**: 0
- **高危问题**: 0
- **中危问题**: 2
- **低危问题**: 3

## 详细发现

### 中危问题

#### 1. 缺少输入验证
- **位置**: src/reviewer.py:45
- **类型**: input_validation
- **描述**: 函数 `analyze_code` 未验证输入参数
- **证据**: `def analyze_code(code):` 直接处理未验证的输入
- **建议**: 添加输入验证逻辑，检查 code 参数格式和长度
- **CWE**: CWE-20 (Improper Input Validation)

#### 2. 错误消息泄露内部信息
- **位置**: src/errors.py:23
- **类型**: information_disclosure
- **描述**: 异常处理泄露堆栈追踪
- **证据**: `return f"Error: {str(e)} at {traceback.format_exc()}"`
- **建议**: 使用通用错误消息，记录详细错误到日志
- **CWE**: CWE-209 (Information Exposure Through Stack Trace)

### 低危问题

#### 1. 缺少安全文档
- **类型**: documentation
- **描述**: 技能缺少安全使用说明
- **建议**: 添加 SECURITY.md 文件

#### 2. 审计日志不完整
- **类型**: logging
- **描述**: 部分操作未记录审计日志
- **建议**: 补充关键操作的审计日志

#### 3. 依赖版本过旧
- **类型**: dependency
- **描述**: requests 库版本为 2.25.1，存在已知漏洞
- **建议**: 升级到 2.31.0 或更高版本

## 合规状态

### Internal Security Standard v2.0
- **合规状态**: ✅ 合规
- **通过项**: 15/17
- **部分通过**: 2/17

## 修复建议

### 高优先级
1. 添加输入验证逻辑（预计 2 小时）
2. 修复错误消息泄露（预计 1 小时）

### 中优先级
3. 补充安全文档（预计 1 小时）
4. 完善审计日志（预计 2 小时）

### 低优先级
5. 升级依赖版本（预计 0.5 小时）

## 结论
✅ **技能可以通过安全审计**

该技能整体安全风险较低，发现的问题均为中低危，建议在下一个版本中修复。无阻碍发布的严重或高危问题。
```

### 示例 2：定期安全审查

**场景**: 月度技能库安全审查

**执行命令**:
```bash
skill-security-auditor scan --scope=all --mode=quick
```

**审查结果**:
```markdown
# 月度安全审查报告

## 审查范围
- **审查时间**: 2026-03-01 至 2026-03-31
- **审查技能数**: 50
- **审查模式**: 快速扫描

## 整体状况

### 风险分布
- 🟢 低风险：40 个技能 (80%)
- 🟡 中风险：8 个技能 (16%)
- 🟠 高风险：2 个技能 (4%)
- 🔴 严重风险：0 个技能 (0%)

### 问题趋势
- 新增问题：12 个
- 修复问题：18 个
- 净减少：6 个

## 需要关注的技能

### 1. LegacyAPI (高风险)
- **风险评分**: 68/100
- **主要问题**: 硬编码 API 密钥
- **负责人**: @developer1
- **状态**: 修复中
- **截止日期**: 2026-04-07

### 2. OldComponent (高风险)
- **风险评分**: 55/100
- **主要问题**: 使用有漏洞的依赖
- **负责人**: @developer2
- **状态**: 待修复
- **截止日期**: 2026-04-07

## 行动项
1. ⚠️ 高风险技能需在 7 天内修复
2. 📋 所有中危问题需在 30 天内修复
3. 🔄 下月审查重点关注依赖漏洞
```

### 示例 3：合规性检查

**场景**: GDPR 合规性验证

**执行命令**:
```bash
skill-security-auditor compliance --skill=DataProcessor --standard=gdpr
```

**合规报告**:
```markdown
# GDPR 合规性报告

## 技能信息
- **技能**: DataProcessor v2.1.0
- **标准**: GDPR (General Data Protection Regulation)
- **检查时间**: 2026-03-31

## 合规状态
- **整体合规**: ⚠️ 部分合规
- **通过项**: 8/10
- **失败项**: 1/10
- **部分通过**: 1/10

## 详细检查结果

### ✅ 通过项

1. **数据最小化** (Article 5(1)(c))
   - 状态：通过
   - 证据：技能仅收集必要的数据字段

2. **目的限制** (Article 5(1)(b))
   - 状态：通过
   - 证据：数据处理目的明确声明

3. **准确性** (Article 5(1)(d))
   - 状态：通过
   - 证据：提供数据校正功能

4. **存储限制** (Article 5(1)(e))
   - 状态：通过
   - 证据：实现数据自动删除机制

5. **完整性和保密性** (Article 5(1)(f))
   - 状态：通过
   - 证据：使用加密传输和存储

### ❌ 失败项

1. **同意管理** (Article 7)
   - 状态：失败
   - 问题：未实现用户同意撤回机制
   - 证据：缺少 `withdraw_consent()` 功能
   - 整改：添加同意撤回功能

### ⚠️ 部分通过

1. **数据可携权** (Article 20)
   - 状态：部分通过
   - 问题：支持导出但不支持常用格式
   - 证据：仅支持 JSON，不支持 CSV/XML
   - 整改：添加 CSV 和 XML 导出格式

## 整改计划

### 高优先级（1 个月内）
1. 实现同意撤回功能
   - 工作量：3 天
   - 负责人：@developer1

### 中优先级（3 个月内）
2. 添加 CSV/XML 导出格式
   - 工作量：2 天
   - 负责人：@developer2

## 结论
⚠️ **需要整改后才能完全合规**

当前技能在大部分 GDPR 要求上合规，但存在 1 项失败和 1 项部分通过。建议在 1 个月内完成高优先级整改，3 个月内完成所有整改。
```

## 🔗 相关资源

### 前置技能
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析
- [SkillDeployment](../SkillDeployment/SKILL.md) - 技能部署与发布

### 后续技能
- [SkillPerformanceOptimizer](../SkillPerformanceOptimizer/SKILL.md) - 技能性能优化器
- [SkillConflictResolver](../SkillConflictResolver/SKILL.md) - 技能冲突检测与解决

### 参考资料
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [CWE/SANS Top 25](https://cwe.mitre.org/top25/)
- [GDPR 官方文本](https://gdpr.eu/)
- [ISO 27001 标准](https://www.iso.org/isoiec-27001-information-security.html)
- [安全编码最佳实践](链接)

### 工具依赖
- [Bandit](https://bandit.readthedocs.io/) - Python 安全扫描
- [Safety](https://pyup.io/safety/) - 依赖漏洞扫描
- [Semgrep](https://semgrep.dev/) - 代码模式扫描

## ❓ FAQ

### Q1: 如何处理误报？

**问题**: 安全扫描报告了误报，如何处理？

**解答**: 
1. **验证误报**: 手动检查确认是误报
2. **记录原因**: 在审计报告中记录误报原因
3. **调整规则**: 优化检测规则减少误报
4. **添加白名单**: 将误报模式加入白名单

**示例**:
```yaml
# 白名单配置
false_positive_whitelist:
  - pattern: "password = \"example\""
    reason: "示例代码中的示例密码"
    files: ["examples/*.py"]
```

### Q2: 如何优先修复安全问题？

**问题**: 发现很多安全问题，如何确定修复优先级？

**解答**: 
1. **按严重程度**: 严重 > 高危 > 中危 > 低危
2. **按影响范围**: 影响用户数多的优先
3. **按利用难度**: 容易利用的优先
4. **按合规要求**: 合规相关的优先

**优先级矩阵**:
```
严重程度 × 影响范围 = 优先级
- 严重 × 广泛 = P0（立即修复）
- 高危 × 中等 = P1（24 小时内）
- 中危 × 局部 = P2（7 天内）
- 低危 × 个别 = P3（30 天内）
```

### Q3: 如何平衡安全和开发效率？

**问题**: 安全检查影响开发效率，如何平衡？

**解答**: 
1. **分层检查**: 
   - 开发时：快速扫描（1-2 分钟）
   - CI 时：全面扫描（5-10 分钟）
   - 发布前：深度审计（10-20 分钟）
2. **自动化**: 集成到 CI/CD，减少人工干预
3. **左移安全**: 在开发早期发现问题，降低修复成本
4. **智能建议**: 提供具体的修复建议和代码示例

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的安全审计能力 |
| 1.0.1 | 2026-03-31 | AI Assistant | 扩充安全审计策略引擎、输入输出规范、错误处理等章节 |
