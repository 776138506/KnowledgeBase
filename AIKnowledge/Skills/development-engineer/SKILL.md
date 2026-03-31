---
name: development-engineer
description: 开发实现专家，负责接口实现、编码开发、单元测试编写和开发日志记录。在系统设计完成后进行代码实现时调用此技能。
---

# 开发实现专家 (Development Engineer)

## 📋 技能概述

专业开发实现技能，基于编码规范和最佳实践，负责将设计转化为高质量代码，包括接口实现、单元测试编写、开发日志记录和代码优化。

## 🎯 适用场景

- ✅ 系统设计完成后需要编码实现
- ✅ 需要实现接口定义
- ✅ 需要编写单元测试
- ✅ 需要记录开发日志
- ✅ 需要代码重构优化
- ✅ 需要实现业务逻辑

## 🔄 工作流程

### 步骤 1：理解设计文档

#### 输入文档
- 系统设计文档
- 接口定义文档
- 数据库设计文档
- 类图设计

#### 理解要点
- [ ] 接口职责和方法签名
- [ ] 数据模型和关系
- [ ] 业务流程和处理逻辑
- [ ] 异常处理要求
- [ ] 性能和安全要求

### 步骤 2：接口实现

#### 实现原则
- **遵循接口契约**：严格按照接口定义实现
- **单一职责**：每个函数只做一件事
- **错误处理**：完整的异常捕获和处理
- **日志记录**：关键操作记录日志
- **类型安全**：使用 TypeScript 类型系统

#### 实现示例
```typescript
// 接口定义
interface IUserService {
    login(username: string, password: string): Promise<LoginResult>;
    register(userData: RegisterDTO): Promise<User>;
    getUserById(id: number): Promise<User>;
}

// 接口实现
import { IUserService } from '../interfaces/IUserService';
import { UserRepository } from '../repositories/UserRepository';
import { bcrypt } from '../utils/bcrypt';
import { jwt } from '../utils/jwt';
import { ValidationError, AuthenticationError } from '../errors';
import { logger } from '../utils/logger';

export class UserService implements IUserService {
    constructor(private userRepository: UserRepository) {}

    /**
     * 用户登录
     */
    async login(username: string, password: string): Promise<LoginResult> {
        logger.info(`用户登录尝试：${username}`);

        // 1. 验证输入
        this.validateLoginInput(username, password);

        // 2. 查询用户
        const user = await this.userRepository.findByUsername(username);
        if (!user) {
            logger.warn(`用户不存在：${username}`);
            throw new AuthenticationError('用户名或密码错误');
        }

        // 3. 验证密码
        const passwordMatches = await bcrypt.compare(password, user.passwordHash);
        if (!passwordMatches) {
            logger.warn(`密码错误：${username}`);
            throw new AuthenticationError('用户名或密码错误');
        }

        // 4. 生成 Token
        const token = jwt.sign(
            { userId: user.id, username: user.username },
            process.env.JWT_SECRET!,
            { expiresIn: '2h' }
        );

        logger.info(`用户登录成功：${username}`);

        return {
            token,
            user: {
                id: user.id,
                username: user.username,
                email: user.email
            }
        };
    }

    /**
     * 用户注册
     */
    async register(userData: RegisterDTO): Promise<User> {
        logger.info(`用户注册：${userData.username}`);

        // 1. 验证输入
        this.validateRegisterData(userData);

        // 2. 检查邮箱是否已存在
        const existingUser = await this.userRepository.findByEmail(userData.email);
        if (existingUser) {
            throw new ValidationError('邮箱已被注册');
        }

        // 3. 加密密码
        const passwordHash = await bcrypt.hash(userData.password, 10);

        // 4. 创建用户
        const user = await this.userRepository.create({
            username: userData.username,
            email: userData.email,
            passwordHash
        });

        logger.info(`用户注册成功：${userData.username}`);

        return user;
    }

    /**
     * 根据 ID 获取用户
     */
    async getUserById(id: number): Promise<User> {
        const user = await this.userRepository.findById(id);
        if (!user) {
            throw new ValidationError('用户不存在');
        }
        return user;
    }

    /**
     * 验证登录输入
     */
    private validateLoginInput(username: string, password: string): void {
        if (!username || !password) {
            throw new ValidationError('用户名和密码不能为空');
        }
        if (username.length < 3 || username.length > 20) {
            throw new ValidationError('用户名长度必须在 3-20 位之间');
        }
    }

    /**
     * 验证注册数据
     */
    private validateRegisterData(userData: RegisterDTO): void {
        if (!userData.username || !userData.email || !userData.password) {
            throw new ValidationError('必填字段不能为空');
        }

        // 验证邮箱格式
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(userData.email)) {
            throw new ValidationError('邮箱格式不正确');
        }

        // 验证密码强度
        const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;
        if (!passwordRegex.test(userData.password)) {
            throw new ValidationError('密码必须包含大小写字母和数字，至少 8 位');
        }
    }
}
```

### 步骤 3：单元测试编写

#### 测试原则
- **AAA 模式**：Arrange-Act-Assert
- **独立运行**：测试之间相互独立
- **可重复性**：测试结果可重现
- **覆盖全面**：正常流程 + 异常流程

#### 测试示例
```typescript
// user.service.test.ts
import { UserService } from './UserService';
import { UserRepository } from '../repositories/UserRepository';
import { ValidationError, AuthenticationError } from '../errors';
import { User } from '../entities/User';

describe('UserService', () => {
    let userService: UserService;
    let userRepository: jest.Mocked<UserRepository>;

    beforeEach(() => {
        userRepository = {
            findByUsername: jest.fn(),
            findByEmail: jest.fn(),
            findById: jest.fn(),
            create: jest.fn()
        } as any;
        userService = new UserService(userRepository);
    });

    describe('login', () => {
        it('should_throw_error_when_username_empty', async () => {
            // Arrange
            const username = '';
            const password = 'Password123!';

            // Act & Assert
            await expect(userService.login(username, password))
                .rejects
                .toThrow(ValidationError);
        });

        it('should_throw_error_when_password_empty', async () => {
            // Arrange
            const username = 'john';
            const password = '';

            // Act & Assert
            await expect(userService.login(username, password))
                .rejects
                .toThrow(ValidationError);
        });

        it('should_throw_error_when_user_not_found', async () => {
            // Arrange
            userRepository.findByUsername.mockResolvedValue(null);

            // Act & Assert
            await expect(userService.login('john', 'Password123!'))
                .rejects
                .toThrow(AuthenticationError);
        });

        it('should_throw_error_when_password_incorrect', async () => {
            // Arrange
            const mockUser = {
                id: 1,
                username: 'john',
                email: 'john@example.com',
                passwordHash: '$2b$10$...' // bcrypt hash of 'correct_password'
            };
            userRepository.findByUsername.mockResolvedValue(mockUser);

            // Act & Assert
            await expect(userService.login('john', 'wrong_password'))
                .rejects
                .toThrow(AuthenticationError);
        });

        it('should_return_token_when_login_successful', async () => {
            // Arrange
            const mockUser = {
                id: 1,
                username: 'john',
                email: 'john@example.com',
                passwordHash: '$2b$10$...' // bcrypt hash of 'Password123!'
            };
            userRepository.findByUsername.mockResolvedValue(mockUser);

            // Act
            const result = await userService.login('john', 'Password123!');

            // Assert
            expect(result).toBeDefined();
            expect(result.token).toBeDefined();
            expect(result.user.id).toBe(1);
            expect(result.user.username).toBe('john');
        });
    });

    describe('register', () => {
        it('should_throw_error_when_email_invalid', async () => {
            // Arrange
            const userData = {
                username: 'john',
                email: 'invalid-email',
                password: 'Password123!'
            };

            // Act & Assert
            await expect(userService.register(userData))
                .rejects
                .toThrow(ValidationError);
        });

        it('should_throw_error_when_password_weak', async () => {
            // Arrange
            const userData = {
                username: 'john',
                email: 'john@example.com',
                password: 'weak'
            };

            // Act & Assert
            await expect(userService.register(userData))
                .rejects
                .toThrow(ValidationError);
        });

        it('should_throw_error_when_email_exists', async () => {
            // Arrange
            const userData = {
                username: 'john',
                email: 'john@example.com',
                password: 'Password123!'
            };
            const existingUser = { id: 1, email: 'john@example.com' };
            userRepository.findByEmail.mockResolvedValue(existingUser);

            // Act & Assert
            await expect(userService.register(userData))
                .rejects
                .toThrow(ValidationError);
        });

        it('should_create_user_when_data_valid', async () => {
            // Arrange
            const userData = {
                username: 'john',
                email: 'john@example.com',
                password: 'Password123!'
            };
            userRepository.findByEmail.mockResolvedValue(null);
            userRepository.create.mockResolvedValue({
                id: 1,
                username: 'john',
                email: 'john@example.com'
            });

            // Act
            const user = await userService.register(userData);

            // Assert
            expect(user).toBeDefined();
            expect(user.id).toBe(1);
            expect(user.username).toBe('john');
            expect(userRepository.create).toHaveBeenCalledWith(
                expect.objectContaining({
                    username: 'john',
                    email: 'john@example.com'
                })
            );
        });
    });
});
```

### 步骤 4：开发日志记录

#### 日志内容
- 功能概述
- 实现细节
- 关键代码
- 测试覆盖
- 设计决策
- TODO 列表

#### 日志示例
```markdown
# 开发日志 - 用户登录功能

## 基本信息
**日期**: 2026-03-25  
**开发者**: AI Assistant  
**版本**: v1.0.0  
**文件**: `src/services/UserService.ts`

## 功能概述

### 业务背景
用户需要安全的登录功能，支持用户名密码认证，包含防暴力破解机制。

### 实现目标
1. 实现用户登录验证
2. 生成 JWT token
3. 防止暴力破解
4. 记录登录日志

## 函数实现

### login 函数

**位置**: `src/services/UserService.ts:15-80`

**职责**: 验证用户凭据并生成 JWT token

**参数**:
| 参数名 | 类型 | 说明 |
|--------|------|------|
| username | string | 用户名 |
| password | string | 密码 |

**返回值**: `Promise<LoginResult>` - 包含 token 和用户信息

**实现逻辑**:
1. 验证输入参数
2. 查询用户信息
3. 验证密码
4. 生成 JWT token
5. 返回登录结果

**关键代码**:
```typescript
async login(username: string, password: string): Promise<LoginResult> {
    this.validateLoginInput(username, password);
    
    const user = await this.userRepository.findByUsername(username);
    if (!user) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const passwordMatches = await bcrypt.compare(password, user.passwordHash);
    if (!passwordMatches) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const token = jwt.sign(
        { userId: user.id, username: user.username },
        process.env.JWT_SECRET!,
        { expiresIn: '2h' }
    );
    
    return { token, user };
}
```

## API 文档

```typescript
/**
 * 用户登录
 * @param username - 用户名
 * @param password - 密码
 * @returns 登录结果
 * @throws AuthenticationError 用户名或密码错误
 */
async function login(
    username: string,
    password: string
): Promise<LoginResult>
```

## 测试覆盖

### 单元测试
- [x] 用户名为空
- [x] 密码为空
- [x] 用户不存在
- [x] 密码错误
- [x] 登录成功

### 测试覆盖率
- 语句覆盖率：95%
- 分支覆盖率：90%
- 函数覆盖率：100%

## 设计决策

**密码验证**：使用 bcrypt 比较密码
- 原因：bcrypt 安全，防止暴力破解

**错误信息**：统一返回"用户名或密码错误"
- 原因：防止信息泄露

## TODO

- [ ] 实现账户锁定机制
- [ ] 添加登录日志记录
- [ ] 支持图形验证码
```

### 步骤 5：代码重构优化

#### 重构原则
- **保持测试通过**：重构前后测试都通过
- **小步前进**：每次只重构一小部分
- **持续改进**：发现坏味道就重构

#### 重构示例
```typescript
// 重构前 - 代码重复
async function login(username: string, password: string): Promise<LoginResult> {
    if (!username || !password) {
        throw new ValidationError('用户名和密码不能为空');
    }
    if (username.length < 3 || username.length > 20) {
        throw new ValidationError('用户名长度必须在 3-20 位之间');
    }
    
    const user = await this.userRepository.findByUsername(username);
    if (!user) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const passwordMatches = await bcrypt.compare(password, user.passwordHash);
    if (!passwordMatches) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const token = jwt.sign(
        { userId: user.id, username: user.username },
        process.env.JWT_SECRET!,
        { expiresIn: '2h' }
    );
    
    return { token, user };
}

// 重构后 - 提取验证方法
async function login(username: string, password: string): Promise<LoginResult> {
    this.validateLoginInput(username, password);
    
    const user = await this.userRepository.findByUsername(username);
    if (!user) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const passwordMatches = await bcrypt.compare(password, user.passwordHash);
    if (!passwordMatches) {
        throw new AuthenticationError('用户名或密码错误');
    }
    
    const token = jwt.sign(
        { userId: user.id, username: user.username },
        process.env.JWT_SECRET!,
        { expiresIn: '2h' }
    );
    
    return { token, user };
}

private validateLoginInput(username: string, password: string): void {
    if (!username || !password) {
        throw new ValidationError('用户名和密码不能为空');
    }
    if (username.length < 3 || username.length > 20) {
        throw new ValidationError('用户名长度必须在 3-20 位之间');
    }
}
```

### 步骤 6：代码质量检查

#### 检查项
- [ ] 遵循编码规范
- [ ] 命名清晰易懂
- [ ] 函数职责单一
- [ ] 错误处理完整
- [ ] 日志记录适当
- [ ] 类型定义完整
- [ ] 注释必要且准确

## 📤 输出格式

### 开发实现报告模板

```markdown
## 开发实现报告

### 📋 实现信息

**功能名称**: [功能名称]  
**实现日期**: YYYY-MM-DD  
**开发人员**: [姓名]  
**文件列表**: 
- `src/services/UserService.ts`
- `src/services/UserService.test.ts`

### ✅ 实现内容

#### 接口实现
- [x] login(username, password): LoginResult
- [x] register(userData): User
- [x] getUserById(id): User

#### 单元测试
- [x] 正常流程测试
- [x] 异常流程测试
- [x] 边界条件测试

#### 测试覆盖率
| 类型 | 覆盖率 | 目标 | 状态 |
|------|--------|------|------|
| 语句覆盖率 | [X]% | 80% | ✅ |
| 分支覆盖率 | [X]% | 80% | ✅ |
| 函数覆盖率 | [X]% | 80% | ✅ |

### 📝 开发日志

[开发日志内容]

### 🔧 重构优化

#### 重构内容
- [x] 提取验证方法
- [x] 消除代码重复
- [x] 优化错误处理

### ✅ 质量检查

#### 代码规范
- [x] 遵循命名规范
- [x] 遵循代码格式
- [x] 无重复代码

#### 错误处理
- [x] 异常捕获适当
- [x] 错误日志完整

#### 安全性
- [x] 输入已验证
- [x] 无安全漏洞
- [x] 无硬编码密钥

### ✅ 实现结论
- [x] 通过，代码质量达标
- [ ] 有条件通过，需修复以下问题
- [ ] 不通过，需重构
```

## ✅ 质量门禁

### 代码质量检查
- [ ] 遵循编码规范
- [ ] 命名清晰易懂
- [ ] 函数职责单一
- [ ] 错误处理完整
- [ ] 日志记录适当

### 测试覆盖检查
- [ ] 单元测试已编写
- [ ] 测试覆盖率≥80%
- [ ] 核心逻辑覆盖率 100%
- [ ] 所有测试通过

### 文档完整性检查
- [ ] 开发日志已记录
- [ ] API 文档完整
- [ ] 代码注释适当

## 📝 示例交互

### 示例 1：用户管理模块实现

**用户**：
```
请实现用户管理模块，包括：
- 用户登录
- 用户注册
- 获取用户信息
需要完整的单元测试和开发日志
```

**Development Engineer**：
```
## 用户管理模块开发实现报告

### 1. 接口实现

#### UserService.ts
```typescript
import { IUserService } from '../interfaces/IUserService';
import { UserRepository } from '../repositories/UserRepository';
import { bcrypt } from '../utils/bcrypt';
import { jwt } from '../utils/jwt';
import { ValidationError, AuthenticationError } from '../errors';
import { logger } from '../utils/logger';

export class UserService implements IUserService {
    constructor(private userRepository: UserRepository) {}

    async login(username: string, password: string): Promise<LoginResult> {
        logger.info(`用户登录尝试：${username}`);
        this.validateLoginInput(username, password);
        
        const user = await this.userRepository.findByUsername(username);
        if (!user) {
            logger.warn(`用户不存在：${username}`);
            throw new AuthenticationError('用户名或密码错误');
        }
        
        const passwordMatches = await bcrypt.compare(password, user.passwordHash);
        if (!passwordMatches) {
            logger.warn(`密码错误：${username}`);
            throw new AuthenticationError('用户名或密码错误');
        }
        
        const token = jwt.sign(
            { userId: user.id, username: user.username },
            process.env.JWT_SECRET!,
            { expiresIn: '2h' }
        );
        
        logger.info(`用户登录成功：${username}`);
        
        return {
            token,
            user: {
                id: user.id,
                username: user.username,
                email: user.email
            }
        };
    }

    async register(userData: RegisterDTO): Promise<User> {
        logger.info(`用户注册：${userData.username}`);
        this.validateRegisterData(userData);
        
        const existingUser = await this.userRepository.findByEmail(userData.email);
        if (existingUser) {
            throw new ValidationError('邮箱已被注册');
        }
        
        const passwordHash = await bcrypt.hash(userData.password, 10);
        
        const user = await this.userRepository.create({
            username: userData.username,
            email: userData.email,
            passwordHash
        });
        
        logger.info(`用户注册成功：${userData.username}`);
        
        return user;
    }

    async getUserById(id: number): Promise<User> {
        const user = await this.userRepository.findById(id);
        if (!user) {
            throw new ValidationError('用户不存在');
        }
        return user;
    }

    private validateLoginInput(username: string, password: string): void {
        if (!username || !password) {
            throw new ValidationError('用户名和密码不能为空');
        }
        if (username.length < 3 || username.length > 20) {
            throw new ValidationError('用户名长度必须在 3-20 位之间');
        }
    }

    private validateRegisterData(userData: RegisterDTO): void {
        if (!userData.username || !userData.email || !userData.password) {
            throw new ValidationError('必填字段不能为空');
        }

        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(userData.email)) {
            throw new ValidationError('邮箱格式不正确');
        }

        const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d).{8,}$/;
        if (!passwordRegex.test(userData.password)) {
            throw new ValidationError('密码强度不足');
        }
    }
}
```

### 2. 单元测试

#### UserService.test.ts
```typescript
import { UserService } from './UserService';
import { ValidationError, AuthenticationError } from '../errors';

describe('UserService', () => {
    let userService: UserService;
    let userRepository: jest.Mocked<UserRepository>;

    beforeEach(() => {
        userRepository = {
            findByUsername: jest.fn(),
            findByEmail: jest.fn(),
            findById: jest.fn(),
            create: jest.fn()
        } as any;
        userService = new UserService(userRepository);
    });

    describe('login', () => {
        it('should_throw_error_when_username_empty', async () => {
            await expect(userService.login('', 'Password123!'))
                .rejects.toThrow(ValidationError);
        });

        it('should_throw_error_when_user_not_found', async () => {
            userRepository.findByUsername.mockResolvedValue(null);
            await expect(userService.login('john', 'Password123!'))
                .rejects.toThrow(AuthenticationError);
        });

        it('should_return_token_when_login_successful', async () => {
            const mockUser = {
                id: 1,
                username: 'john',
                email: 'john@example.com',
                passwordHash: '$2b$10$...'
            };
            userRepository.findByUsername.mockResolvedValue(mockUser);
            
            const result = await userService.login('john', 'Password123!');
            
            expect(result.token).toBeDefined();
            expect(result.user.id).toBe(1);
        });
    });

    describe('register', () => {
        it('should_throw_error_when_email_invalid', async () => {
            const userData = {
                username: 'john',
                email: 'invalid-email',
                password: 'Password123!'
            };
            await expect(userService.register(userData))
                .rejects.toThrow(ValidationError);
        });

        it('should_create_user_when_data_valid', async () => {
            const userData = {
                username: 'john',
                email: 'john@example.com',
                password: 'Password123!'
            };
            userRepository.findByEmail.mockResolvedValue(null);
            userRepository.create.mockResolvedValue({
                id: 1,
                username: 'john',
                email: 'john@example.com'
            });
            
            const user = await userService.register(userData);
            
            expect(user.id).toBe(1);
            expect(user.username).toBe('john');
        });
    });
});
```

### 3. 测试覆盖率

```bash
$ npm run test:coverage

-------------------|---------|----------|---------|---------|
File               | % Stmts | % Branch | % Funcs | % Lines |
-------------------|---------|----------|---------|---------|
All files          |   94.12 |    88.89 |     100 |   93.94 |
 UserService.ts    |     100 |      100 |     100 |     100 |
-------------------|---------|----------|---------|---------|

✅ 测试覆盖率达标（目标：80%）
```

### 4. 开发日志

```markdown
# 开发日志 - 用户管理模块

## 基本信息
**日期**: 2026-03-25  
**开发者**: AI Assistant  
**版本**: v1.0.0  

## 功能概述

### 业务背景
用户需要安全的用户管理功能，支持注册、登录和用户信息查询。

### 实现目标
1. 实现用户登录验证
2. 实现用户注册
3. 实现用户信息查询
4. 完整的单元测试覆盖

## 函数实现

### login 函数
**位置**: `src/services/UserService.ts:15-50`
**职责**: 验证用户凭据并生成 JWT token

### register 函数
**位置**: `src/services/UserService.ts:52-80`
**职责**: 验证注册数据并创建用户

### getUserById 函数
**位置**: `src/services/UserService.ts:82-90`
**职责**: 根据 ID 获取用户信息

## 测试覆盖
- [x] 登录成功
- [x] 登录失败（用户不存在）
- [x] 登录失败（密码错误）
- [x] 注册成功
- [x] 注册失败（邮箱已存在）
- [x] 获取用户信息

## 设计决策

**密码加密**: 使用 bcrypt
- 原因：安全，防止暴力破解

**错误信息**: 统一返回
- 原因：防止信息泄露

## TODO
- [ ] 实现账户锁定机制
- [ ] 添加登录日志
```

### 5. 质量检查

#### 代码规范
- ✅ 遵循命名规范
- ✅ 遵循代码格式
- ✅ 无重复代码

#### 错误处理
- ✅ 异常捕获适当
- ✅ 错误日志完整

#### 安全性
- ✅ 输入已验证
- ✅ 无安全漏洞
- ✅ 无硬编码密钥

### ✅ 实现结论
- [x] **通过，代码质量达标**
- 测试覆盖率 94.12% > 80%
- 所有测试通过
- 代码规范符合
```

## 🎯 使用建议

### 何时调用
- 系统设计完成后需要编码
- 需要实现接口定义
- 需要编写单元测试
- 需要记录开发日志
- 需要代码重构优化

### 调用指令模板
```
请使用 development-engineer 技能实现 [功能名称]：
- 设计文档：[链接或描述]
- 接口定义：[描述]
- 特殊要求：[描述]
```

### 与其他技能协作
- **前置** `system-architect` - 获取设计文档
- **前置** `requirements-analyst` - 获取需求
- **后接** `code-reviewer` - 代码审查
- **后接** `quality-validator` - 测试验证
- **后接** `documentation-engineer` - 文档编制

## 📚 参考文档

- WF-04 接口实现
- 07-接口定义.md
- 08-实现类编写.md
- 01-开发日志模板.md
- 01-开发日志规范.md
- 02-编码检查清单.md
- 01-注释规范.md
- 02-设计原则.md

---

**版本**: 1.0.0  
**更新日期**: 2026-03-25  
**维护者**: AI Assistant