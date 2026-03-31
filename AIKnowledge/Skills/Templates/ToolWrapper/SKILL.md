---
name: [SkillIdentifier]
description: [技能的详细描述，包括角色、职责、使用场景。例如：Expert in [technology/library]. Use when building, reviewing, or debugging [technology] applications.]
---

# [技能中文名称]

## 🎯 核心目标

[用 1-2 句话描述技能的核心目标和价值。例如：提供 [技术/领域] 的最佳实践和规范，帮助开发者快速构建、审查和调试相关应用。]

## 🏗️ 目录结构

```
skills/[SkillIdentifier]/
├── SKILL.md                    # 技能定义文件（本文件）
└── references/
    └── [conventions.md]        # 详细的规范文档
```

## 📋 使用说明

### 何时加载

在以下场景中，Agent 应该加载此技能：

- ✅ 构建、开发 [技术/领域] 相关应用时
- ✅ 审查 [技术/领域] 代码时
- ✅ 调试 [技术/领域] 问题时
- ✅ 需要遵循团队规范时

### 如何使用

#### 1. 加载规范文档

```
Load 'references/[conventions.md]' for the complete list of best practices.
```

#### 2. 审查代码时

按照以下流程：

1. 加载规范文档（Load the conventions reference）
2. 逐条检查代码是否符合规范（Check code against each convention）
3. 发现违规时，引用具体规则并建议修复方案（For violations, cite the rule and suggest the fix）

#### 3. 编写代码时

按照以下流程：

1. 加载规范文档（Load the conventions reference）
2. 严格遵循所有规范（Follow every convention exactly）
3. 为所有函数签名添加类型注解（Add type annotations to all function signatures）

## 🔄 工作流程

```
用户请求
    ↓
判断场景（编写/审查/调试）
    ↓
加载 references/[conventions.md]
    ↓
执行对应流程
    ↓
输出结果（代码/审查报告/解决方案）
```

## 📚 参考文档

### references/conventions.md 内容模板

```markdown
# [技术/领域] 开发规范

## 1. 项目结构

[描述项目组织规范]

## 2. 编码规范

### 2.1 命名规范
- [命名规则 1]
- [命名规则 2]

### 2.2 代码组织
- [代码组织规则 1]
- [代码组织规则 2]

## 3. 最佳实践

### 3.1 [最佳实践类别 1]
- [具体实践 1]
- [具体实践 2]

### 3.2 [最佳实践类别 2]
- [具体实践 1]
- [具体实践 2]

## 4. 常见陷阱

- [陷阱 1] + [避免方法]
- [陷阱 2] + [避免方法]

## 5. 性能优化

- [优化建议 1]
- [优化建议 2]

## 6. 安全建议

- [安全建议 1]
- [安全建议 2]
```

## ✅ 质量检查清单

使用此技能时，确保：

- [ ] 已加载完整的规范文档
- [ ] 审查时逐条对照规范
- [ ] 违规时提供具体的规则引用
- [ ] 修复建议具体可执行
- [ ] 编写的代码遵循所有规范

## 📖 示例

### 示例 1：代码审查

**用户请求**:
```
请审查这段代码：
def get_user(user_id):
    query = "SELECT * FROM users WHERE id = " + user_id
    return db.execute(query)
```

**Agent 响应**:
```
## 代码审查结果

### ❌ 严重问题

**第 2 行**: SQL 注入风险
- **违反规则**: 安全规范 6.1 - 禁止字符串拼接 SQL 查询
- **问题说明**: 直接使用字符串拼接构造 SQL 查询，存在 SQL 注入漏洞
- **修复建议**: 使用参数化查询
```python
def get_user(user_id: int) -> User:
    query = "SELECT * FROM users WHERE id = ?"
    return db.execute(query, (user_id,))
```

### ⚠️ 警告

**第 1 行**: 缺少类型注解
- **违反规则**: 编码规范 2.1 - 所有函数必须有类型注解
- **修复建议**: 添加参数和返回值类型注解
```

### 示例 2：代码编写

**用户请求**:
```
帮我创建一个 FastAPI 的用户注册端点
```

**Agent 响应**:
```
[加载规范文档后，按照规范创建端点]

```python
from fastapi import APIRouter, HTTPException, status
from pydantic import BaseModel, EmailStr
from typing import Optional

router = APIRouter()

class UserCreate(BaseModel):
    email: EmailStr
    password: str
    name: Optional[str] = None

@router.post(
    "/users",
    response_model=UserResponse,
    status_code=status.HTTP_201_CREATED,
    tags=["users"]
)
async def create_user(user_data: UserCreate) -> UserResponse:
    """
    创建新用户
    
    Args:
        user_data: 用户注册信息
        
    Returns:
        创建的用户信息
        
    Raises:
        HTTPException: 用户已存在时抛出 400 错误
    """
    # 实现代码...
```

遵循的规范：
- ✅ 使用 Pydantic 模型验证输入
- ✅ 添加完整的类型注解
- ✅ 使用 HTTP 状态码常量
- ✅ 包含详细的文档字符串
- ✅ 使用 tags 组织端点
```

## ⚠️ 注意事项

- 不要将规范硬编码到系统提示词，保持灵活性
- 规范文档应该详细且可执行
- 定期更新规范文档以反映最佳实践的变化

## 🔗 相关资源

- [相关技术官方文档](链接)
- [团队编码规范](链接)
- [最佳实践指南](链接)

***

**版本**: 1.0.0  
**创建日期**: YYYY-MM-DD  
**模式类型**: Tool Wrapper（工具包装器）
