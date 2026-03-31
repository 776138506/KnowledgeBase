# cc-godmode 技能调用

## 适用场景

- ✅ 新功能开发
- ✅ Bug 修复
- ✅ API 变更
- ✅ 重构任务

## 工作流程

**新功能**:
```
@researcher(可选) → @architect → @builder → @validator + @tester → @scribe
```

**API 变更**:
```
@architect → @api-guardian(必需) → @builder → @validator + @tester → @scribe
```

## 质量门禁

- **@validator** - TypeScript、单元测试、安全
- **@tester** - E2E 测试、截图、无障碍性
- **双门禁** - 两个都必须通过

## 使用原则

1. Version-First - 先确定版本
2. @architect is the Gate - 无架构不开始
3. @api-guardian MANDATORY - API 变更必需
4. Dual Quality Gates - 双门禁
5. No Skipping - 不跳过任何代理
