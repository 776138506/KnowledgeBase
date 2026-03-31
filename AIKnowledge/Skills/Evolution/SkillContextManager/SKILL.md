---
name: SkillContextManager
description: 技能上下文管理专家，负责管理技能执行上下文状态和会话记忆、优化 token 使用（摘要生成、记忆压缩、上下文窗口管理）、支持长期记忆和跨会话状态保持、处理上下文溢出和切换、实现智能摘要和关键信息保留，适用于长对话管理、多轮会话、上下文优化、记忆持久化场景
---

# 技能上下文管理器

## 🎯 核心目标

赋予 Agent **上下文管理** 与 **状态保持** 的能力，使其能够：
1. 管理技能执行的上下文状态
2. 优化 token 使用和上下文窗口
3. 支持长期记忆和状态保持
4. 实现上下文压缩和摘要
5. 处理上下文溢出和切换

## 🎯 适用场景

- ✅ **长对话管理**：管理长对话的上下文
- ✅ **状态保持**：保持多轮对话的状态
- ✅ **上下文优化**：优化 token 使用
- ✅ **记忆管理**：管理长期和短期记忆
- ✅ **上下文切换**：在不同任务间切换上下文
- ✅ **摘要压缩**：生成对话摘要节省 token

### 不适用场景
- ❌ 技能功能开发（应使用 development-engineer）
- ❌ 技能性能优化（应使用 SkillPerformanceOptimizer）
- ❌ 技能测试（应使用 SkillTesting）

## 🏗️ 技能架构

### 核心组件

```
SkillContextManager (上下文管理核心)
├── ContextTracker (上下文追踪器)
│   ├── StateManager (状态管理器)
│   ├── HistoryManager (历史管理器)
│   └── TokenCounter (Token 计数器)
├── OptimizationEngine (优化引擎)
│   ├── Compressor (上下文压缩器)
│   ├── Summarizer (摘要生成器)
│   └── Pruner (上下文修剪器)
├── MemoryManager (记忆管理器)
│   ├── ShortTermMemory (短期记忆)
│   ├── LongTermMemory (长期记忆)
│   └── MemoryRetriever (记忆检索器)
└── ContextSwitcher (上下文切换器)
    ├── ContextSaver (上下文保存)
    ├── ContextLoader (上下文加载)
    └── ContextPool (上下文池)
```

## 🔄 工作流程

```
上下文监控 → 状态追踪 → 优化决策 → 执行优化 → 上下文切换 → 记忆管理
    ↓          ↓          ↓          ↓          ↓          ↓
[实时监控] [状态保持] [优化策略] [压缩/摘要] [切换保存] [记忆存储]
```

## ⚙️ 执行模式

### Mode A: 监控模式
- 实时监控上下文使用
- token 使用追踪
- 持续运行

### Mode B: 优化模式
- 压缩过长的上下文
- 生成摘要
- 按需执行

### Mode C: 记忆模式
- 管理长期记忆
- 检索相关记忆
- 按需执行

### Mode D: 切换模式
- 保存当前上下文
- 加载目标上下文
- 快速切换

## 👥 上下文管理策略引擎

### Token 计数与监控算法

```python
def monitor_context_usage(conversation_history):
    """
    监控上下文使用情况
    """
    total_tokens = count_tokens(conversation_history)
    window_limit = get_context_window_limit()
    usage_percent = (total_tokens / window_limit) * 100
    
    # 识别可优化的部分
    optimizable_parts = []
    
    # 检查历史对话
    if len(conversation_history) > 10:
        old_messages = conversation_history[:len(conversation_history)-10]
        old_tokens = count_tokens(old_messages)
        optimizable_parts.append({
            "type": "old_messages",
            "tokens": old_tokens,
            "suggestion": "可以压缩或摘要"
        })
    
    # 检查长消息
    for msg in conversation_history:
        if count_tokens([msg]) > 500:
            optimizable_parts.append({
                "type": "long_message",
                "tokens": count_tokens([msg]),
                "suggestion": "可以精简"
            })
    
    return {
        "total_tokens": total_tokens,
        "window_limit": window_limit,
        "usage_percent": usage_percent,
        "optimizable_parts": optimizable_parts,
        "urgency": "high" if usage_percent > 80 else "medium" if usage_percent > 60 else "low"
    }
```

### 摘要生成策略

```python
def generate_summary(conversation_segment, summary_type='detailed'):
    """
    生成对话摘要
    """
    if summary_type == 'brief':
        # 简要摘要：只保留关键决策
        key_points = extract_key_decisions(conversation_segment)
        return {
            "type": "brief",
            "content": key_points,
            "compression_ratio": 0.1,  # 压缩到 10%
            "tokens_saved": estimate_tokens_saved(conversation_segment, 0.1)
        }
    
    elif summary_type == 'detailed':
        # 详细摘要：保留决策和关键信息
        key_points = extract_key_decisions(conversation_segment)
        key_info = extract_key_information(conversation_segment)
        return {
            "type": "detailed",
            "content": key_points + key_info,
            "compression_ratio": 0.3,
            "tokens_saved": estimate_tokens_saved(conversation_segment, 0.3)
        }
```

### 记忆管理算法

```python
def manage_memory(memory_item, memory_type='long_term'):
    """
    管理长期记忆
    """
    if memory_type == 'long_term':
        # 长期记忆存储
        return {
            "storage": "persistent_db",
            "indexing": ["topic", "timestamp", "importance"],
            "retrieval": "semantic_search",
            "retention": "indefinite"
        }
    
    elif memory_type == 'short_term':
        # 短期记忆缓存
        return {
            "storage": "in_memory_cache",
            "capacity": 100,
            "eviction_policy": "LRU",
            "ttl_hours": 24
        }
```

## 📋 输入输出规范

### 输入格式

```json
{
  "context_data": {
    "type": "object",
    "description": "上下文数据",
    "properties": {
      "conversation_history": "类型：array，说明：对话历史",
      "current_state": "类型：object，说明：当前状态",
      "active_variables": "类型：object，说明：活跃变量"
    }
  },
  "management_config": {
    "type": "object",
    "description": "管理配置",
    "properties": {
      "optimization_threshold": "类型：number，说明：优化阈值（百分比）",
      "summary_frequency": "类型：number，说明：摘要频率（轮数）",
      "memory_enabled": "类型：boolean，说明：是否启用记忆"
    }
  }
}
```

### 输出格式

```json
{
  "status": "success|partial_success|failed",
  "context_status": {
    "total_tokens": "总 token 数",
    "window_limit": "窗口限制",
    "usage_percent": "使用百分比",
    "urgency": "紧急程度"
  },
  "optimization_result": {
    "tokens_before": "优化前 token 数",
    "tokens_after": "优化后 token 数",
    "tokens_saved": "节省 token 数",
    "compression_ratio": "压缩率"
  },
  "summary": {
    "type": "摘要类型",
    "content": "摘要内容",
    "key_points": ["关键点列表"]
  },
  "memory_operations": [
    {
      "operation": "操作类型",
      "item_id": "记忆 ID",
      "status": "状态"
    }
  ]
}
```

## ✅ 质量门禁

### 上下文管理检查

- [ ] Token 计数准确
- [ ] 优化不丢失关键信息
- [ ] 摘要保留要点
- [ ] 记忆检索准确

### 性能检查

- [ ] 优化操作<5 秒
- [ ] 摘要生成<10 秒
- [ ] 记忆检索<1 秒
- [ ] 上下文切换<2 秒

## ⚠️ 错误处理

### 常见错误

| 错误代码 | 错误信息 | 原因分析 | 解决方案 |
|---------|---------|---------|---------|
| ERR_CONTEXT_OVERFLOW | 上下文溢出 | 超出窗口限制 | 紧急压缩 |
| ERR_SUMMARY_FAILED | 摘要失败 | 内容无法解析 | 手动摘要 |
| ERR_MEMORY_LOST | 记忆丢失 | 存储故障 | 从备份恢复 |

## 📚 最佳实践

### 推荐做法

- ✅ **主动监控**: 实时监控上下文使用
- ✅ **渐进压缩**: 逐步压缩而非一次性
- ✅ **智能摘要**: 保留关键信息
- ✅ **定期清理**: 清理过期数据

### 避免做法

- ❌ **过度压缩**: 丢失重要信息
- ❌ **延迟优化**: 等到溢出才优化
- ❌ **无差别压缩**: 不区分重要性

## 🔧 配置选项

```yaml
skill_context_manager:
  version: 1.0.0
  
  monitoring:
    enabled: true
    check_interval_seconds: 60
    warning_threshold: 60
    critical_threshold: 80
  
  optimization:
    auto_optimize: true
    compression_strategy: "progressive"
    summary_frequency: 10
  
  memory:
    enabled: true
    short_term_capacity: 100
    long_term_storage: "persistent"
```

## 📖 示例

### 长对话管理

**场景**: 管理超过 50 轮的长对话

**执行命令**:
```bash
skill-context-manager optimize --threshold=70
```

**优化结果**:
```markdown
# 上下文优化报告

## 优化前
- Token 使用：11500/12000 (95.8%)
- 对话轮数：52
- 状态：⚠️ 紧急

## 优化操作
1. 压缩前 30 轮对话 → 节省 3500 tokens
2. 生成关键决策摘要 → 节省 800 tokens
3. 清理临时变量 → 节省 200 tokens

## 优化后
- Token 使用：7000/12000 (58.3%)
- 可用空间：5000 tokens
- 节省：4500 tokens (39.1%)
```

## 🔗 相关资源

### 前置技能
- [SkillMetrics](../SkillMetrics/SKILL.md) - 技能度量与分析
- [SkillPerformanceOptimizer](../SkillPerformanceOptimizer/SKILL.md) - 技能性能优化器

### 参考资料
- [上下文管理最佳实践](链接)
- [Token 优化指南](链接)

## ❓ FAQ

### Q1: 如何平衡压缩率和信息完整性？

**解答**: 使用渐进式压缩策略，先压缩不重要的历史对话，保留关键决策和状态信息。

### Q2: 上下文溢出怎么办？

**解答**: 立即执行紧急压缩，优先保留最近 10 轮对话和关键状态。

## 📝 更新日志

| 版本 | 日期 | 作者 | 变更内容 |
|------|------|------|---------|
| 1.0.0 | 2026-03-31 | AI Assistant | 初始版本 |
| 1.0.1 | 2026-03-31 | AI Assistant | 扩充上下文管理策略引擎等章节 |
