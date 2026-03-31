---
name: 技能文档生成器
identifier: SkillDocGenerator
version: 1.0.0
type: meta-skill
status: 🟢 稳定
created: 2026-03-31
updated: 2026-03-31
author: AI Assistant
tags:
  - 文档生成
  - 自动化文档
  - 技能文档
  - 元技能
  - 文档管理
---

# 技能文档生成器

## 📋 基本信息

| 属性 | 值 |
|------|-----|
| **中文名称** | 技能文档生成器 |
| **英文标识名** | `SkillDocGenerator` |
| **版本号** | 1.0.0 |
| **类型** | Meta-Skill（元技能） |
| **状态** | 🟢 稳定 |
| **创建日期** | 2026-03-31 |
| **最后更新** | 2026-03-31 |
| **维护者** | AI Assistant |

## 🎯 核心目标

赋予 Agent **技能文档自动生成** 的能力，使其能够：
1. 从技能定义自动生成 API 文档
2. 生成技能使用示例和教程
3. 支持多语言文档生成
4. 文档版本管理和同步更新
5. 生成交互式文档和演示

## 🎯 适用场景

- ✅ **API 文档生成**：从技能定义生成 API 文档
- ✅ **使用示例生成**：自动生成使用示例
- ✅ **多语言文档**：生成多语言版本文档
- ✅ **文档更新**：技能更新时同步更新文档
- ✅ **教程生成**：生成技能使用教程
- ✅ **交互式文档**：生成可交互的文档

### 不适用场景
- ❌ 技能功能开发（应使用 development-engineer）
- ❌ 技能内容编写（应使用 documentation-engineer）
- ❌ 技能质量审查（应使用 SkillQualityGate）

## 🏗️ 技能架构

### 核心组件

```
SkillDocGenerator (文档生成核心)
├── APIDocGenerator (API 文档生成器)
│   ├── SchemaExtractor (模式提取器)
│   ├── EndpointGenerator (端点生成器)
│   └── ExampleGenerator (示例生成器)
├── TutorialGenerator (教程生成器)
│   ├── GettingStartedGenerator (入门生成器)
│   ├── AdvancedGuideGenerator (进阶指南生成)
│   └── BestPracticeGenerator (最佳实践生成)
├── MultiLangGenerator (多语言生成器)
│   ├── TranslationEngine (翻译引擎)
│   ├── LocalizationManager (本地化管理)
│   └── CultureAdapter (文化适配器)
└── VersionManager (版本管理器)
    ├── DocVersioning (版本文档化)
    ├── ChangeTracker (变更追踪)
    └── SyncManager (同步管理器)
```

## 🧠 策略引擎

### 文档生成策略

```python
def generate_api_doc(skill_definition):
    """生成 API 文档"""
    # 提取基本信息
    basic_info = {
        'name': skill_definition['name'],
        'identifier': skill_definition['identifier'],
        'version': skill_definition['version'],
        'description': skill_definition.get('description', '')
    }
    
    # 提取工具和方法
    tools = extract_tools(skill_definition)
    methods = []
    for tool in tools:
        method = {
            'name': tool['name'],
            'parameters': extract_parameters(tool),
            'returns': extract_returns(tool),
            'examples': generate_examples(tool),
            'errors': extract_errors(tool)
        }
        methods.append(method)
    
    # 生成文档结构
    doc = {
        'title': f"{basic_info['name']} API 文档",
        'basic_info': basic_info,
        'methods': methods,
        'examples': generate_usage_examples(methods),
        'related_skills': extract_related_skills(skill_definition)
    }
    
    return doc

def extract_tools(skill_definition):
    """从技能定义中提取工具信息"""
    tools = []
    # 从 tools 字段提取
    if 'tools' in skill_definition:
        for tool in skill_definition['tools']:
            tools.append({
                'name': tool.get('name', ''),
                'description': tool.get('description', ''),
                'parameters': tool.get('parameters', {}),
                'returns': tool.get('returns', {})
            })
    # 从代码中分析
    if 'code' in skill_definition:
        tools.extend(analyze_code_for_tools(skill_definition['code']))
    return tools

def generate_examples(tool_info):
    """生成使用示例"""
    examples = []
    # 基础调用示例
    basic_example = {
        'type': 'basic',
        'title': '基础用法',
        'code': generate_basic_call(tool_info)
    }
    examples.append(basic_example)
    
    # 高级示例
    if tool_info['parameters']:
        advanced_example = {
            'type': 'advanced',
            'title': '高级用法',
            'code': generate_advanced_call(tool_info)
        }
        examples.append(advanced_example)
    
    # 错误处理示例
    error_example = {
        'type': 'error_handling',
        'title': '错误处理',
        'code': generate_error_handling_example(tool_info)
    }
    examples.append(error_example)
    
    return examples
```

### 教程生成策略

```python
def generate_tutorial(skill_definition, tutorial_type='getting_started'):
    """生成教程文档"""
    if tutorial_type == 'getting_started':
        return generate_getting_started(skill_definition)
    elif tutorial_type == 'advanced':
        return generate_advanced_guide(skill_definition)
    elif tutorial_type == 'best_practices':
        return generate_best_practices(skill_definition)
    else:
        raise ValueError(f"Unknown tutorial type: {tutorial_type}")

def generate_getting_started(skill_definition):
    """生成入门教程"""
    tutorial = {
        'title': f"{skill_definition['name']} 入门指南",
        'prerequisites': get_prerequisites(skill_definition),
        'steps': []
    }
    
    # 步骤 1: 安装/配置
    tutorial['steps'].append({
        'step': 1,
        'title': '安装与配置',
        'content': '介绍如何安装和配置技能',
        'code_examples': get_setup_examples(skill_definition)
    })
    
    # 步骤 2: 第一个用例
    tutorial['steps'].append({
        'step': 2,
        'title': '第一个用例',
        'content': '通过简单示例快速上手',
        'code_examples': get_hello_world_example(skill_definition)
    })
    
    # 步骤 3: 核心功能
    tutorial['steps'].append({
        'step': 3,
        'title': '核心功能',
        'content': '学习技能的核心功能',
        'code_examples': get_core_feature_examples(skill_definition)
    })
    
    # 步骤 4: 下一步
    tutorial['steps'].append({
        'step': 4,
        'title': '下一步',
        'content': '进阶学习资源推荐',
        'resources': get_advanced_resources(skill_definition)
    })
    
    return tutorial

def generate_best_practices(skill_definition):
    """生成最佳实践"""
    practices = {
        'title': f"{skill_definition['name']} 最佳实践",
        'categories': []
    }
    
    # 性能优化
    practices['categories'].append({
        'category': '性能优化',
        'practices': get_performance_best_practices(skill_definition)
    })
    
    # 安全建议
    practices['categories'].append({
        'category': '安全建议',
        'practices': get_security_best_practices(skill_definition)
    })
    
    # 代码组织
    practices['categories'].append({
        'category': '代码组织',
        'practices': get_code_organization_tips(skill_definition)
    })
    
    # 常见陷阱
    practices['categories'].append({
        'category': '常见陷阱',
        'practices': get_common_pitfalls(skill_definition)
    })
    
    return practices
```

### 多语言翻译策略

```python
def translate_document(doc, target_languages):
    """翻译文档到多种语言"""
    translations = {}
    
    for lang in target_languages:
        # 翻译内容
        translated_content = translate_content(doc, lang)
        
        # 本地化调整
        localized = localize_content(translated_content, lang)
        
        # 文化适配
        adapted = adapt_to_culture(localized, lang)
        
        translations[lang] = {
            'content': adapted,
            'metadata': {
                'language': lang,
                'translated_at': datetime.now().isoformat(),
                'translation_quality': 'auto'  # 可标记为自动翻译
            }
        }
    
    return translations

def translate_content(doc, target_lang):
    """翻译文档内容"""
    # 使用翻译 API 或本地模型
    translation_engine = get_translation_engine()
    
    # 翻译标题
    translated_title = translation_engine.translate(
        doc['title'], 
        target_lang=target_lang
    )
    
    # 翻译正文
    translated_body = {}
    for section_name, section_content in doc.items():
        if section_name != 'title':
            translated_body[section_name] = translation_engine.translate(
                section_content,
                target_lang=target_lang
            )
    
    return {
        'title': translated_title,
        **translated_body
    }

def localize_content(doc, lang):
    """本地化内容调整"""
    # 日期格式
    if 'date' in doc:
        doc['date'] = format_date_for_locale(doc['date'], lang)
    
    # 代码示例中的注释翻译
    if 'code_examples' in doc:
        for example in doc['code_examples']:
            example['comments'] = translate_comments(example['comments'], lang)
    
    # 术语表映射
    if 'terms' in doc:
        doc['terms'] = map_terms_to_local(doc['terms'], lang)
    
    return doc
```

### 版本管理策略

```python
def manage_doc_versions(skill_definition, existing_docs):
    """管理版本文档"""
    current_version = skill_definition['version']
    new_docs = generate_all_docs(skill_definition)
    
    version_history = []
    
    for doc_type, new_doc in new_docs.items():
        # 检查是否有变更
        if doc_type in existing_docs:
            old_doc = existing_docs[doc_type]
            changes = detect_changes(old_doc, new_doc)
            
            if changes:
                # 版本更新
                version_entry = {
                    'version': current_version,
                    'date': datetime.now().isoformat(),
                    'doc_type': doc_type,
                    'changes': changes,
                    'status': 'updated'
                }
                version_history.append(version_entry)
                
                # 保留旧版本
                archive_old_version(old_doc, doc_type)
                
                # 更新为新版本
                update_doc_version(new_doc, doc_type, current_version)
        else:
            # 新文档
            version_entry = {
                'version': current_version,
                'date': datetime.now().isoformat(),
                'doc_type': doc_type,
                'changes': ['初始创建'],
                'status': 'created'
            }
            version_history.append(version_entry)
    
    return {
        'new_docs': new_docs,
        'version_history': version_history
    }

def detect_changes(old_doc, new_doc):
    """检测文档变更"""
    changes = []
    
    # 比较文本内容
    if old_doc.get('content') != new_doc.get('content'):
        changes.append('内容更新')
    
    # 比较示例代码
    if old_doc.get('examples') != new_doc.get('examples'):
        changes.append('示例代码更新')
    
    # 比较参数
    if old_doc.get('parameters') != new_doc.get('parameters'):
        changes.append('参数变更')
    
    return changes
```

## 🔄 工作流程

```
技能分析 → 内容提取 → 模板匹配 → 文档生成 → 多语言翻译 → 版本同步 → 发布
    ↓          ↓          ↓          ↓          ↓          ↓          ↓
[解析技能] [提取信息] [选择模板] [生成文档] [翻译文档] [更新版本] [发布文档]
```

## 📥📤 输入输出规范

### 输入规范

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "SkillDocGenerator Input Schema",
  "type": "object",
  "required": ["skill_definition", "generation_type"],
  "properties": {
    "skill_definition": {
      "type": "object",
      "description": "技能定义对象",
      "required": ["name", "identifier", "version"],
      "properties": {
        "name": {
          "type": "string",
          "description": "技能中文名称"
        },
        "identifier": {
          "type": "string",
          "description": "技能英文标识名"
        },
        "version": {
          "type": "string",
          "description": "技能版本号"
        },
        "description": {
          "type": "string",
          "description": "技能描述"
        },
        "tools": {
          "type": "array",
          "description": "工具列表",
          "items": {
            "type": "object"
          }
        },
        "code": {
          "type": "string",
          "description": "技能代码"
        }
      }
    },
    "generation_type": {
      "type": "string",
      "enum": ["api", "tutorial", "best_practices", "multi_lang", "all"],
      "description": "生成类型"
    },
    "target_languages": {
      "type": "array",
      "description": "目标语言列表",
      "items": {
        "type": "string"
      },
      "default": ["zh"]
    },
    "output_format": {
      "type": "string",
      "enum": ["markdown", "html", "pdf", "all"],
      "default": "markdown"
    },
    "template": {
      "type": "string",
      "description": "文档模板名称"
    },
    "options": {
      "type": "object",
      "properties": {
        "include_examples": {
          "type": "boolean",
          "default": true
        },
        "include_diagrams": {
          "type": "boolean",
          "default": false
        },
        "auto_translate": {
          "type": "boolean",
          "default": false
        }
      }
    }
  }
}
```

### 输出规范

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "SkillDocGenerator Output Schema",
  "type": "object",
  "properties": {
    "status": {
      "type": "string",
      "enum": ["success", "partial", "failed"]
    },
    "generated_docs": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "doc_type": {
            "type": "string",
            "enum": ["api", "tutorial", "best_practices", "translation"]
          },
          "file_path": {
            "type": "string",
            "description": "生成的文件路径"
          },
          "language": {
            "type": "string",
            "default": "zh"
          },
          "word_count": {
            "type": "integer",
            "description": "文档字数"
          },
          "sections": {
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      }
    },
    "version_info": {
      "type": "object",
      "properties": {
        "skill_version": {
          "type": "string"
        },
        "doc_version": {
          "type": "string"
        },
        "changes": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      }
    },
    "quality_metrics": {
      "type": "object",
      "properties": {
        "completeness_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100
        },
        "accuracy_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100
        },
        "readability_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100
        }
      }
    },
    "errors": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "error_code": {
            "type": "string"
          },
          "message": {
            "type": "string"
          },
          "severity": {
            "type": "string",
            "enum": ["low", "medium", "high", "critical"]
          }
        }
      }
    },
    "execution_time": {
      "type": "number",
      "description": "执行时间（秒）"
    }
  }
}
```

## ⚙️ 执行模式

### Mode A: API 文档模式
- 生成 API 参考文档
- 包含参数说明
- 耗时：2-5 分钟

### Mode B: 教程生成模式
- 生成使用教程
- 包含示例代码
- 耗时：5-10 分钟

### Mode C: 多语言模式
- 生成多版本文档
- 支持多种语言
- 耗时：10-20 分钟

### Mode D: 全量生成模式
- 生成所有文档
- API+ 教程 + 多语言
- 耗时：15-30 分钟

## 🛡️ 质量门禁

### 生成质量检查

| 检查项 | 检查规则 | 通过标准 | 验证方法 |
|--------|---------|---------|---------|
| **完整性检查** | 所有必需章节已生成 | 完整性得分 ≥ 90% | 章节覆盖率统计 |
| **准确性检查** | API 参数与定义一致 | 准确率 = 100% | 参数对比验证 |
| **示例可运行** | 所有代码示例可执行 | 可运行率 ≥ 95% | 自动化测试 |
| **术语一致性** | 全文术语使用一致 | 术语一致率 ≥ 98% | 术语表检查 |
| **格式规范性** | Markdown 格式正确 | 无格式错误 | Markdown 验证器 |
| **链接有效性** | 所有内部链接有效 | 有效链接率 = 100% | 链接检查器 |
| **翻译质量** | 多语言翻译准确 | 翻译准确率 ≥ 90% | 人工抽检 |
| **版本同步** | 文档版本与技能版本一致 | 版本匹配率 = 100% | 版本号对比 |

### 质量评分计算

```python
def calculate_quality_score(generated_doc):
    """计算文档质量评分"""
    scores = {}
    
    # 完整性评分（30% 权重）
    completeness = calculate_completeness(generated_doc)
    scores['completeness'] = completeness * 0.3
    
    # 准确性评分（35% 权重）
    accuracy = calculate_accuracy(generated_doc)
    scores['accuracy'] = accuracy * 0.35
    
    # 可读性评分（20% 权重）
    readability = calculate_readability(generated_doc)
    scores['readability'] = readability * 0.2
    
    # 规范性评分（15% 权重）
    standardization = calculate_standardization(generated_doc)
    scores['standardization'] = standardization * 0.15
    
    # 总分
    total_score = sum(scores.values())
    
    return {
        'total_score': total_score,
        'breakdown': scores,
        'level': '优秀' if total_score >= 90 else '良好' if total_score >= 80 else '合格' if total_score >= 70 else '需改进'
    }

def calculate_completeness(doc):
    """计算完整性得分"""
    required_sections = ['基本信息', '方法说明', '参数说明', '返回值', '示例', '错误码']
    present_sections = [section for section in required_sections if section in doc]
    return len(present_sections) / len(required_sections) * 100

def calculate_accuracy(doc):
    """计算准确性得分"""
    # 检查参数准确性
    param_accuracy = check_parameter_accuracy(doc)
    # 检查示例准确性
    example_accuracy = check_example_accuracy(doc)
    # 检查错误码准确性
    error_accuracy = check_error_code_accuracy(doc)
    
    return (param_accuracy * 0.4 + example_accuracy * 0.4 + error_accuracy * 0.2)

def calculate_readability(doc):
    """计算可读性得分"""
    # 句子长度分析
    avg_sentence_length = calculate_avg_sentence_length(doc)
    length_score = max(0, 100 - (avg_sentence_length - 20) * 2)
    
    # 段落结构
    structure_score = evaluate_paragraph_structure(doc)
    
    # 代码注释
    comment_score = evaluate_code_comments(doc)
    
    return length_score * 0.4 + structure_score * 0.3 + comment_score * 0.3
```

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 可能原因 | 解决方案 |
|---------|---------|---------|---------|
| `ERR_SKILL_NOT_FOUND` | 技能定义不存在 | 技能文件路径错误或技能未创建 | 检查技能路径，确认技能已创建 |
| `ERR_INVALID_SKILL_FORMAT` | 技能定义格式无效 | 技能定义 JSON/YAML 格式错误 | 验证技能定义格式，修复语法错误 |
| `ERR_MISSING_REQUIRED_FIELD` | 缺少必需字段 | 技能定义缺少 name/identifier 等必需字段 | 补充缺失的必需字段 |
| `ERR_TEMPLATE_NOT_FOUND` | 文档模板不存在 | 指定模板不存在或未安装 | 使用默认模板或安装指定模板 |
| `ERR_TRANSLATION_FAILED` | 翻译失败 | 翻译 API 不可用或配额用尽 | 检查 API 连接，或使用本地翻译 |
| `ERR_CODE_EXTRACTION_FAILED` | 代码提取失败 | 技能代码无法解析或格式错误 | 检查代码语法，确保代码可解析 |
| `ERR_OUTPUT_WRITE_FAILED` | 输出写入失败 | 输出目录无权限或磁盘空间不足 | 检查目录权限和磁盘空间 |
| `ERR_VERSION_CONFLICT` | 版本冲突 | 版本文档已存在且未解决冲突 | 手动解决版本冲突或备份旧版本 |
| `ERR_QUALITY_CHECK_FAILED` | 质量检查失败 | 生成文档未通过质量门禁 | 根据质量报告修复文档问题 |
| `ERR_TIMEOUT` | 生成超时 | 文档生成时间超过限制 | 增加超时限制或分批生成 |

### 异常处理流程

```python
def generate_with_error_handling(skill_definition, options):
    """带错误处理的文档生成"""
    try:
        # 验证输入
        validation_result = validate_input(skill_definition)
        if not validation_result['valid']:
            raise ValidationError(validation_result['errors'])
        
        # 生成文档
        generated_doc = generate_document(skill_definition, options)
        
        # 质量检查
        quality_result = quality_check(generated_doc)
        if quality_result['score'] < 70:
            raise QualityCheckFailed(quality_result['issues'])
        
        # 写入输出
        write_output(generated_doc, options['output_path'])
        
        return {
            'status': 'success',
            'doc': generated_doc,
            'quality_score': quality_result['score']
        }
        
    except ValidationError as e:
        return {
            'status': 'failed',
            'error_code': 'ERR_VALIDATION_FAILED',
            'message': str(e),
            'details': e.errors
        }
    
    except QualityCheckFailed as e:
        return {
            'status': 'failed',
            'error_code': 'ERR_QUALITY_CHECK_FAILED',
            'message': '文档质量检查未通过',
            'details': e.issues
        }
    
    except Exception as e:
        return {
            'status': 'failed',
            'error_code': 'ERR_UNKNOWN',
            'message': str(e)
        }
```

## 🚀 快速开始

```bash
# 生成 API 文档
skill-doc-generator generate --skill=SkillName --type=api

# 生成教程
skill-doc-generator generate --skill=SkillName --type=tutorial

# 生成多语言文档
skill-doc-generator generate --skill=SkillName --langs=en,zh,es

# 全量生成
skill-doc-generator generate --skill=SkillName --type=all
```

## 💡 最佳实践

### 推荐做法

1. **增量生成**
   - ✅ 先生成 API 文档，再生成教程
   - ✅ 先生成中文版，再翻译其他语言
   - ✅ 每次技能更新后及时更新文档
   - ✅ 使用版本控制管理文档变更

2. **质量保证**
   - ✅ 始终运行质量检查
   - ✅ 人工审核自动生成的内容
   - ✅ 定期更新文档模板
   - ✅ 建立文档审查流程

3. **示例代码**
   - ✅ 提供完整可运行的示例
   - ✅ 包含错误处理示例
   - ✅ 使用真实场景数据
   - ✅ 添加详细注释说明

4. **多语言支持**
   - ✅ 优先保证英文和中文质量
   - ✅ 使用专业翻译服务
   - ✅ 考虑文化差异
   - ✅ 本地化术语表

5. **版本管理**
   - ✅ 文档版本与技能版本严格对应
   - ✅ 保留历史版本文档
   - ✅ 清晰标注版本变更
   - ✅ 提供版本迁移指南

### 避免做法

1. **生成质量**
   - ❌ 完全依赖自动生成不审核
   - ❌ 忽略质量检查报告
   - ❌ 使用过期的文档模板
   - ❌ 文档与代码不同步

2. **示例代码**
   - ❌ 提供无法运行的伪代码
   - ❌ 缺少必要的错误处理
   - ❌ 使用敏感数据作为示例
   - ❌ 示例过于简单无实际价值

3. **多语言**
   - ❌ 机器翻译后不校对
   - ❌ 忽略本地化习惯
   - ❌ 术语翻译不一致
   - ❌ 文化不敏感的表述

4. **版本管理**
   - ❌ 版本对应关系混乱
   - ❌ 删除旧版本文档
   - ❌ 不标注破坏性变更
   - ❌ 缺少升级指南

## ⚙️ 配置选项

### 基本配置

```yaml
# config.yaml
doc_generator:
  # 输出配置
  output:
    base_path: ./docs
    format: markdown  # markdown, html, pdf
    organize_by: version  # version, type, language
  
  # 生成配置
  generation:
    include_examples: true
    include_diagrams: false
    auto_translate: false
    quality_threshold: 80
  
  # 模板配置
  template:
    api_doc: templates/api_doc.md
    tutorial: templates/tutorial.md
    best_practices: templates/best_practices.md
  
  # 翻译配置
  translation:
    engine: google  # google, deepl, local
    auto_approve: false
    review_required: true
  
  # 版本配置
  versioning:
    enabled: true
    archive_old_versions: true
    max_versions_to_keep: 5
```

### 高级配置

```yaml
# advanced_config.yaml
advanced:
  # 性能优化
  performance:
    parallel_generation: true
    max_workers: 4
    cache_enabled: true
    cache_ttl: 3600
  
  # 质量增强
  quality_enhancement:
    grammar_check: true
    spell_check: true
    style_check: true
    link_check: true
  
  # 自定义规则
  custom_rules:
    - name: require_security_section
      description: 必须包含安全说明章节
      enabled: true
    
    - name: require_code_examples
      description: 每个方法必须有代码示例
      enabled: true
    
    - name: max_example_length
      description: 示例代码不超过 50 行
      params:
        max_lines: 50
      enabled: true
  
  # 通知配置
  notifications:
    on_success: false
    on_failure: true
    on_quality_warning: true
    channels:
      - type: email
        recipients: [docs@example.com]
      - type: slack
        webhook: https://hooks.slack.com/xxx
```

## 📊 监控与日志

### 监控指标

| 指标名称 | 描述 | 告警阈值 | 监控频率 |
|---------|------|---------|---------|
| `doc_generation_count` | 文档生成次数 | - | 实时 |
| `doc_generation_duration` | 生成耗时 | > 30 分钟 | 每次生成 |
| `quality_score_avg` | 平均质量评分 | < 80 | 每天 |
| `error_rate` | 生成失败率 | > 5% | 每小时 |
| `translation_accuracy` | 翻译准确率 | < 90% | 每周 |
| `version_sync_rate` | 版本同步率 | < 100% | 每次技能更新 |
| `user_satisfaction` | 用户满意度 | < 4.0/5.0 | 每周 |

### 日志格式

```json
{
  "timestamp": "2026-03-31T12:00:00Z",
  "level": "INFO",
  "event": "doc_generation_started",
  "skill_name": "SkillDeployment",
  "generation_type": "api",
  "options": {
    "include_examples": true,
    "output_format": "markdown"
  },
  "trace_id": "abc123"
}
```

### 日志分析

```python
def analyze_generation_logs(logs):
    """分析生成日志"""
    metrics = {
        'total_generations': 0,
        'successful': 0,
        'failed': 0,
        'avg_duration': 0,
        'quality_scores': [],
        'common_errors': {}
    }
    
    for log in logs:
        if log['event'] == 'doc_generation_completed':
            metrics['total_generations'] += 1
            if log['status'] == 'success':
                metrics['successful'] += 1
                metrics['quality_scores'].append(log['quality_score'])
            else:
                metrics['failed'] += 1
                error = log.get('error_code', 'UNKNOWN')
                metrics['common_errors'][error] = metrics['common_errors'].get(error, 0) + 1
            
            metrics['avg_duration'] += log['duration']
    
    # 计算平均值
    if metrics['total_generations'] > 0:
        metrics['avg_duration'] /= metrics['total_generations']
        metrics['avg_quality_score'] = sum(metrics['quality_scores']) / len(metrics['quality_scores'])
    
    return metrics
```

## ✅ 文档质量标准

### API 文档
- [ ] 参数说明完整
- [ ] 返回值说明清晰
- [ ] 示例可运行
- [ ] 错误码完整

### 教程文档
- [ ] 步骤清晰
- [ ] 示例丰富
- [ ] 截图/图表辅助
- [ ] 常见问题解答

### 多语言文档
- [ ] 翻译准确
- [ ] 本地化适当
- [ ] 文化敏感
- [ ] 术语一致

## 🧪 测试用例

### 单元测试

```python
def test_api_doc_generation():
    """测试 API 文档生成"""
    skill_def = {
        'name': '测试技能',
        'identifier': 'TestSkill',
        'version': '1.0.0',
        'tools': [
            {
                'name': 'test_method',
                'parameters': [
                    {'name': 'param1', 'type': 'string', 'required': True}
                ],
                'returns': {'type': 'object'}
            }
        ]
    }
    
    result = generate_api_doc(skill_def)
    
    assert result['title'] == '测试技能 API 文档'
    assert len(result['methods']) == 1
    assert result['methods'][0]['name'] == 'test_method'
    assert 'parameters' in result['methods'][0]
    assert 'examples' in result['methods'][0]

def test_tutorial_generation():
    """测试教程生成"""
    skill_def = {
        'name': '入门技能',
        'identifier': 'GettingStartedSkill',
        'version': '1.0.0'
    }
    
    tutorial = generate_tutorial(skill_def, 'getting_started')
    
    assert 'title' in tutorial
    assert len(tutorial['steps']) >= 3
    assert tutorial['steps'][0]['step'] == 1
    assert 'code_examples' in tutorial['steps'][0]

def test_translation():
    """测试翻译功能"""
    doc = {
        'title': '测试文档',
        'content': '这是一个测试'
    }
    
    translations = translate_document(doc, ['en', 'zh'])
    
    assert 'en' in translations
    assert 'zh' in translations
    assert translations['en']['content'] is not None
    assert translations['zh']['content'] is not None

def test_quality_check():
    """测试质量检查"""
    doc = {
        'title': '完整文档',
        'methods': [...],
        'examples': [...],
        'errors': [...]
    }
    
    result = calculate_quality_score(doc)
    
    assert 'total_score' in result
    assert 0 <= result['total_score'] <= 100
    assert 'level' in result

def test_version_management():
    """测试版本管理"""
    skill_def = {
        'name': '版本技能',
        'version': '2.0.0'
    }
    
    existing_docs = {
        'api': {...}  # 版本文档
    }
    
    result = manage_doc_versions(skill_def, existing_docs)
    
    assert 'new_docs' in result
    assert 'version_history' in result
    assert len(result['version_history']) > 0
```

### 集成测试

```python
def test_full_generation_workflow():
    """测试完整生成流程"""
    # 准备测试技能
    skill_def = load_test_skill()
    
    # 生成所有文档类型
    generator = SkillDocGenerator()
    result = generator.generate_all(skill_def)
    
    # 验证结果
    assert result['status'] == 'success'
    assert len(result['generated_docs']) >= 3  # API + 教程 + 最佳实践
    
    # 验证质量
    for doc in result['generated_docs']:
        assert doc['quality_score'] >= 80

def test_multi_language_generation():
    """测试多语言生成"""
    skill_def = load_test_skill()
    
    generator = SkillDocGenerator()
    result = generator.generate(
        skill_def,
        languages=['zh', 'en', 'es'],
        type='api'
    )
    
    # 验证所有语言都已生成
    assert len(result['translations']) == 3
    for lang in ['zh', 'en', 'es']:
        assert lang in result['translations']
        assert result['translations'][lang]['quality_score'] >= 85

def test_version_sync():
    """测试版本同步"""
    # 创建版本文档
    skill_v1 = load_skill_version('1.0.0')
    result_v1 = generate_docs(skill_v1)
    
    # 更新技能版本
    skill_v2 = load_skill_version('2.0.0')
    result_v2 = generate_docs(skill_v2)
    
    # 验证版本更新
    assert result_v2['version_info']['changes'] != []
    assert result_v2['version_info']['skill_version'] == '2.0.0'
```

## 📖 示例

### 生成的 API 文档

```markdown
# SkillDeployment API 文档

## 基本信息
- **技能名称**: SkillDeployment
- **版本**: 1.0.0
- **描述**: 技能部署与发布

## 方法

### deploy(skill_name, mode='prod')

部署技能到指定环境

**参数**:
- `skill_name` (string, 必填): 技能标识名
- `mode` (string, 可选): 部署模式（dev/test/prod），默认'prod'

**返回值**:
```json
{
  "status": "success",
  "deployment_id": "dep_123",
  "timestamp": "2026-03-31T12:00:00Z"
}
```

**示例**:
```bash
skill-deployment deploy --skill=MySkill --mode=test
```

**错误码**:
- `ERR_SKILL_NOT_FOUND`: 技能不存在
- `ERR_DEPLOYMENT_FAILED`: 部署失败
```

### 生成的教程文档

```markdown
# SkillDeployment 入门指南

## 前置要求
- 已安装 Skill CLI 工具
- 配置了部署环境
- 有部署权限

## 步骤 1: 安装与配置

### 安装 CLI 工具
```bash
npm install -g skill-deployment-cli
```

### 配置环境
```bash
skill-deployment config init
skill-deployment config set environment prod
```

## 步骤 2: 第一个部署

### 部署技能到测试环境
```bash
skill-deployment deploy --skill=MyFirstSkill --mode=test
```

### 查看部署状态
```bash
skill-deployment status --deployment-id=dep_123
```

## 步骤 3: 生产环境部署

### 部署前检查
```bash
skill-deployment pre-check --skill=MyFirstSkill
```

### 部署到生产环境
```bash
skill-deployment deploy --skill=MyFirstSkill --mode=prod
```

## 步骤 4: 监控与维护

### 查看部署日志
```bash
skill-deployment logs --deployment-id=dep_123
```

### 回滚操作
```bash
skill-deployment rollback --deployment-id=dep_123 --version=previous
```
```

### 生成的最佳实践文档

```markdown
# SkillDeployment 最佳实践

## 性能优化

### 推荐做法
1. 使用增量部署减少部署时间
2. 并行部署多个技能
3. 使用缓存加速依赖安装

### 性能指标
- 部署时间 < 5 分钟
- 回滚时间 < 1 分钟
- 部署成功率 > 99%

## 安全建议

### 权限管理
- 使用最小权限原则
- 定期轮换部署密钥
- 启用多因素认证

### 安全检查
- 部署前进行安全扫描
- 检查依赖漏洞
- 审计部署日志

## 常见陷阱

### 避免这些问题
1. 不要跳过测试环境直接部署生产
2. 不要在业务高峰期部署
3. 不要忘记备份配置
4. 不要忽略部署告警
```

## ❓ FAQ

### Q1: 如何处理技能定义格式变化？

**A**: 文档生成器会自动检测技能定义格式：
```python
# 支持多种格式
if 'tools' in skill_definition:
    # 新格式
    extract_tools_new_format()
elif 'methods' in skill_definition:
    # 旧格式
    extract_tools_old_format()
else:
    # 从代码分析
    analyze_code()
```

### Q2: 多语言翻译的准确性如何保证？

**A**: 采用多层质量保证：
1. **机器翻译**: 使用 Google Translate/DeepL
2. **术语表**: 维护专业术语翻译表
3. **人工审核**: 关键文档人工审核
4. **用户反馈**: 收集用户反馈持续改进

### Q3: 文档版本如何与技能版本保持同步？

**A**: 自动化版本同步流程：
```yaml
# CI/CD 配置
on:
  skill_version_updated:
    branches: [main]

jobs:
  update-docs:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Generate Docs
        run: skill-doc-generator generate --skill=${{ github.event.skill }} --type=all
      - name: Commit Changes
        run: |
          git config --global user.name 'Doc Bot'
          git add docs/
          git commit -m "docs: update to version ${{ github.event.version }}"
          git push
```

### Q4: 如何处理大型技能的文档生成？

**A**: 分批处理和优化：
```python
def generate_large_skill_doc(skill_definition):
    # 分批处理
    batches = split_into_batches(skill_definition['tools'], batch_size=20)
    
    results = []
    for batch in batches:
        result = generate_batch(batch)
        results.append(result)
    
    # 合并结果
    final_doc = merge_results(results)
    
    return final_doc
```

### Q5: 如何自定义文档模板？

**A**: 提供模板继承机制：
```yaml
# 自定义模板配置
template:
  extends: default  # 继承默认模板
  overrides:
    api_doc: ./templates/custom_api.md
    tutorial: ./templates/custom_tutorial.md
  
  custom_sections:
    - name: 安全说明
      position: after_methods
      template: ./templates/security_section.md
    
    - name: 性能提示
      position: before_examples
      template: ./templates/performance_tips.md
```

### Q6: 文档生成失败如何处理？

**A**: 完善的错误处理和重试机制：
```python
def generate_with_retry(skill_definition, max_retries=3):
    for attempt in range(max_retries):
        try:
            return generate_document(skill_definition)
        except TemporaryError as e:
            if attempt == max_retries - 1:
                raise
            wait_time = 2 ** attempt  # 指数退避
            time.sleep(wait_time)
        except PermanentError as e:
            # 永久错误不重试
            raise
    
    raise MaxRetriesExceeded()
```

## 🔗 相关资源

### 前置技能
- [documentation-engineer](../../documentation-engineer/SKILL.md) - 文档工程师
- [SkillQualityGate](../SkillQualityGate/SKILL.md) - 技能质量门禁

### 后置技能
- [SkillDeployment](../SkillDeployment/SKILL.md) - 技能部署
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量

### 辅助工具
- Markdown 编辑器
- 翻译 API（Google Translate, DeepL）
- 文档版本控制工具

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本，包含完整的文档生成策略、质量门禁、错误处理等 |

## 📞 维护信息

**维护者**: AI Assistant  
**邮箱**: support@example.com  
**Issue**: [GitHub Issue 链接](https://github.com/776138506/MyKnowledge/issues)

---

**创建日期**: 2026-03-31  
**最后更新**: 2026-03-31  
**版本**: 1.0.0  
**状态**: 🟢 稳定
