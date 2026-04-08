---
name: prototype-design
description: 原型设计技能 — 支持线框图、高保真原型、可交互原型和 UI 设计规范的设计与验证。集成到 Phase 1 后用于需求可视化，支持外部工具（Figma/墨刀）和 HTML/CSS 实现。
---

# 原型设计技能 v1.0

## 🎯 核心目标

在 Phase 1（需求调研）完成后，通过可视化原型帮助：
- ✅ **需求具象化**：将抽象的用例图转化为可视的界面原型
- ✅ **早期验证**：在编码前验证用户流程和交互设计
- ✅ **降低沟通成本**：用可视化原型替代文字描述，减少理解偏差
- ✅ **快速迭代**：低成本修改原型，避免编码后返工

## 🏗️ 目录结构

```
skills/prototype-design/
├── SKILL.md                              # 本文件（原型设计技能定义）
├── references/
│   ├── wireframe-guidelines.md          # 线框图设计规范
│   ├── hifi-prototype-guidelines.md     # 高保真原型设计规范
│   ├── interactive-prototype-guidelines.md # 可交互原型设计规范
│   └── ui-design-system-guidelines.md   # UI 设计规范指南
├── templates/
│   ├── wireframe-template.html          # 线框图 HTML 模板
│   ├── prototype-template.html          # 可交互原型模板
│   └── design-system-template.md        # UI 设计规范模板
└── examples/
    └── user-register-prototype/         # 用户注册原型示例
```

## 📋 何时使用

### 在 Phase 1.3（原型设计阶段）使用

```
Phase 1: 需求调研 → 用例图 + 业务活动图 ✓
  ↓ 【门禁】
Phase 1.3: 原型设计 ← 本技能在此执行
  ├─ 🧠 编写前：头脑风暴（原型目标/保真度/工具选择）
  ├─ 🎨 设计：线框图 → 高保真 → 可交互原型
  ├─ 🔍 编写后：原型审核（完整性/一致性/可访问性）
  └─ 🔗 输出：外部工具链接 + HTML/CSS 原型代码
  ↓ 【门禁】
Phase 1.5: 技术栈验证
```

### 适用场景

- ✅ 面向用户的功能（需要 UI 界面）
- ✅ 复杂交互流程（需要可视化验证）
- ✅ 创新功能（用户不熟悉，需要原型演示）
- ✅ 多端适配（需要验证响应式布局）
- ❌ 纯后端 API（无 UI 界面）
- ❌ 内部工具（已有成熟 UI 框架）

## 🎨 原型设计流程

### Step 1: 原型规划（头脑风暴）

> 加载 `skills/brainstorming/SKILL.md` 执行原型设计探索

**核心问题**：

1. **原型目标**：
   - 验证用户流程？
   - 展示视觉效果？
   - 用户测试？
   - 利益相关者演示？

2. **保真度选择**：
   - **低保真（线框图）**：快速探索布局，适合早期
   - **中保真**：加入基础样式，适合流程验证
   - **高保真**：完整视觉效果，适合最终确认

3. **工具选择**：
   - **Figma/墨刀**：适合协作、评论、用户测试
   - **HTML/CSS**：适合可交互原型、代码复用
   - **混合模式**：Figma 设计 + HTML 实现关键流程

4. **覆盖范围**：
   - 核心流程（必须）
   - 异常流程（建议）
   - 边界场景（可选）

**输出**：原型设计计划书

```markdown
# 原型设计计划

## 目标
- 验证用户注册流程的交互设计
- 向利益相关者展示核心功能

## 保真度
- 线框图：全部 5 个页面
- 高保真：核心 3 个页面
- 可交互：注册主流程

## 工具
- Figma: 完整设计稿（链接：[Figma 项目](https://figma.com/file/xxx)）
- HTML/CSS: 注册页面可交互原型

## 覆盖范围
- ✅ 主流程：首页 → 注册表单 → 邮箱验证 → 完成
- ✅ 异常流程：表单验证失败、邮箱已存在
- ⚠️ 边界场景：密码强度校验（简化版）

## 时间估算
- 线框图：2 小时
- 高保真：4 小时
- HTML 实现：3 小时
- 审核修改：2 小时
```

---

## Step 2: 线框图设计（低保真）

> 快速探索页面布局和元素排布

### 2.1 页面清单

基于 Phase 1 的用例图，提取需要原型的页面：

```markdown
## 页面清单

| 页面 ID | 页面名称 | 对应用例 | 优先级 |
|--------|---------|---------|--------|
| P-001 | 首页 | UC-001 | P0 |
| P-002 | 注册表单页 | UC-002 | P0 |
| P-003 | 邮箱验证页 | UC-003 | P0 |
| P-004 | 完成页 | UC-004 | P1 |
| P-005 | 错误页 | UC-005 | P1 |
```

### 2.2 线框图模板（HTML/CSS 实现）

使用提供的模板快速生成线框图：

```html
<!-- templates/wireframe-template.html -->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>线框图 - {页面名称}</title>
  <style>
    /* 线框图基础样式 - 灰度、无细节 */
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f5f5f5; }
    .wireframe { 
      max-width: 1200px; 
      margin: 20px auto; 
      background: white; 
      padding: 20px;
      border: 1px solid #ccc;
    }
    .header { height: 60px; background: #ddd; margin-bottom: 20px; }
    .content { min-height: 400px; background: #eee; }
    .footer { height: 40px; background: #ddd; margin-top: 20px; }
    .placeholder { 
      border: 2px dashed #999; 
      padding: 20px; 
      text-align: center;
      color: #666;
      margin: 10px;
    }
    .button { 
      display: inline-block; 
      padding: 10px 20px; 
      background: #ccc; 
      border: none; 
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="wireframe">
    <div class="header">
      <div class="placeholder">Logo + 导航</div>
    </div>
    <div class="content">
      <div class="placeholder">页面内容区域</div>
    </div>
    <div class="footer">
      <div class="placeholder">页脚信息</div>
    </div>
  </div>
</body>
</html>
```

### 2.3 输出格式

**每个页面的线框图包含**：

1. **HTML 文件**：`wireframes/{page-id}-wireframe.html`
2. **说明文档**：`wireframes/{page-id}-notes.md`

```markdown
# P-002 注册表单页 - 线框图说明

## 布局说明
- 顶部：Logo + 导航栏（高度 60px）
- 中部：表单区域（居中对齐，最大宽度 400px）
- 底部：页脚（版权信息）

## 表单元素
1. 邮箱输入框（必填）
2. 密码输入框（必填，显示强度指示器）
3. 确认密码框（必填）
4. 注册按钮

## 交互说明
- 输入框获得焦点时显示提示
- 实时密码强度校验
- 提交前表单验证

## 响应式
- 移动端（<768px）：表单宽度 100%
- 桌面端：表单宽度 400px 居中
```

---

## Step 3: 高保真原型设计

> 在线框图基础上加入视觉效果和品牌元素

### 3.1 UI 设计规范

在开始高保真设计前，先定义设计系统：

```markdown
# UI 设计规范（精简版）

## 颜色系统
- 主色：#007AFF（品牌蓝）
- 成功色：#34C759
- 警告色：#FF9500
- 错误色：#FF3B30
- 中性色：#1D1D1F, #6E6E73, #8E8E93, #C7C7CC, #E5E5EA, #F2F2F7

## 字体系统
- 标题：24px / 20px / 17px（粗体）
- 正文：17px / 15px / 13px（常规）
- 辅助文字：13px / 11px

## 间距系统
- 基础单位：4px
- 常用间距：8px, 12px, 16px, 20px, 24px, 32px

## 圆角规范
- 小按钮：6px
- 卡片：12px
- 大容器：16px

## 阴影规范
- 轻阴影：0 2px 8px rgba(0,0,0,0.08)
- 中阴影：0 4px 16px rgba(0,0,0,0.12)
- 重阴影：0 8px 32px rgba(0,0,0,0.16)
```

### 3.2 Figma/墨刀设计

**外部工具设计流程**：

1. 创建 Figma/墨刀项目
2. 导入线框图作为参考
3. 应用 UI 设计规范
4. 设计每个页面的高保真版本
5. 添加页面间跳转链接（可交互）
6. 分享原型链接

**输出**：

```markdown
# 高保真原型链接

## Figma 项目
- 完整设计稿：https://figma.com/file/{file-id}
- 可交互原型：https://figma.com/proto/{file-id}

## 页面列表
- P-001 首页：Frame 1-2
- P-002 注册表单页：Frame 3-5
- P-003 邮箱验证页：Frame 6
- P-004 完成页：Frame 7
```

---

## Step 4: 可交互原型实现（HTML/CSS）

> 对核心流程实现可点击、可交互的 HTML 原型

### 4.1 项目结构

```
prototype-html/
├── index.html                    # 入口（原型导航页）
├── css/
│   ├── design-system.css        # 设计系统（颜色/字体/间距）
│   ├── components.css           # 组件库（按钮/输入框/卡片）
│   └── pages.css                # 页面特定样式
├── js/
│   ├── interactions.js          # 交互逻辑
│   └── validation.js            # 表单验证
├── pages/
│   ├── home.html                # P-001 首页
│   ├── register.html            # P-002 注册表单页
│   ├── verify.html              # P-003 邮箱验证页
│   └── complete.html            # P-004 完成页
└── assets/
    ├── images/                  # 图片资源
    └── icons/                   # 图标资源
```

### 4.2 设计系统实现

```css
/* css/design-system.css */

:root {
  /* 颜色系统 */
  --color-primary: #007AFF;
  --color-success: #34C759;
  --color-warning: #FF9500;
  --color-error: #FF3B30;
  
  /* 中性色 */
  --color-text-primary: #1D1D1F;
  --color-text-secondary: #6E6E73;
  --color-text-tertiary: #8E8E93;
  --color-border: #E5E5EA;
  --color-background: #F2F2F7;
  
  /* 间距系统 */
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  
  /* 圆角 */
  --radius-sm: 6px;
  --radius-md: 12px;
  --radius-lg: 16px;
  
  /* 阴影 */
  --shadow-sm: 0 2px 8px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 16px rgba(0,0,0,0.12);
  --shadow-lg: 0 8px 32px rgba(0,0,0,0.16);
  
  /* 字体 */
  --font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-size-xs: 11px;
  --font-size-sm: 13px;
  --font-size-md: 15px;
  --font-size-lg: 17px;
  --font-size-xl: 20px;
  --font-size-2xl: 24px;
}
```

### 4.3 组件库实现

```css
/* css/components.css */

/* 按钮组件 */
.btn {
  display: inline-block;
  padding: var(--spacing-sm) var(--spacing-lg);
  font-size: var(--font-size-lg);
  font-weight: 600;
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-primary {
  background: var(--color-primary);
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
  box-shadow: var(--shadow-md);
}

/* 输入框组件 */
.input {
  width: 100%;
  padding: var(--spacing-sm);
  font-size: var(--font-size-md);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-sm);
  transition: border-color 0.2s ease;
}

.input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(0,122,255,0.1);
}

/* 卡片组件 */
.card {
  background: white;
  border-radius: var(--radius-md);
  padding: var(--spacing-lg);
  box-shadow: var(--shadow-sm);
}
```

### 4.4 页面实现示例

```html
<!-- pages/register.html -->
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>用户注册 - 原型</title>
  <link rel="stylesheet" href="../css/design-system.css">
  <link rel="stylesheet" href="../css/components.css">
  <link rel="stylesheet" href="../css/pages.css">
</head>
<body>
  <div class="page register-page">
    <div class="container">
      <header class="header">
        <h1>创建账户</h1>
        <p class="subtitle">已有账户？<a href="login.html">登录</a></p>
      </header>
      
      <main class="card">
        <form id="registerForm" novalidate>
          <div class="form-group">
            <label for="email">邮箱地址</label>
            <input 
              type="email" 
              id="email" 
              class="input" 
              placeholder="your@email.com"
              required
            >
            <span class="error-message" id="emailError"></span>
          </div>
          
          <div class="form-group">
            <label for="password">密码</label>
            <input 
              type="password" 
              id="password" 
              class="input" 
              placeholder="至少 8 位"
              required
              minlength="8"
            >
            <div class="password-strength" id="passwordStrength"></div>
            <span class="error-message" id="passwordError"></span>
          </div>
          
          <div class="form-group">
            <label for="confirmPassword">确认密码</label>
            <input 
              type="password" 
              id="confirmPassword" 
              class="input" 
              placeholder="再次输入密码"
              required
            >
            <span class="error-message" id="confirmError"></span>
          </div>
          
          <button type="submit" class="btn btn-primary btn-block">
            立即注册
          </button>
        </form>
      </main>
      
      <footer class="footer">
        <p>点击"立即注册"即表示同意我们的<a href="#">服务条款</a></p>
      </footer>
    </div>
  </div>
  
  <script src="../js/validation.js"></script>
  <script src="../js/interactions.js"></script>
</body>
</html>
```

### 4.5 交互逻辑实现

```javascript
// js/interactions.js

// 表单提交处理
document.getElementById('registerForm').addEventListener('submit', async (e) => {
  e.preventDefault();
  
  const formData = {
    email: document.getElementById('email').value,
    password: document.getElementById('password').value,
    confirmPassword: document.getElementById('confirmPassword').value
  };
  
  // 验证表单
  const errors = validateForm(formData);
  if (Object.keys(errors).length > 0) {
    displayErrors(errors);
    return;
  }
  
  // 模拟 API 调用
  try {
    showLoading(true);
    await mockApiCall(formData);
    showLoading(false);
    // 跳转到验证页
    window.location.href = 'verify.html';
  } catch (error) {
    showLoading(false);
    displayErrors({ submit: error.message });
  }
});

// 密码强度实时校验
document.getElementById('password').addEventListener('input', (e) => {
  const password = e.target.value;
  const strength = calculatePasswordStrength(password);
  updatePasswordStrengthIndicator(strength);
});

// 辅助函数
function mockApiCall(data) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      // 模拟邮箱已存在错误
      if (data.email === 'existing@example.com') {
        reject(new Error('该邮箱已被注册'));
      } else {
        resolve({ success: true });
      }
    }, 1000);
  });
}

function showLoading(show) {
  const btn = document.querySelector('button[type="submit"]');
  if (show) {
    btn.disabled = true;
    btn.textContent = '注册中...';
  } else {
    btn.disabled = false;
    btn.textContent = '立即注册';
  }
}
```

---

## 🔍 Step 5: 原型审核

> 加载 `references/enhanced-review-protocol.md` 执行原型审核

### 审核维度 — 原型设计专用

| 审核项 | 检查点 | 极端情况压力测试 |
|-------|--------|----------------|
| **场景覆盖率** | 100% Phase 1 用例有对应页面？ | 未覆盖的异常流程 |
| **流程完整性** | 主流程 + 异常流程都完整？ | 所有分支路径都有页面 |
| **交互一致性** | 相同操作在不同页面行为一致？ | 按钮/表单/导航的一致性 |
| **可访问性** | 是否考虑无障碍访问？ | 键盘导航/屏幕阅读器 |
| **响应式布局** | 移动端/桌面端都适配？ | 极端屏幕尺寸（320px-2560px） |
| **加载状态** | 异步操作是否有加载反馈？ | 网络超时/加载失败 |
| **错误处理** | 表单验证/错误提示是否清晰？ | 所有可能的错误场景 |
| **边界值** | 输入框长度/文件上传限制？ | 超长文本/大文件上传 |

### 审核输出模板

```markdown
# 原型设计审核报告

## 基本信息
- 项目名称：{project-name}
- 原型版本：v{version}
- 审核日期：{date}
- 审核人：{reviewer}

## 审核结果

### 场景覆盖率
✅ 通过：10/10 用例有对应页面
⚠️ 建议：UC-008（找回密码）未覆盖，建议补充

### 流程完整性
✅ 主流程完整
⚠️ 异常流程缺失：
  - 邮箱验证失败后的重试流程
  - 网络错误的兜底页面

### 交互一致性
✅ 按钮风格统一
✅ 表单验证逻辑一致
⚠️ 导航栏在不同页面位置不一致

### 可访问性
⚠️ 部分按钮缺少 aria-label
⚠️ 颜色对比度不足（错误提示文字）

### 响应式布局
✅ 移动端（375px）适配良好
✅ 桌面端（1920px）适配良好
⚠️ 平板端（768px）布局错位

### 加载状态
✅ 表单提交有加载反馈
⚠️ 图片加载无占位符

### 错误处理
✅ 表单验证提示清晰
⚠️ 网络错误提示不够友好

### 边界值
✅ 输入框有长度限制
⚠️ 未处理 emoji 等特殊字符

## 审核结论

**总体评价**: CONDITIONAL_PASS

**阻塞项** (必须修复后才可进入下一阶段):
1. 补充 UC-008 找回密码流程原型
2. 修复平板端布局错位问题

**建议项** (建议修复但不阻塞):
1. 补充异常流程原型
2. 优化可访问性
3. 添加图片占位符

## 下一步

1. 修复阻塞项（预计 2 小时）
2. 重新提交审核
3. 审核通过后进入 Phase 1.5（技术栈验证）
```

---

## 📊 原型设计质量检查清单

### 线框图检查

- [ ] 所有 Phase 1 用例都有对应页面
- [ ] 每个页面的布局清晰可读
- [ ] 表单元素标注完整（类型/验证规则）
- [ ] 交互说明文档完整
- [ ] 响应式规则已定义

### 高保真原型检查

- [ ] UI 设计规范已定义并应用
- [ ] 颜色系统完整（主色/辅助色/中性色）
- [ ] 字体系统完整（字号/字重/行高）
- [ ] 间距系统一致（4px 基础单位）
- [ ] Figma/墨刀原型可访问
- [ ] 可交互链接有效

### HTML/CSS原型检查

- [ ] 项目结构清晰（css/js/pages分离）
- [ ] 设计系统已实现（CSS 变量）
- [ ] 组件库已实现（按钮/输入框/卡片）
- [ ] 核心流程可交互
- [ ] 表单验证逻辑完整
- [ ] 响应式布局测试通过
- [ ] 跨浏览器测试通过（Chrome/Firefox/Safari）

### 审核准备检查

- [ ] 原型审核清单已自检
- [ ] 所有阻塞项已修复
- [ ] 审核文档已准备
- [ ] 利益相关者已邀请（如需要）

---

## 🔗 与主流程的集成

### 在 Phase 1.3 执行原型设计

```markdown
### Phase 1.3: 原型设计 → 需求可视化

**产出**：线框图、高保真原型、可交互原型、UI 设计规范

**AI 操作**：

1. 加载 `skills/prototype-design/SKILL.md`
2. 执行 Step 1-5（规划→线框→高保真→交互→审核）
3. 输出原型链接和 HTML 代码

**质量检查**：

- [ ] 线框图已完成
- [ ] 高保真原型已完成
- [ ] HTML/CSS原型（核心流程）已完成
- [ ] 原型审核已通过
- [ ] 阻塞项已全部修复

**门禁检查**：

```
Phase 1.3 完成！
📊 产出物：
- 线框图：{n} 个页面 ✓
- 高保真原型：Figma/墨刀链接 ✓
- 可交互原型：HTML/CSS ✓
- UI 设计规范：✓
- 原型审核：✓ 通过
请确认：
1. 原型是否准确反映了 Phase 1 的需求？
2. 交互流程是否顺畅？
3. 审核意见是否已处理？
4. 可以进入阶段 1.5 吗？
```

**用户确认前不要继续！**
```

---

## 📚 模板与资源

### 模板文件

- `templates/wireframe-template.html` — 线框图 HTML 模板
- `templates/prototype-template.html` — 可交互原型模板
- `templates/design-system-template.md` — UI 设计规范模板

### 示例项目

- `examples/user-register-prototype/` — 用户注册完整原型示例

### 外部工具推荐

- **Figma**: https://figma.com — 协作式设计工具
- **墨刀**: https://modao.cc — 国产原型设计工具
- **CodePen**: https://codepen.io — HTML/CSS 原型分享
- **Lighthouse**: Chrome 内置 — 可访问性测试

---

## ✅ 最佳实践

### 1. 原型保真度选择指南

| 项目阶段 | 推荐保真度 | 目标 | 工具 |
|---------|-----------|------|------|
| 需求探索 | 低保真（线框图） | 快速试错 | 纸笔/Balsamiq |
| 流程验证 | 中保真 | 验证交互 | Figma/墨刀 |
| 最终确认 | 高保真 + 可交互 | 用户测试/演示 | Figma + HTML |
| 开发参考 | 高保真 + 代码 | 交付开发 | Figma + HTML/CSS |

### 2. 原型设计原则

- **KISS 原则**：保持简单，避免过度设计
- **一致性原则**：相同元素在不同页面保持一致
- **渐进式披露**：只展示当前步骤需要的信息
- **容错性原则**：允许用户犯错并提供恢复路径
- **可访问性原则**：考虑残障用户的需求

### 3. 常见陷阱

❌ **过度追求完美**：原型不是最终产品，快速迭代优先
❌ **忽略异常流程**：只设计主流程，异常流程缺失
❌ **缺少交互说明**：静态图无法表达动态交互
❌ **脱离技术可行性**：设计无法实现的效果
❌ **忽略响应式**：只设计桌面端，不考虑移动端

---

**版本**: 1.0.0
**创建日期**: 2026-04-07
**最后更新**: 2026-04-07 (v1.0.0: 初始版本 — 线框图/高保真/可交互原型/UI 设计规范)
**适用阶段**: Phase 1.3（原型设计）
**输出格式**: Figma/墨刀链接 + HTML/CSS 代码
**状态**: 🟢 稳定
