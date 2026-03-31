# TDD 测试驱动开发

## 🎯 适用场景

### 强制使用场景

- ✅ **创建新文件后** - 必须进行测试验证
- ✅ **编写新功能后** - 必须进行测试验证
- ✅ **修改现有代码后** - 必须回归测试
- ✅ **修复 Bug 后** - 必须验证修复

### 调用方式

```
"请使用 tdd-guide 技能对 [文件名/功能] 进行测试"
```

---

## 🔄 TDD 循环

```
1. RED     - 编写失败的测试
2. GREEN   - 编写最少代码通过测试
3. REFACTOR - 重构代码保持测试通过
```

---

## 📝 详细步骤

### 文件创建后的标准流程

1. **创建文件** - 编写代码
2. **调用 TDD 技能** - "使用 tdd-guide 测试 [文件名]"
3. **编写测试** - 为功能编写测试用例
4. **运行测试** - 验证测试失败（RED）
5. **编写代码** - 刚好能让测试通过（GREEN）
6. **运行测试** - 所有测试通过
7. **重构** - 清理代码，保持测试通过（REFACTOR）
8. **重复** - 继续下一个功能
9. **完成** - 覆盖率≥80%，所有测试通过

### 一般步骤

1. 添加测试 - 为小功能编写测试
2. 运行测试 - 新测试应该失败
3. 编写代码 - 刚好能让测试通过
4. 运行测试 - 所有测试通过
5. 重构 - 清理代码
6. 重复 - 继续下一个测试

## AAA 模式

```typescript
// Arrange - 准备数据
const input = 5;
const expected = 10;

// Act - 执行代码
const result = double(input);

// Assert - 验证结果
expect(result).toBe(expected);
```

## 测试命名

`should_[预期行为]_when_[条件]`

示例：
- `should_return_empty_array_when_list_is_empty`
- `should_throw_exception_when_input_is_null`

## 原则

- **Write tests first** - 先写测试
- **Write minimal code** - 最少代码
- **Refactor continuously** - 持续重构
- **Small steps** - 小步前进
- **Green bar addiction** - 保持测试通过
- **Mandatory after file creation** - 文件创建后必须调用

---

## ✅ 完成标准

使用 TDD 技能后的完成标准：

1. [ ] 所有测试通过
2. [ ] 测试覆盖率≥80%
3. [ ] 核心逻辑覆盖率 100%
4. [ ] 边界条件已测试
5. [ ] 异常处理已测试
6. [ ] 代码已重构优化
7. [ ] 可以提交代码

---

**版本**: 1.1.0  
**更新日期**: 2026-03-19  
**维护者**: AI Assistant
