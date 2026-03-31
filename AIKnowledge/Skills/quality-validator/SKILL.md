---
name: quality-validator
description: 测试验证专家，负责 TDD 测试驱动开发、单元测试、集成测试、测试覆盖率验证和质量门禁检查。在代码编写过程中和完成后调用此技能进行测试验证。
---

# 测试验证专家 (Quality Validator)

## 📋 技能概述

专业测试验证技能，基于 TDD（测试驱动开发）方法和四层测试体系，确保代码质量、测试覆盖率和功能正确性。严格遵守 RED-GREEN-REFACTOR 循环。

## 🎯 适用场景

- ✅ 创建新文件后
- ✅ 编写新功能后
- ✅ 修改现有代码后
- ✅ 修复 Bug 后
- ✅ 需要 TDD 测试
- ✅ 需要验证测试覆盖率
- ✅ 需要运行质量门禁检查

## 🔄 工作流程

### 步骤 1：TDD 测试驱动开发（强制）

#### TDD 循环（严格遵守）
```
1. RED     - 先写测试，测试应该失败 ❌
2. GREEN   - 写最少代码让测试通过 ✅
3. REFACTOR - 重构代码保持测试通过 🔧
```

#### 开发顺序（必须严格遵守）
```
步骤 1: 编写测试用例 (.test.ts)
         ↓
步骤 2: 运行测试，验证失败 (RED)
         ↓
步骤 3: 编写实现代码 (.ts)
         ↓
步骤 4: 运行测试，验证通过 (GREEN)
         ↓
步骤 5: 重构优化 (REFACTOR)
         ↓
步骤 6: 重复步骤 1-5
```

#### AAA 测试模式
```typescript
// Arrange - 准备数据
const input = 5;
const expected = 10;

// Act - 执行代码
const result = double(input);

// Assert - 验证结果
expect(result).toBe(expected);
```

### 步骤 2：单元测试

#### 测试覆盖率要求
- **整体覆盖率**：≥ 80%
- **核心逻辑覆盖率**：100%
- **分支覆盖**：≥ 80%
- **边界条件测试**：必须覆盖

#### 测试命名规范
```typescript
// 格式：should_[预期行为]_when_[条件]
describe('UserService', () => {
    describe('login', () => {
        it('should_return_token_when_credentials_valid', async () => { });
        it('should_throw_error_when_password_incorrect', async () => { });
        it('should_throw_error_when_user_not_found', async () => { });
        it('should_lock_account_after_5_failed_attempts', async () => { });
    });
});
```

#### 测试结构
```typescript
describe('组件名/模块名', () => {
    describe('方法名', () => {
        it('应该 [预期行为] 当 [条件]', () => {
            // Arrange
            // Act
            // Assert
        });
    });
});
```

### 步骤 3：集成测试

#### 测试范围
- [ ] 模块间接口测试
- [ ] 数据传递测试
- [ ] 事务处理测试
- [ ] 第三方集成测试

#### 集成测试示例
```typescript
describe('Order Integration Test', () => {
    it('should_complete_order_flow', async () => {
        // 1. 创建用户
        const user = await userService.register(userData);
        
        // 2. 创建商品
        const product = await productService.create(productData);
        
        // 3. 创建订单
        const order = await orderService.create(user.id, [product]);
        
        // 4. 支付订单
        await paymentService.pay(order.id, paymentInfo);
        
        // 5. 验证订单状态
        expect(order.status).toBe('PAID');
    });
});
```

### 步骤 4：系统测试

#### 测试类型
- **功能测试**：验证所有功能需求
- **性能测试**：验证性能指标
- **安全测试**：验证安全机制
- **兼容性测试**：验证浏览器/设备兼容性

#### 性能测试示例
```typescript
describe('Performance Test', () => {
    it('should_respond_within_200ms', async () => {
        const start = Date.now();
        await api.get('/api/products');
        const duration = Date.now() - start;
        
        expect(duration).toBeLessThan(200);
    });
    
    it('should_handle_1000_concurrent_users', async () => {
        const promises = Array(1000).fill(null).map(() => 
            api.get('/api/products')
        );
        
        const results = await Promise.all(promises);
        expect(results.every(r => r.status === 200)).toBe(true);
    });
});
```

### 步骤 5：验收测试

#### 验收标准验证
- [ ] 功能验收：所有功能需求已实现
- [ ] 性能验收：性能指标达标
- [ ] 安全验收：安全测试通过
- [ ] 用户验收：业务流程验证通过

#### 验收测试示例
```typescript
describe('Acceptance Test - User Login', () => {
    it('should_allow_user_to_login', async () => {
        // 前置条件：用户已注册
        await authService.register({
            username: 'testuser',
            email: 'test@example.com',
            password: 'Password123!'
        });
        
        // 执行登录
        const response = await authService.login({
            username: 'testuser',
            password: 'Password123!'
        });
        
        // 验收标准
        expect(response.token).toBeDefined();
        expect(response.user.username).toBe('testuser');
        expect(response.user.email).toBe('test@example.com');
    });
});
```

### 步骤 6：质量门禁检查

#### 验证命令
```bash
# 代码质量检查
npm run lint

# TypeScript 类型检查
npm run type-check

# 运行测试
npm run test

# 测试覆盖率检查
npm run test:coverage

# 构建验证
npm run build
```

#### 质量门禁标准
- [ ] ESLint 检查通过
- [ ] TypeScript 编译通过
- [ ] 所有测试通过
- [ ] 测试覆盖率≥80%
- [ ] 构建成功

## 📤 输出格式

### 测试验证报告模板

```markdown
## 测试验证报告

### 📊 测试结果

#### 单元测试
- 总测试数：[X]
- 通过：[X]
- 失败：[X]
- 跳过：[X]
- 通过率：[X]%

#### 集成测试
- 总测试数：[X]
- 通过：[X]
- 失败：[X]
- 通过率：[X]%

#### 系统测试
- 功能测试：[X]/[X] 通过
- 性能测试：[X]/[X] 通过
- 安全测试：[X]/[X] 通过

### 📈 测试覆盖率

| 类型 | 覆盖率 | 目标 | 状态 |
|------|--------|------|------|
| 语句覆盖率 | [X]% | 80% | ✅/❌ |
| 分支覆盖率 | [X]% | 80% | ✅/❌ |
| 函数覆盖率 | [X]% | 80% | ✅/❌ |
| 行覆盖率 | [X]% | 80% | ✅/❌ |

### ✅ 质量门禁

| 检查项 | 状态 | 说明 |
|--------|------|------|
| ESLint | ✅/❌ | [说明] |
| TypeScript | ✅/❌ | [说明] |
| 单元测试 | ✅/❌ | [说明] |
| 集成测试 | ✅/❌ | [说明] |
| 测试覆盖率 | ✅/❌ | [说明] |
| 构建 | ✅/❌ | [说明] |

### 🧪 测试用例详情

#### 通过的测试
- [x] 测试用例 1
- [x] 测试用例 2

#### 失败的测试
- [ ] 测试用例 3
  - 错误信息：[错误详情]
  - 失败原因：[分析]
  - 修复建议：[建议]

### 📝 改进建议

#### 高优先级
- [ ] 添加 XX 场景的测试
- [ ] 补充边界条件测试

#### 中优先级
- [ ] 提高 XX 模块的测试覆盖率
- [ ] 优化测试执行速度

### ✅ 验证结论
- [ ] 通过，所有测试和检查都通过
- [ ] 有条件通过，需修复非关键问题
- [ ] 不通过，有关键测试失败或覆盖率不达标
```

## ✅ 质量门禁

### TDD 执行检查
- [ ] 先编写了测试用例
- [ ] 测试用例在实现前失败（RED）
- [ ] 编写了实现代码
- [ ] 测试通过（GREEN）
- [ ] 代码已重构优化
- [ ] 测试覆盖率≥80%

### 测试完整性检查
- [ ] 单元测试已编写
- [ ] 集成测试已编写
- [ ] 系统测试已执行
- [ ] 验收测试已执行
- [ ] 边界条件已测试
- [ ] 异常处理已测试

### 覆盖率要求
- [ ] 语句覆盖率≥80%
- [ ] 分支覆盖率≥80%
- [ ] 函数覆盖率≥80%
- [ ] 行覆盖率≥80%
- [ ] 核心逻辑覆盖率 100%

## 📝 示例交互

### 示例 1：TDD 测试驱动开发

**用户**：
```
请使用 TDD 方式实现一个用户注册功能：
- 验证邮箱格式
- 验证密码强度（至少 8 位，包含大小写字母和数字）
- 检查邮箱是否已注册
- 保存用户信息
```

**Quality Validator**：
```
## TDD 测试驱动开发 - 用户注册功能

### 步骤 1: RED - 编写测试（测试失败）

```typescript
// user.service.test.ts
import { UserService } from './user.service';
import { ValidationError } from '../errors';

describe('UserService', () => {
    let userService: UserService;
    
    beforeEach(() => {
        userService = new UserService();
    });
    
    describe('register', () => {
        it('should_throw_error_when_email_invalid', async () => {
            // Arrange
            const invalidEmail = 'invalid-email';
            
            // Act & Assert
            await expect(
                userService.register({
                    email: invalidEmail,
                    password: 'Password123!',
                    username: 'testuser'
                })
            ).rejects.toThrow(ValidationError);
        });
        
        it('should_throw_error_when_password_too_short', async () => {
            // Arrange
            const weakPassword = 'Ab1';
            
            // Act & Assert
            await expect(
                userService.register({
                    email: 'test@example.com',
                    password: weakPassword,
                    username: 'testuser'
                })
            ).rejects.toThrow(ValidationError);
        });
        
        it('should_throw_error_when_password_missing_uppercase', async () => {
            // Arrange
            const weakPassword = 'password123';
            
            // Act & Assert
            await expect(
                userService.register({
                    email: 'test@example.com',
                    password: weakPassword,
                    username: 'testuser'
                })
            ).rejects.toThrow(ValidationError);
        });
        
        it('should_register_user_when_data_valid', async () => {
            // Arrange
            const validData = {
                email: 'test@example.com',
                password: 'Password123!',
                username: 'testuser'
            };
            
            // Act
            const user = await userService.register(validData);
            
            // Assert
            expect(user.email).toBe('test@example.com');
            expect(user.username).toBe('testuser');
            expect(user.password).not.toBe('Password123!'); // 已加密
        });
    });
});
```

**运行测试**：
```bash
$ npm run test

 FAIL  user.service.test.ts
  UserService
    register
      ✗ should_throw_error_when_email_invalid
        Expected function to throw, but it did not
      ✗ should_throw_error_when_password_too_short
        Expected function to throw, but it did not
      ✗ should_throw_error_when_password_missing_uppercase
        Expected function to throw, but it did not
      ✗ should_register_user_when_data_valid
        TypeError: Cannot read property 'email' of undefined

Tests: 4 failed, 0 passed
```

### 步骤 2: GREEN - 编写实现代码

```typescript
// user.service.ts
import { ValidationError } from '../errors';
import bcrypt from 'bcrypt';

export class UserService {
    async register(data: RegisterDTO): Promise<User> {
        // 验证邮箱格式
        if (!this.isValidEmail(data.email)) {
            throw new ValidationError('邮箱格式不正确');
        }
        
        // 验证密码强度
        if (!this.isStrongPassword(data.password)) {
            throw new ValidationError('密码强度不足');
        }
        
        // 检查邮箱是否已注册
        const existingUser = await this.findByEmail(data.email);
        if (existingUser) {
            throw new ValidationError('邮箱已被注册');
        }
        
        // 加密密码
        const passwordHash = await bcrypt.hash(data.password, 10);
        
        // 保存用户
        const user = await this.userRepository.create({
            email: data.email,
            username: data.username,
            passwordHash
        });
        
        return user;
    }
    
    private isValidEmail(email: string): boolean {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return emailRegex.test(email);
    }
    
    private isStrongPassword(password: string): boolean {
        // 至少 8 位，包含大小写字母和数字
        const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;
        return passwordRegex.test(password);
    }
    
    private async findByEmail(email: string): Promise<User | null> {
        return this.userRepository.findOne({ email });
    }
}
```

**运行测试**：
```bash
$ npm run test

 PASS  user.service.test.ts
  UserService
    register
      ✓ should_throw_error_when_email_invalid (15ms)
      ✓ should_throw_error_when_password_too_short (10ms)
      ✓ should_throw_error_when_password_missing_uppercase (8ms)
      ✓ should_register_user_when_data_valid (45ms)

Tests: 4 passed, 0 failed
```

### 步骤 3: REFACTOR - 重构优化

```typescript
// 重构后的代码 - 提取验证逻辑到单独的类
import { ValidationError } from '../errors';
import bcrypt from 'bcrypt';
import { UserValidator } from './user.validator';

export class UserService {
    constructor(
        private userRepository: UserRepository,
        private validator: UserValidator = new UserValidator()
    ) {}
    
    async register(data: RegisterDTO): Promise<User> {
        // 验证数据
        this.validator.validateRegisterData(data);
        
        // 检查邮箱是否已注册
        await this.checkEmailExists(data.email);
        
        // 加密密码
        const passwordHash = await this.hashPassword(data.password);
        
        // 保存用户
        return this.createUser(data, passwordHash);
    }
    
    private async checkEmailExists(email: string): Promise<void> {
        const existingUser = await this.userRepository.findOne({ email });
        if (existingUser) {
            throw new ValidationError('邮箱已被注册');
        }
    }
    
    private async hashPassword(password: string): Promise<string> {
        return bcrypt.hash(password, 10);
    }
    
    private async createUser(data: RegisterDTO, passwordHash: string): Promise<User> {
        return this.userRepository.create({
            email: data.email,
            username: data.username,
            passwordHash
        });
    }
}
```

**再次运行测试**：
```bash
$ npm run test

 PASS  user.service.test.ts
  UserService
    register
      ✓ should_throw_error_when_email_invalid (12ms)
      ✓ should_throw_error_when_password_too_short (8ms)
      ✓ should_throw_error_when_password_missing_uppercase (7ms)
      ✓ should_register_user_when_data_valid (42ms)

Tests: 4 passed, 0 failed
```

### 测试覆盖率报告

```bash
$ npm run test:coverage

-------------------|---------|----------|---------|---------|
File               | % Stmts | % Branch | % Funcs | % Lines |
-------------------|---------|----------|---------|---------|
All files          |   92.31 |    85.71 |     100 |   91.89 |
 user.service.ts   |     100 |      100 |     100 |     100 |
 user.validator.ts |   88.89 |    83.33 |     100 |   88.24 |
-------------------|---------|----------|---------|---------|

✅ 测试覆盖率达标（目标：80%）
```

### 质量门禁检查

```bash
$ npm run lint
✔ No lint errors found

$ npm run type-check
✔ TypeScript compilation successful

$ npm run test
✔ All tests passed (4/4)

$ npm run test:coverage
✔ Coverage: 92.31% (target: 80%)

$ npm run build
✔ Build successful
```

### ✅ 验证结论
- [x] 通过，所有测试和检查都通过
- TDD 循环完整执行（RED-GREEN-REFACTOR）
- 测试覆盖率 92.31% > 80%
- 所有质量门禁通过
```

## 🎯 使用建议

### 何时调用
- 创建新文件后（强制）
- 编写新功能后（强制）
- 修改代码后（强制）
- 修复 Bug 后（强制）
- 需要 TDD 测试时
- 需要验证测试覆盖率时

### 调用指令模板
```
请使用 quality-validator 技能对 [文件名/功能] 进行测试验证：
- 文件路径：[路径]
- 功能说明：[描述]
- 测试类型：[单元测试/集成测试/系统测试]
- 特殊要求：[描述]
```

### 与其他技能协作
- **前置** `cc-godmode` - 生成代码
- **前置** `code-reviewer` - 代码审查
- **后接** `tdd-guide` - 深入 TDD 测试

## 📚 参考文档

- WF-05 测试质量
- 01-测试验证规范.md
- 01-测试验证检查清单.md
- 02-tdd-guide.md
- 09-单元测试.md
- 10-测试质量.md
- CK-04 测试检查清单

---

**版本**: 1.0.0  
**更新日期**: 2026-03-25  
**维护者**: AI Assistant