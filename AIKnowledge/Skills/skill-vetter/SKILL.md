---
name: "skill-vetter"
description: "Validates and reviews skills for quality, security, and best practices. Invoke when creating, modifying, or reviewing skills to ensure they meet standards."
---

# Skill Vetter

此技能用于验证和审查 SkillHub 技能的质量、安全性和最佳实践。

## 功能

- 验证技能结构是否符合规范
- 检查 SKILL.md 文件格式
- 审查技能描述是否清晰
- 确保技能遵循安全最佳实践
- 提供改进建议

## 检查项目

1. **结构验证**
   - 检查 `.trae/skills/<skill-name>/SKILL.md` 目录结构
   - 验证 frontmatter 格式

2. **内容审查**
   - 名称是否唯一且有意义
   - 描述是否清晰说明功能和触发时机
   - 使用说明是否完整

3. **安全性检查**
   - 确保不包含敏感信息
   - 验证权限要求合理

## 使用方法

当用户创建、修改或审查技能时，使用此技能进行质量检查。
