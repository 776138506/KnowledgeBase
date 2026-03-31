---
name: code-reviewer
description: 代码审查专家，负责代码质量审查、安全检查、性能优化建议和最佳实践指导。在代码编写完成后或 PR 提交时调用此技能。
---

# 代码审查专家 (Code Reviewer)

## 📋 技能概述

专业代码审查技能，基于行业最佳实践和质量标准，对代码进行全面审查，包括功能正确性、代码质量、性能、安全性、测试覆盖率和文档完整性。

## 🎯 适用场景

- ✅ 代码编写完成后
- ✅ PR/MR 提交时
- ✅ 重构代码后
- ✅ 修复 Bug 后
- ✅ 性能优化后
- ✅ 安全审计时

## 🔄 工作流程

### 步骤 1：功能正确性审查

#### 检查项
- [ ] 代码实现符合需求
- [ ] 边界条件处理正确
- [ ] 错误处理完整
- [ ] 无逻辑错误
- [ ] 异常场景覆盖完整

#### 审查方法
```typescript
// ❌ 错误示例 - 缺少边界检查
function getUser(id: number): User {
    return users[id]; // 可能越界
}

// ✅ 正确示例
function getUser(id: number): User | null {
    if (id < 0 || id >= users.length) {
        return null;
    }
    return users[id];
}
```

### 步骤 2：代码质量审查

#### 代码规范检查
- [ ] 遵循项目代码规范
- [ ] 命名清晰易懂
- [ ] 函数职责单一（SRP）
- [ ] 代码可复用性好
- [ ] 无重复代码（DRY）

#### 命名规范
```typescript
// ✅ 好的命名
const userName = "john";
function calculateTotalPrice(): number { }
class UserProfile { }

// ❌ 坏的命名
const name = "john"; // 太泛
function calc(): number { } // 不清晰
class Data { } // 无意义
```

#### 函数设计
```typescript
// ❌ 违反单一职责
function processUser(user: User) {
    // 验证用户
    if (!user.name) throw new Error("Invalid name");
    
    // 保存到数据库
    db.save(user);
    
    // 发送邮件
    emailService.send(user.email, "Welcome");
    
    // 记录日志
    logger.info(`User ${user.name} created`);
}

// ✅ 单一职责
function validateUser(user: User): void { }
function saveUser(user: User): void { }
function sendWelcomeEmail(user: User): void { }
function logUserCreation(user: User): void { }
```

### 步骤 3：性能审查

#### 检查项
- [ ] 无明显的性能问题
- [ ] 使用了合适的算法和数据结构
- [ ] 避免不必要的计算
- [ ] 内存管理合理
- [ ] 使用了缓存策略

#### 性能优化示例
```typescript
// ❌ 性能问题 - O(n²)
function findDuplicates(arr: number[]): number[] {
    const duplicates: number[] = [];
    for (let i = 0; i < arr.length; i++) {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] === arr[j]) {
                duplicates.push(arr[i]);
            }
        }
    }
    return duplicates;
}

// ✅ 性能优化 - O(n)
function findDuplicates(arr: number[]): number[] {
    const seen = new Set<number>();
    const duplicates = new Set<number>();
    for (const num of arr) {
        if (seen.has(num)) {
            duplicates.add(num);
        } else {
            seen.add(num);
        }
    }
    return Array.from(duplicates);
}
```

### 步骤 4：安全审查

#### 检查项
- [ ] 输入验证完整
- [ ] 无 SQL 注入风险
- [ ] 无 XSS 漏洞
- [ ] 无 CSRF 风险
- [ ] 敏感信息处理正确
- [ ] 认证授权完整

#### 安全示例
```typescript
// ❌ SQL 注入风险
const query = `SELECT * FROM users WHERE id = ${userId}`;

// ✅ 参数化查询
const query = 'SELECT * FROM users WHERE id = ?';
db.execute(query, [userId]);

// ❌ XSS 风险
res.send(`<div>${userInput}</div>`);

// ✅ 转义输出
res.send(escapeHtml(userInput));

// ❌ 硬编码密钥
const apiKey = 'sk-1234567890';

// ✅ 环境变量
const apiKey = process.env.API_KEY;
```

### 步骤 5：测试审查

#### 检查项
- [ ] 单元测试已编写
- [ ] 测试覆盖率≥80%
- [ ] 核心逻辑覆盖率 100%
- [ ] 测试用例包含边界情况
- [ ] 测试命名清晰
- [ ] 测试可独立运行

#### 测试质量
```typescript
// ❌ 测试不完整
test('should add numbers', () => {
    expect(add(1, 2)).toBe(3);
});

// ✅ 测试完整
describe('add function', () => {
    it('should add positive numbers', () => {
        expect(add(1, 2)).toBe(3);
    });
    
    it('should handle negative numbers', () => {
        expect(add(-1, -2)).toBe(-3);
    });
    
    it('should handle zero', () => {
        expect(add(0, 0)).toBe(0);
    });
    
    it('should throw error for invalid input', () => {
        expect(() => add(null, 1)).toThrow();
    });
});
```

### 步骤 6：文档审查

#### 检查项
- [ ] 函数有必要的注释
- [ ] 复杂逻辑有说明
- [ ] API 文档完整
- [ ] 更新了 CHANGELOG
- [ ] README 已更新

#### 注释质量
```typescript
// ❌ 多余注释
const total = price * quantity; // 计算总价

// ✅ 意图解释
// 使用 Map 而不是 Object，因为性能更好
const userCache = new Map<string, User>();

// ✅ JSDoc 文档
/**
 * 计算订单总价
 * @param items - 商品列表
 * @param discount - 折扣率（0-1）
 * @returns 折后总价
 * @throws Error 当折扣率超出范围时
 */
function calculateTotal(
    items: OrderItem[],
    discount: number
): number { }
```

## 📤 输出格式

### 代码审查反馈模板

```markdown
## 代码审查报告

### ✅ 优点
- [列出做得好的地方]

### ⚠️ 需要改进

#### 高优先级（必须修复）
1. **问题描述**
   - 位置：`[文件路径：行号]`
   - 严重性：🔴 严重
   - 建议：[改进建议]
   - 原因：[为什么需要改]
   - 示例：
   ```typescript
   // ❌ 原代码
   // ✅ 修改后
   ```

2. **问题描述**
   ...

#### 中优先级（建议修复）
1. **问题描述**
   - 位置：`[文件路径：行号]`
   - 严重性：🟡 中等
   - 建议：[改进建议]
   - 原因：[为什么需要改]

#### 低优先级（可选优化）
1. **问题描述**
   - 位置：`[文件路径：行号]`
   - 严重性：🟢 轻微
   - 建议：[改进建议]

### 📝 建议
- [可选的优化建议]

### 🧪 测试要求
- [ ] 添加 XX 场景的测试
- [ ] 补充边界条件测试
- [ ] 提高测试覆盖率到 XX%

### 📊 评分
| 维度 | 评分 | 说明 |
|------|------|------|
| 功能正确性 | ⭐⭐⭐⭐⭐ | 5/5 |
| 代码质量 | ⭐⭐⭐⭐☆ | 4/5 |
| 性能 | ⭐⭐⭐☆☆ | 3/5 |
| 安全性 | ⭐⭐⭐⭐⭐ | 5/5 |
| 测试覆盖 | ⭐⭐⭐☆☆ | 3/5 |
| 文档完整性 | ⭐⭐⭐⭐☆ | 4/5 |
| **总体评分** | **⭐⭐⭐⭐☆** | **4.2/5** |

### ✅ 审查结论
- [ ] 通过，可以合并
- [ ] 有条件通过，需修复中优先级问题
- [ ] 不通过，需修复高优先级问题
```

## ✅ 质量门禁

### 审查完整性检查
- [ ] 功能正确性已审查
- [ ] 代码质量已审查
- [ ] 性能已审查
- [ ] 安全性已审查
- [ ] 测试已审查
- [ ] 文档已审查

### 问题分级标准
- **高优先级**：影响功能、安全、严重性能问题
- **中优先级**：代码质量、可维护性问题
- **低优先级**：代码风格、优化建议

## 📝 示例交互

### 示例 1：登录功能审查

**用户**：
```
请审查这个登录功能的代码：

```typescript
async function login(username: string, password: string) {
    const user = db.query(`SELECT * FROM users WHERE username = '${username}'`);
    
    if (user.password === password) {
        return { token: 'token_' + user.id };
    }
    
    return null;
}
```
```

**Code Reviewer**：
```
## 代码审查报告 - 登录功能

### ⚠️ 需要改进

#### 高优先级（必须修复）

1. **SQL 注入漏洞** 🔴 严重
   - 位置：`login.ts:2`
   - 问题：直接使用字符串拼接 SQL
   - 建议：使用参数化查询
   - 示例：
   ```typescript
   // ❌ 原代码
   const user = db.query(`SELECT * FROM users WHERE username = '${username}'`);
   
   // ✅ 修改后
   const user = await db.query(
       'SELECT * FROM users WHERE username = ?',
       [username]
   );
   ```

2. **密码明文比较** 🔴 严重
   - 位置：`login.ts:4`
   - 问题：密码未加密存储和比较
   - 建议：使用 bcrypt 加密
   - 示例：
   ```typescript
   // ❌ 原代码
   if (user.password === password) {
   
   // ✅ 修改后
   const passwordMatches = await bcrypt.compare(password, user.passwordHash);
   if (passwordMatches) {
   ```

3. **Token 生成不安全** 🔴 严重
   - 位置：`login.ts:5`
   - 问题：Token 可预测，无过期时间
   - 建议：使用 JWT
   - 示例：
   ```typescript
   // ❌ 原代码
   return { token: 'token_' + user.id };
   
   // ✅ 修改后
   const token = jwt.sign(
       { userId: user.id, username: user.username },
       process.env.JWT_SECRET,
       { expiresIn: '2h' }
   );
   return { token };
   ```

#### 中优先级（建议修复）

1. **缺少输入验证** 🟡 中等
   - 位置：`login.ts:1`
   - 问题：未验证用户名和密码格式
   - 建议：添加输入验证
   ```typescript
   if (!username || !password) {
       throw new ValidationError('用户名和密码不能为空');
   }
   ```

2. **缺少错误处理** 🟡 中等
   - 位置：`login.ts:1-8`
   - 问题：未处理数据库异常
   - 建议：添加 try-catch
   ```typescript
   try {
       const user = await db.query(...);
   } catch (error) {
       logger.error('登录失败', error);
       throw new DatabaseError('数据库错误');
   }
   ```

3. **缺少类型定义** 🟡 中等
   - 问题：返回值类型不明确
   - 建议：定义接口
   ```typescript
   interface LoginResult {
       token: string;
       user: {
           id: number;
           username: string;
       };
   }
   
   async function login(username: string, password: string): Promise<LoginResult>
   ```

#### 低优先级（可选优化）

1. **添加登录日志** 🟢 轻微
   - 建议：记录登录成功/失败日志
   ```typescript
   await loginLogRepository.create({
       userId: user.id,
       loginTime: new Date(),
       success: true,
       ip: req.ip
   });
   ```

### 📊 评分
| 维度 | 评分 | 说明 |
|------|------|------|
| 功能正确性 | ⭐⭐☆☆☆ | 2/5 - 逻辑不完整 |
| 代码质量 | ⭐⭐☆☆☆ | 2/5 - 缺少类型和错误处理 |
| 性能 | ⭐⭐⭐☆☆ | 3/5 - 无明显性能问题 |
| 安全性 | ⭐☆☆☆☆ | 1/5 - 存在严重安全漏洞 |
| 测试覆盖 | ⭐☆☆☆☆ | 1/5 - 无测试 |
| 文档完整性 | ⭐☆☆☆☆ | 1/5 - 无注释和文档 |
| **总体评分** | **⭐⭐☆☆☆** | **1.7/5** |

### ✅ 审查结论
- [ ] 通过，可以合并
- [ ] 有条件通过，需修复中优先级问题
- [x] **不通过，需修复高优先级问题**

**必须修复的问题**：
1. SQL 注入漏洞
2. 密码明文比较
3. Token 生成不安全

修复后请重新提交审查。
```

## 🎯 使用建议

### 何时调用
- 代码编写完成后
- 提交 PR/MR 时
- 重构代码后
- 修复 Bug 后
- 性能优化后

### 调用指令模板
```
请使用 code-reviewer 技能审查以下代码：
- 文件路径：[路径]
- 功能说明：[描述]
- 审查重点：[安全性/性能/代码质量等]

[粘贴代码]
```

### 与其他技能协作
- **前置** `cc-godmode` - 生成代码
- **前置** `tdd-guide` - 编写测试
- **后接** `quality-validator` - 质量验证

## 📚 参考文档

- 04-代码审查.md
- 02-编码检查清单.md
- 01-注释规范.md
- 02-设计原则.md
- 安全编码最佳实践

---

**版本**: 1.0.0  
**更新日期**: 2026-03-25  
**维护者**: AI Assistant