---
name: documentation-engineer
description: 文档编制专家，负责 API 文档、用户手册、开发日志、技术文档的编写和维护。在项目各阶段需要文档时调用此技能。
---

# 文档编制专家 (Documentation Engineer)

## 📋 技能概述

专业文档编制技能，基于技术文档最佳实践和命名规范，负责编写和维护各类技术文档，包括 API 文档、用户手册、开发日志、设计文档等。

## 🎯 适用场景

- ✅ 新功能开发完成后
- ✅ 需要编写 API 文档
- ✅ 需要编写用户手册
- ✅ 需要记录开发日志
- ✅ 需要整理技术文档
- ✅ 需要文档审查和重构

## 🔄 工作流程

### 步骤 1：文档需求分析

#### 识别文档类型
| 文档类型 | 用途 | 读者对象 |
|---------|------|---------|
| API 文档 | 接口说明 | 开发人员 |
| 用户手册 | 使用指南 | 最终用户 |
| 开发日志 | 开发记录 | 开发团队 |
| 设计文档 | 架构设计 | 技术人员 |
| 测试文档 | 测试用例 | 测试人员 |
| 部署文档 | 部署指南 | 运维人员 |

#### 文档优先级
- **P0**：API 文档、部署文档（必须）
- **P1**：用户手册、开发日志（重要）
- **P2**：技术文档、最佳实践（推荐）

### 步骤 2：API 文档编写

#### JSDoc 标准格式
```typescript
/**
 * 用户登录接口
 * @description 验证用户凭据并返回 JWT token
 * 
 * @url POST /api/auth/login
 * 
 * @param {string} username - 用户名（必填）
 * @param {string} password - 密码（必填）
 * @param {boolean} [rememberMe] - 是否记住我（可选，默认 false）
 * 
 * @returns {Promise<LoginResult>} 登录结果
 * @property {string} token - JWT token
 * @property {User} user - 用户信息
 * 
 * @throws {AuthenticationError} 用户名或密码错误
 * @throws {AccountLockedError} 账户被锁定
 * 
 * @example
 * // 调用示例
 * const result = await login('john', 'password123');
 * console.log(result.token);
 * 
 * @author AI Assistant
 * @since 1.0.0
 * @version 1.0.0
 */
async function login(
    username: string,
    password: string,
    rememberMe: boolean = false
): Promise<LoginResult>
```

#### API 文档结构
```markdown
# API 文档

## 认证模块

### 用户登录

**接口路径**: `POST /api/auth/login`

**请求参数**:
| 参数名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| username | string | 是 | 用户名 |
| password | string | 是 | 密码 |
| rememberMe | boolean | 否 | 是否记住我（默认 false） |

**请求示例**:
```json
{
  "username": "john",
  "password": "password123",
  "rememberMe": true
}
```

**响应示例**:
```json
{
  "code": 200,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIs...",
    "user": {
      "id": 1,
      "username": "john",
      "email": "john@example.com"
    }
  }
}
```

**错误码**:
| 错误码 | 说明 |
|--------|------|
| 401 | 用户名或密码错误 |
| 403 | 账户被锁定 |
| 400 | 参数错误 |
```

### 步骤 3：用户手册编写

#### 用户手册结构
```markdown
# 用户手册

## 1. 产品简介
- 产品功能
- 适用场景
- 系统要求

## 2. 快速开始
- 注册账号
- 登录系统
- 基本操作

## 3. 功能说明
- 功能 1 使用说明
- 功能 2 使用说明
- 常见问题

## 4. 高级功能
- 高级配置
- 自定义设置

## 5. 故障排除
- 常见问题 FAQ
- 错误代码说明
- 联系方式
```

#### 编写原则
- **清晰简洁**：避免技术术语
- **步骤详细**：逐步说明操作
- **图文并茂**：配合截图说明
- **问题导向**：解答常见问题

### 步骤 4：开发日志编写

#### 开发日志模板
```markdown
# 开发日志 - [功能名称]

## 基本信息
**日期**: YYYY-MM-DD  
**开发者**: [姓名]  
**版本**: v1.0.0  

## 功能概述

### 业务背景
[为什么需要这个功能]

### 实现目标
[功能要解决什么问题]

### 技术栈
- 语言：[TypeScript]
- 框架：[React]

## 函数实现

### [函数名称]

**位置**: `文件路径：行号范围`

**职责**: [描述]

**参数**: [表格]

**返回值**: `类型` - 描述

**实现逻辑**:
1. 步骤 1
2. 步骤 2
3. 步骤 3

**关键代码**:
```typescript
// 代码 + 注释
```

## API 文档

```typescript
/**
 * JSDoc 文档
 */
```

## 测试覆盖

[测试用例]

## 设计决策

[方案选择和原因]

## TODO

- [ ] [改进事项]
```

### 步骤 5：文档命名和归档

#### 文档命名规范
```
格式：[类别]-[编号]-[描述].md

示例：
- api-auth-login.md       # API 文档
- user-manual-v1.0.md     # 用户手册
- dev-log-2026-03-25.md   # 开发日志
- design-system-arch.md   # 设计文档
```

#### 文档目录结构
```
docs/
├── api/                  # API 文档
│   ├── auth.md
│   ├── user.md
│   └── order.md
├── manual/               # 用户手册
│   ├── quick-start.md
│   └── user-guide.md
├── dev-logs/            # 开发日志
│   ├── 2026-03-25-login-feature.md
│   └── 2026-03-26-order-module.md
├── design/              # 设计文档
│   ├── architecture.md
│   └── database.md
└── deployment/          # 部署文档
    ├── setup-guide.md
    └──运维手册.md
```

### 步骤 6：文档审查和更新

#### 文档质量检查
- [ ] 内容准确完整
- [ ] 格式规范统一
- [ ] 语言清晰易懂
- [ ] 示例正确可运行
- [ ] 链接有效
- [ ] 版本信息正确

#### 文档更新流程
```
1. 识别变更内容
   ↓
2. 更新相关文档
   ↓
3. 审查文档质量
   ↓
4. 更新版本号
   ↓
5. 归档旧版本
```

## 📤 输出格式

### 文档编制报告模板

```markdown
## 文档编制报告

### 📋 文档清单

#### 新增文档
- [x] [文档名称] - [文档类型] - [状态]
- [x] [文档名称] - [文档类型] - [状态]

#### 更新文档
- [x] [文档名称] - [变更内容] - [版本]

### 📊 文档质量评估

| 文档 | 完整性 | 准确性 | 可读性 | 总体评分 |
|------|--------|--------|--------|---------|
| [文档 1] | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐☆ | 4.7/5 |
| [文档 2] | ⭐⭐⭐⭐☆ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 4.7/5 |

### ✅ 文档检查清单

#### API 文档
- [ ] 所有接口已文档化
- [ ] 参数说明完整
- [ ] 示例代码正确
- [ ] 错误码说明完整
- [ ] JSDoc 注释完整

#### 用户手册
- [ ] 快速开始指南完整
- [ ] 功能说明清晰
- [ ] 截图配合适当
- [ ] FAQ 已整理
- [ ] 联系方式正确

#### 开发日志
- [ ] 功能概述完整
- [ ] 实现细节详细
- [ ] API 文档已记录
- [ ] 测试覆盖已说明
- [ ] TODO 列表清晰

### 📝 改进建议

#### 高优先级
- [ ] [建议内容]

#### 中优先级
- [ ] [建议内容]

### ✅ 文档结论
- [ ] 通过，所有文档完整且质量达标
- [ ] 有条件通过，需完善部分文档
- [ ] 不通过，关键文档缺失
```

## ✅ 质量门禁

### 文档完整性检查
- [ ] API 文档完整
- [ ] 用户手册完整
- [ ] 开发日志已记录
- [ ] 设计文档已归档
- [ ] 测试文档完整

### 文档质量检查
- [ ] 内容准确完整
- [ ] 格式规范统一
- [ ] 语言清晰易懂
- [ ] 示例正确可运行
- [ ] 版本信息正确

### 文档规范检查
- [ ] 遵循命名规范
- [ ] 目录结构清晰
- [ ] 版本管理适当
- [ ] 归档及时

## 📝 示例交互

### 示例 1：登录功能文档编制

**用户**：
```
请为登录功能编写完整的文档，包括：
- API 文档
- 用户手册片段
- 开发日志
```

**Documentation Engineer**：
```
## 登录功能文档编制报告

### 1. API 文档

```typescript
/**
 * 用户登录接口
 * @description 验证用户凭据并生成 JWT token
 * 
 * @url POST /api/auth/login
 * 
 * @param {string} username - 用户名（必填，3-20 位字母数字）
 * @param {string} password - 密码（必填，8-20 位，包含大小写字母和数字）
 * @param {boolean} [rememberMe=false] - 是否记住我
 * 
 * @returns {Promise<LoginResult>}
 * @property {string} token - JWT token（有效期 2 小时）
 * @property {User} user - 用户信息
 * @property {number} user.id - 用户 ID
 * @property {string} user.username - 用户名
 * @property {string} user.email - 邮箱
 * 
 * @throws {AuthenticationError} 用户名或密码错误（401）
 * @throws {AccountLockedError} 账户被锁定（403）
 * @throws {ValidationError} 参数验证失败（400）
 * 
 * @example
 * // 调用示例
 * const result = await login('john', 'Password123!', true);
 * console.log('Token:', result.token);
 * 
 * @security 使用 bcrypt 加密密码
 * @security 连续失败 5 次锁定账户
 * 
 * @author AI Assistant
 * @since 1.0.0
 * @version 1.0.0
 */
async function login(
    username: string,
    password: string,
    rememberMe: boolean = false
): Promise<LoginResult>
```

**接口详细说明**:

```markdown
## 用户登录

**接口路径**: `POST /api/auth/login`

**请求参数**:
| 参数名 | 类型 | 必填 | 说明 |
|--------|------|------|------|
| username | string | 是 | 用户名（3-20 位字母数字） |
| password | string | 是 | 密码（8-20 位，包含大小写字母和数字） |
| rememberMe | boolean | 否 | 是否记住我（默认 false，true 则 token 有效期 7 天） |

**请求示例**:
```json
{
  "username": "john",
  "password": "Password123!",
  "rememberMe": true
}
```

**成功响应** (200):
```json
{
  "code": 200,
  "message": "登录成功",
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 7200,
    "user": {
      "id": 1,
      "username": "john",
      "email": "john@example.com",
      "avatar": "https://example.com/avatar.jpg"
    }
  }
}
```

**错误响应**:
```json
// 401 - 用户名或密码错误
{
  "code": 401,
  "message": "用户名或密码错误",
  "data": null
}

// 403 - 账户被锁定
{
  "code": 403,
  "message": "账户已被锁定，请 30 分钟后再试",
  "data": {
    "unlockAt": "2026-03-25T15:30:00Z"
  }
}

// 400 - 参数验证失败
{
  "code": 400,
  "message": "参数验证失败",
  "data": {
    "fields": [
      {
        "field": "password",
        "message": "密码必须包含大小写字母和数字"
      }
    ]
  }
}
```

**安全说明**:
- 密码使用 bcrypt 加密存储
- 连续失败 5 次锁定账户 30 分钟
- Token 使用 JWT，包含用户 ID 和用户名
- 建议前端使用 HTTPS 传输
```

### 2. 用户手册片段

```markdown
## 登录系统

### 登录步骤

1. **打开登录页面**
   - 访问网站，点击右上角"登录"按钮
   
2. **输入账号信息**
   - 用户名：您的用户名（3-20 位字母数字）
   - 密码：您的密码（8-20 位，包含大小写字母和数字）
   
3. **选择是否记住我**
   - 勾选"记住我"：7 天内自动登录
   - 不勾选：2 小时后需要重新登录
   
4. **点击登录**
   - 点击"登录"按钮
   - 等待系统验证
   
5. **登录成功**
   - 成功登录后跳转到首页
   - 右上角显示您的头像和用户名

### 常见问题

**Q: 忘记密码怎么办？**
A: 点击登录页面的"忘记密码"链接，通过注册邮箱重置密码。

**Q: 账户被锁定了怎么办？**
A: 连续输错密码 5 次会导致账户锁定 30 分钟。请等待 30 分钟后重试，或联系客服。

**Q: 为什么登录后很快又被退出？**
A: 如果您没有勾选"记住我"，登录状态 2 小时后过期。勾选"记住我"可保持 7 天登录状态。

### 安全提示

- 不要在公共电脑上勾选"记住我"
- 定期更换密码
- 不要使用简单密码（如 123456）
- 发现异常登录及时修改密码
```

### 3. 开发日志

```markdown
# 开发日志 - 用户登录功能

## 基本信息
**日期**: 2026-03-25  
**开发者**: AI Assistant  
**版本**: v1.0.0  

## 功能概述

### 业务背景
用户需要安全的登录功能，支持用户名密码认证，包含防暴力破解机制。

### 实现目标
1. 实现用户登录验证
2. 生成 JWT token
3. 防止暴力破解
4. 记录登录日志

### 技术栈
- TypeScript 4.9
- Node.js 18 + Express
- bcrypt, jsonwebtoken
- MySQL 8.0

## 函数实现

### login 函数

**位置**: `src/services/auth.service.ts:15-80`

**职责**: 验证用户凭据并生成 JWT token

**参数**:
| 参数名 | 类型 | 说明 |
|--------|------|------|
| username | string | 用户名 |
| password | string | 密码 |
| rememberMe | boolean | 是否记住我（默认 false） |

**返回值**: `Promise<LoginResult>` - 包含 token 和用户信息

**实现逻辑**:
1. 检查账户锁定状态
2. 查询用户信息
3. 验证密码
4. 生成 JWT token
5. 重置失败计数
6. 记录登录日志

**关键代码**:
```typescript
async function login(
  username: string,
  password: string,
  rememberMe: boolean = false
): Promise<LoginResult> {
  // 检查账户锁定
  const lockStatus = await checkAccountLockStatus(username);
  if (lockStatus.isLocked) {
    throw new AccountLockedError('账户已锁定');
  }

  // 查询用户
  const user = await userRepository.findByUsername(username);
  if (!user) {
    await incrementLoginFailure(username);
    throw new AuthenticationError('用户名或密码错误');
  }

  // 验证密码
  const passwordMatches = await bcrypt.compare(password, user.passwordHash);
  if (!passwordMatches) {
    await incrementLoginFailure(username);
    throw new AuthenticationError('用户名或密码错误');
  }

  // 生成 token
  const token = jwt.sign(
    { userId: user.id, username: user.username },
    Config.jwtSecret,
    { expiresIn: rememberMe ? '7d' : '2h' }
  );

  // 重置失败计数
  await resetLoginFailure(username);

  // 记录日志
  await loginLogRepository.create({
    userId: user.id,
    loginTime: new Date(),
    success: true,
  });

  return { token, user };
}
```

## API 文档

```typescript
/**
 * 用户登录
 * @param username - 用户名
 * @param password - 密码
 * @param rememberMe - 是否记住我（默认 false）
 * @returns 登录结果
 * @throws AuthenticationError 用户名或密码错误
 * @throws AccountLockedError 账户被锁定
 */
async function login(
  username: string,
  password: string,
  rememberMe?: boolean
): Promise<LoginResult>
```

## 测试覆盖

### 单元测试
- [x] 正常登录成功
- [x] 错误密码
- [x] 账户锁定
- [x] 连续失败 5 次锁定

### 测试覆盖率
- 语句覆盖率：95%
- 分支覆盖率：90%
- 函数覆盖率：100%

## 设计决策

**密码加密**: 选择 bcrypt 而不是 MD5
- 原因：bcrypt 更安全，防止暴力破解

**Token 有效期**: 
- 记住我：7 天
- 不记住：2 小时
- 原因：平衡安全性和便利性

## TODO

- [ ] 实现图形验证码
- [ ] 添加双因素认证
- [ ] 支持第三方登录（Google、GitHub）
```

### 文档质量评估

| 文档 | 完整性 | 准确性 | 可读性 | 总体评分 |
|------|--------|--------|--------|---------|
| API 文档 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐☆ | 4.7/5 |
| 用户手册 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | 5.0/5 |
| 开发日志 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐☆ | 4.7/5 |

### ✅ 文档结论
- [x] 通过，所有文档完整且质量达标
```

## 🎯 使用建议

### 何时调用
- 新功能开发完成后
- 需要编写 API 文档时
- 需要编写用户手册时
- 需要记录开发日志时
- 需要整理技术文档时

### 调用指令模板
```
请使用 documentation-engineer 技能为 [功能名称] 编写文档：
- 功能说明：[描述]
- 文档类型：[API 文档/用户手册/开发日志]
- 目标读者：[开发人员/最终用户]
- 特殊要求：[描述]
```

### 与其他技能协作
- **前置** `cc-godmode` - 生成代码
- **前置** `code-reviewer` - 代码审查
- **前置** `quality-validator` - 测试验证

## 📚 参考文档

- WF-06 文档编制
- 01-开发日志模板.md
- 01-开发日志规范.md
- 02-开发日志示例.md
- 04-文档命名规范.md
- 11-文档编制.md

---

**版本**: 1.0.0  
**更新日期**: 2026-03-25  
**维护者**: AI Assistant