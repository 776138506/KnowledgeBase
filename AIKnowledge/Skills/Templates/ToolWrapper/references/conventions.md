# [技术/领域] 开发规范

> Tool Wrapper 模式参考文档模板

## 1. 项目结构规范

### 1.1 目录组织

```
project/
├── src/                    # 源代码目录
│   ├── __init__.py
│   ├── main.py            # 应用入口
│   ├── routers/           # API 路由
│   ├── models/            # 数据模型
│   ├── schemas/           # Pydantic 模式
│   ├── services/          # 业务逻辑
│   └── utils/             # 工具函数
├── tests/                 # 测试目录
├── requirements.txt       # 依赖
└── README.md
```

### 1.2 文件命名

- 使用小写字母和下划线：`user_service.py`
- 测试文件前缀：`test_*.py`
- 配置文件：`.env`, `config.yaml`

## 2. 编码规范

### 2.1 命名规范

**变量命名**:
- 使用小写 + 下划线：`user_name`, `total_count`
- 常量使用全大写：`MAX_SIZE`, `API_VERSION`
- 私有变量前缀下划线：`_internal_cache`

**函数命名**:
- 动词 + 名词：`get_user`, `create_order`
- 布尔函数用 is/has/can 前缀：`is_valid`, `has_permission`

**类命名**:
- 使用大驼峰：`UserService`, `OrderManager`
- 异常类以 Error 结尾：`ValidationError`, `DatabaseError`

### 2.2 代码组织

**导入顺序**:
1. 标准库
2. 第三方库
3. 本地模块

**函数长度**:
- 单个函数不超过 50 行
- 超过需要拆分

**类设计**:
- 单一职责原则
- 优先组合而非继承

## 3. 最佳实践

### 3.1 错误处理

- ✅ 使用具体的异常类型
- ✅ 提供有意义的错误消息
- ✅ 记录异常堆栈
- ❌ 不要捕获所有异常（避免 bare except）
- ❌ 不要忽略异常（避免 pass）

**示例**:
```python
# ✅ 好的做法
try:
    user = get_user(user_id)
except UserNotFoundError as e:
    logger.error(f"User {user_id} not found: {e}")
    raise HTTPException(status_code=404, detail="User not found")

# ❌ 坏的做法
try:
    user = get_user(user_id)
except:
    pass
```

### 3.2 日志记录

- 使用适当的日志级别（DEBUG, INFO, WARNING, ERROR）
- 包含上下文信息（用户 ID、请求 ID 等）
- 不要记录敏感信息

**示例**:
```python
logger.info(f"User {user_id} logged in from {ip_address}")
logger.error(f"Payment failed for order {order_id}: {error_message}")
```

### 3.3 数据验证

- 使用 Pydantic 等工具验证输入
- 在边界处验证（API 入口、数据库操作前）
- 提供清晰的验证错误消息

## 4. 安全规范

### 4.1 SQL 注入防护

- ✅ 使用参数化查询
- ❌ 禁止字符串拼接 SQL

```python
# ✅ 好的做法
query = "SELECT * FROM users WHERE id = ?"
db.execute(query, (user_id,))

# ❌ 坏的做法
query = f"SELECT * FROM users WHERE id = {user_id}"
db.execute(query)
```

### 4.2 认证与授权

- 所有 API 端点必须有认证
- 实现基于角色的访问控制（RBAC）
- 使用 JWT 等安全令牌

### 4.3 密码安全

- 使用 bcrypt/argon2 等强哈希算法
- 加盐存储密码
- 实施密码复杂度要求

### 4.4 输入验证

- 验证所有用户输入
- 限制输入长度
- 过滤特殊字符

## 5. 性能优化

### 5.1 数据库优化

- 使用索引加速查询
- 避免 N+1 查询问题
- 使用连接池

### 5.2 缓存策略

- 缓存频繁访问的数据
- 设置合理的过期时间
- 实现缓存失效机制

### 5.3 异步处理

- 对 I/O 密集型操作使用异步
- 使用消息队列处理耗时任务
- 实现背压机制

## 6. 测试规范

### 6.1 单元测试

- 覆盖所有核心功能
- 测试正常场景、边界场景、异常场景
- 保持测试独立

### 6.2 集成测试

- 测试模块间交互
- 使用测试数据库
- 清理测试数据

### 6.3 测试覆盖率

- 语句覆盖率 ≥ 80%
- 分支覆盖率 ≥ 75%
- 函数覆盖率 ≥ 90%

## 7. 文档规范

### 7.1 代码注释

- 解释"为什么"而不是"是什么"
- 复杂的算法需要详细注释
- 保持注释更新

### 7.2 API 文档

- 所有端点必须有文档
- 包含请求/响应示例
- 说明错误情况

### 7.3 README

- 项目说明
- 快速开始指南
- 部署说明

## 8. 版本控制

### 8.1 Git 提交规范

```
feat: 新功能
fix: 修复 bug
docs: 文档更新
style: 代码格式调整
refactor: 重构
test: 测试相关
chore: 构建/工具链
```

### 8.2 分支管理

- `main`: 生产环境代码
- `develop`: 开发分支
- `feature/*`: 功能分支
- `hotfix/*`: 紧急修复

## 9. 部署规范

### 9.1 环境变量

- 敏感信息使用环境变量
- 提供 `.env.example` 模板
- 不同环境使用不同配置

### 9.2 容器化

- 使用多阶段构建减小镜像
- 不以 root 用户运行
- 健康检查端点

### 9.3 监控

- 实现健康检查端点
- 收集关键指标（QPS、延迟、错误率）
- 配置告警

## 10. 常见陷阱

| 陷阱 | 问题 | 避免方法 |
|------|------|----------|
| 循环导入 | 模块间相互导入导致错误 | 重构代码结构，使用导入延迟 |
| 可变默认参数 | 默认参数被共享 | 使用 None 作为默认值 |
| 阻塞异步代码 | 在异步代码中使用同步 I/O | 使用异步版本或线程池 |
| 数据库连接泄漏 | 连接未正确关闭 | 使用上下文管理器 |

## 11. 检查清单

### 代码提交前检查

- [ ] 代码通过 lint 检查
- [ ] 所有测试通过
- [ ] 覆盖率达标
- [ ] 文档已更新
- [ ] 无敏感信息提交

### 代码审查检查

- [ ] 遵循命名规范
- [ ] 函数职责单一
- [ ] 错误处理完善
- [ ] 日志记录适当
- [ ] 安全规范遵循

***

**版本**: 1.0.0  
**最后更新**: YYYY-MM-DD  
**适用范围**: [技术/领域]
