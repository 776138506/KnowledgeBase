# 技术栈最新性验证指南

> 在架构设计前验证技术栈是否为当前主流、活跃、未被废弃
> 
**版本**: 1.0.0  
**用途**: Phase 1.5 技术栈验证阶段的详细操作指南

---

## 🎯 为什么需要技术栈验证？

### AI 训练数据的局限性

AI 模型的训练数据有**截止日期**，可能不知道：

- 📅 **最近发布的新版本**（训练数据之后发布的）
- ⚠️ **最近宣布废弃的技术**（如 Python 3.7 已 EOL）
- 🔴 **最近发现的安全漏洞**（CVE）
- 📉 **社区活跃度变化**（项目是否还在维护）

### 过时技术的风险

| 风险类型 | 具体影响 | 示例 |
|---------|---------|------|
| **安全风险** | 无法获得安全补丁 | Python 3.7 已停止安全更新 |
| **兼容性风险** | 新系统/库不兼容 | 旧版 OpenSSL 被新系统移除 |
| **人才风险** | 找不到维护者 | 使用冷门框架招人困难 |
| **生态风险** | 依赖库无法安装 | PyPI 移除 yanked 版本 |
| **性能风险** | 错过重大性能改进 | Node.js 18 vs 16 性能差距巨大 |

---

## 🔍 验证流程总览

```
Step 1: 提取待验证技术清单
    ↓
Step 2: 对每个技术执行 6 维度检查
    ↓
Step 3: 生成综合评分和推荐决策
    ↓
Step 4: 汇总报告 + 用户确认
    ↓
Step 5: 更新 project-constraint.yaml
```

---

## 📋 6 维度验证框架

### 维度 1: 版本新鲜度 (Version Freshness)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| 当前最新稳定版 | 官网 / GitHub Releases | 与指定版本差距 < 2 个大版本 |
| 最后发布时间 | GitHub / npm / PyPI | < 6 个月前 |
| 发布频率 | Release History | 至少每季度一次（LTS 除外）|
| LTS 支持状态 | 官方文档 | 如使用 LTS，确认仍在支持期内 |

**评分标准**:
- 5分: 最新版或相差 1 个小版本，发布 < 1 个月
- 4分: 相差 1-2 个小版本，发布 < 3 个月
- 3分: 相差 1 个大版本，发布 < 6 个月
- 2分: 相差 > 1 个大版本，或发布 > 6 个月
- 1分: 已停止发布或超过 2 年未更新

---

### 维度 2: 维护活跃度 (Maintenance Activity)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| Last Commit 时间 | GitHub API | < 30 天前（活跃项目）|
| Commit 频率 | GitHub Stats | 平均每周 ≥ 1 次 commit |
| Issue 响应时间 | GitHub Issues | P0 issue < 7 天响应 |
| PR 处理速度 | GitHub Pull Requests | 平均 < 14 天 merge |
| Contributor 数量 | GitHub Contributors | ≥ 5 人（非单点依赖）|

**维护状态分类**:

| 状态 | 定义 | 行动建议 |
|------|------|---------|
| ✅ **积极维护** | 频繁 commit，快速响应 | 安全使用 |
| ⚠️ **维护放缓** | commit 减少，响应变慢 | 关注趋势，准备备选 |
| ❌ **仅安全维护** | 只修 bug 不加功能 | 规划迁移时间线 |
| ❌ **已停止维护** | 无新 commit | 必须替换 |
| 💀 **已废弃** | 官方宣布 EOL | 立即替换 |

**评分标准**:
- 5分: 核心团队活跃，社区贡献多，响应迅速
- 4分: 维持正常节奏，偶有延迟
- 3分: 维护明显放缓，但仍有响应
- 2分: 接近停止维护状态
- 1分: 已停止维护或已废弃

---

### 维度 3: 社区健康度 (Community Health)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| GitHub Stars 趋势 | GitHub API | 持续增长或稳定（非急剧下降）|
| 月下载量趋势 | PyPI / npm / Docker Hub | 持续增长或稳定 |
| Stack Overflow 问题数 | StackOverflow API | 有足够的问题量（说明有人用）|
| 问题回答率 | StackOverflow | ≥ 70% 的问题有答案 |
| Discord/Slack 成员 | 社区链接 | ≥ 1000 人（主流框架）|

**社区健康信号**:

🟢 **健康信号**:
- Stars 持续增长（月增 > 1%）
- 下载量稳步上升
- Stack Overflow 问题活跃且有人回答
- 有年度会议或大型活动

🟡 **警告信号**:
- Stars 增长停滞或下降
- 下载量持平或下降
- 社区讨论减少
- 核心贡献者流失

🔴 **危险信号**:
- Stars 急剧下降
- 下载量持续下跌
- 官方论坛/群组无人管理
- 主要贡献者宣布离开

**评分标准**:
- 5分: 大型活跃社区，生态系统丰富
- 4分: 中等规模社区，核心用户稳定
- 3分: 小型但稳定的社区
- 2分: 社区萎缩中
- 1分: 几乎无社区活动

---

### 维度 4: 安全性 (Security)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| 近 6 个月 CVE 数量 | NVD / CVE Details | 无 Critical/High 级别未修复漏洞 |
| 最高严重等级 | CVE Details | 无 Critical 或仅有 Low |
| 安全公告频率 | 官方 Security Advisories | 有定期的安全公告机制 |
| 依赖安全性 | Snyk / Dependabot | 直接依赖无已知漏洞 |
| 加密算法支持 | 官方文档 | 支持现代加密标准 |

**常见安全问题**:

❌ **必须避免的情况**:
- 存在未修复的 Critical/High CVE
- 使用已知弱加密算法（MD5, SHA1 用于密码等）
- 依赖库存在供应链攻击风险
- 项目不再接收安全报告

⚠️ **需要注意的情况**:
- 存在 Medium 级别 CVE 但有 workaround
- 默认配置不够安全
- 需要额外配置才能达到安全基线

**评分标准**:
- 5分: 无已知 CVE，安全实践优秀
- 4分: 仅有 Low 级别 CVE 或已全部修复
- 3分: 有 Medium CVE 但有官方修复计划
- 2分: 存在 High CVE 未完全修复
- 1分: 存在 Critical CVE 或完全不关心安全

---

### 维度 5: 行业认可度 (Industry Adoption)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| 大公司采用案例 | 官方 Customers 页面 / 博客 | 有知名企业生产使用 |
| 同类项目使用率 | GitHub Topic 搜索 | 在同类项目中占主导地位 |
| 官方背书 | 语言/平台官网推荐 | 被官方推荐或收录 |
| 学习资源质量 | YouTube / Udemy / 官方教程 | 有高质量学习材料 |
| 招聘市场需求 | LinkedIn / Indeed / 招聘网站 | 有大量相关职位 |

**行业采用信号**:

✅ **强烈推荐信号**:
- 被 Google/Meta/Netflix 等科技巨头使用
- 是某领域的 de facto standard
- 有官方语言/平台支持
- 招聘市场需求旺盛

⚠️ **谨慎考虑信号**:
- 仅在小圈子流行
- 主要由单一公司推动
- 招聘市场岗位稀少
- 缺乏权威背书

**评分标准**:
- 5分: 行业标准，广泛采用，招聘需求高
- 4分: 广泛认知，有一定市场份额
- 3分: 小众但在特定领域被接受
- 2分: 仅在极少数项目中使用
- 1分: 几乎无行业采用案例

---

### 维度 6: 兼容性与迁移 (Compatibility & Migration)

**检查项**:

| 检查项 | 数据来源 | 健康标准 |
|-------|---------|---------|
| 向后兼容策略 | 官方 Changelog / Blog | 有清晰的兼容性承诺 |
| 迁移指南完整度 | 官方 Migration Guide | 提供详细的升级路径 |
| Breaking Change 频率 | Release Notes | Major 版本间 breaking change 可控 |
| 弃用 API 警告 | Deprecation Warnings | 提前通知弃用，给过渡期 |
| 文档完整性 | Official Docs / Readme | 文档覆盖主要使用场景 |

**迁移风险评估**:

| 难度 | 特征 | 建议 |
|-----|------|------|
| 🟢 低 | API 兼容，配置改动即可 | 可以随时升级 |
| 🟡 中 | 需要修改部分代码，有 migration 工具 | 规划升级窗口期 |
| 🔴 高 | 架构级变更，需要重写部分模块 | 评估投入产出比 |

**评分标准**:
- 5分: 完全向后兼容，升级无痛
- 4分: 有少量 breaking change 但有 migration 工具
- 3分: 升级需要一定工作量但有清晰指南
- 2分: 升级复杂，breaking change 较多
- 1分: 几乎无法从当前版本平滑升级

---

## 📊 综合评分与决策矩阵

### 评分计算

```
综合评分 = (维度1 + 维度2 + 维度3 + 维度4 + 维度5 + 维度6) / 6

每个维度 1-5 分，总分 1-5 分
```

### 决策矩阵

| 综合评分 | 决策 | 行动 |
|---------|------|------|
| **4.5 - 5.0** | ✅ 强烈推荐 | 直接使用，无需犹豫 |
| **3.5 - 4.4** | ✅ 推荐 | 可以使用，注意监控 |
| **2.5 - 3.4** | ⚠️ 有条件推荐 | 需要评估风险后决定 |
| **1.5 - 2.4** | ❌ 不推荐 | 寻找替代方案 |
| **1.0 - 1.4** | 🔴 必须替换 | 立即替换，禁止使用 |

### 特殊情况处理

**即使评分高，也要警惕**:
- 单人维护的项目（⚠️ Bus Factor = 1）
- 许可证变更风险（如 MongoDB 从 AGPL 变更）
- 商业化转型（开源 → 闭源/收费）
- 公司被收购后方向不明朗

**即使评分低，也可以用**:
- 内部工具/脚本（短期使用）
- 遗留系统维护（已有代码）
- 特殊场景无替代品（需制定退出策略）

---

## 🔧 各类技术验证重点

### 编程语言

**必查项**:
- [ ] 是否仍在官方支持期内？（Python 3.8+ 支持, 3.7 已 EOL）
- [ ] 最新版本的发布时间和新特性
- [ ] 性能基准测试对比（如 Python 3.11 vs 3.12）
- [ ] 类型系统/语法是否有重大更新

**常用语言支持状态速查**:

| 语言 | 最低推荐版本 | 当前稳定版 | EOL 版本 | 备注 |
|------|------------|-----------|---------|------|
| Python | 3.11+ | 3.12.x | ≤ 3.9 | 3.10 安全支持至 2026-10 |
| Node.js | 20 LTS | 22.x | ≤ 18.x | 每 6 个月新 LTS |
| Go | 1.22+ | 1.23.x | ≤ 1.20 | 每 6 个月新版本 |
| Java | 17 LTS / 21 LTS | 23.x | ≤ 17 (非LTS) | LTS 周期延长至多年 |
| Rust | 1.75+ | stable | - | 每 6 周新版本 |
| TypeScript | 5.x | 5.x | ≤ 4.x | 与 JS 生态同步 |

---

### Web 框架

**必查项**:
- [ ] 性能基准对比（TechEmpower Framework Benchmarks）
- [ ] 异步支持情况（async/await）
- [ ] 中间件/插件生态丰富度
- [ ] OpenAPI/Swagger 自动生成支持
- [ ] 认证授权方案成熟度

**2026 主流 Web 框架对比**:

| 框架 | 语言 | Stars | 特点 | 适用场景 |
|------|------|-------|------|---------|
| FastAPI | Python | 80k+ | 自动文档、高性能异步 | API 服务、微服务 |
| Django | Python | 80k+ | 全功能 ORM、Admin | 全栈应用、CMS |
| Express.js | Node.js | 65k+ | 极简灵活 | 快速原型、小型服务 |
| Next.js | React | 125k+ | SSR/SSG、App Router | 现代 Web 应用 |
| Spring Boot | Java | 75k+ | 企业级、生态完善 | 企业应用、微服务 |
| Gin | Go | 78k+ | 高性能、简洁 | Go 微服务、高性能 API |

---

### 数据库

**必查项**:
- [ ] 版本支持状态（MySQL 5.7 EOL, 8.0+ 推荐）
- [ ] 云原生支持（Aurora、Cloud SQL、RDS）
- [ ] 与 ORM 的兼容性
- [ ] 备份恢复方案成熟度
- [ ] 分片/集群能力

**数据库选择决策树**:

```
需要关系型？
    ↓ 是
数据量大（TB+）？
    ↓ 是 → PostgreSQL（强大扩展性）或 MySQL（云生态好）
    ↓ 否 → SQLite（轻量）/ PostgreSQL（功能全）
    
    ↓ 否（NoSQL）
强一致性需求？
    ↓ 是 → MongoDB Document / TiDB HTAP
    ↓ 否
键值缓存？→ Redis
全文搜索？→ Elasticsearch
时序数据？→ InfluxDB / TimescaleDB
图数据？→ Neo4j
```

---

### ORM / ODM

**必查项**:
- [ ] 是否支持异步（async session）
- [ ] 迁移工具集成（Alembic 等）
- [ ] 查询性能（N+1 问题检测）
- [ ] 多数据库支持
- [ ] 类型安全（Pydantic 集成等）

**Python ORM 选择**:

| ORM | 异步支持 | 迁移工具 | 类型安全 | 适用场景 |
|-----|---------|---------|---------|---------|
| SQLAlchemy 2.0 | ✅ 原生 | ✅ Alembic | ✅ TypedSQL | 企业级首选 |
| Tortoise ORM | ✅ 原生 | ✅ Aerich | ✅ 类型提示 | asyncio 项目 |
| Django ORM | ⚠️ 有限 | ✅ 内置 | ✅ 类型提示 | Django 项目 |
| PonyORM | ✅ 原生 | ⚠️ 第三方 | ✅ | 简洁查询语法 |

---

### 缓存与消息队列

**Redis 验证要点**:
- [ ] 版本：7.0+（推荐），6.2 已 EOL
- [ ] Redis Stack（含 JSON、Search、TimeSeries）
- [ ] 集群模式支持
- [ ] 持久化方案（RDB/AOF）
- [ ] 内存优化（Hash tagging 等）

**消息队列验证要点**:

| 方案 | 特点 | 适用场景 | 验证重点 |
|------|------|---------|---------|
| Celery + RabbitMQ | 成熟稳定 | Python 异步任务 | Celery 5.x+ 支持 |
| BullMQ + Redis | 轻量快速 | Node.js 任务队列 | Redis 7+ 兼容 |
| Kafka | 高吞吐 | 事件驱动、日志 | Kafka 3.x+ |
| NATS | 云原生 | 微服务通信 | JetStream 支持 |

---

## 🛠️ 验证工具与自动化

### 手动验证清单

对每个技术，手动访问以下资源：

```markdown
## [技术名称] 验证 Checklist

### 官方信息
- [ ] 访问官方网站，确认最新版本号
- [ ] 查看 README 中的 "Last Updated" 时间
- [ ] 检查 Documentation 链接有效性
- [ ] 查看 License 信息

### GitHub 仓库
- [ ] 访问 GitHub Repo
- [ ] 查看 Stars 数量和趋势（Insights → Traffic）
- [ ] 检查 Latest Release 日期
- [ ] 浏览最近的 Commits（< 30 天？）
- [ ] 查看 Open Issues 数量和响应情况
- [ ] 检查 Contributors 数量

### 包管理器
- [ ] PyPI / npm: 查看最新版本和月下载量
- [ ] Docker Hub: 查看拉取数量和最后更新
- [ ] 检查依赖树是否有已知漏洞

### 安全信息
- [ ] 访问 https://cve.mitre.org/ 搜索 CVE
- [ ] 访问 GitHub Security Advisories
- [ ] 检查 snyk.io 的安全评级
- [ ] 搜索 "[技术名] vulnerability 2025/2026"

### 社区信息
- [ ] Stack Overflow: 搜索标签，看问题活跃度
- [ ] Reddit: 搜索 r/[技术名] 或相关 subreddit
- [ ] Discord/Slack: 加入官方社区看人数
- [ ] YouTube: 搜索最新教程视频日期
```

### 自动化验证脚本（示例）

```python
# scripts/tech_validator.py
"""
技术栈自动验证工具
使用 GitHub API 和 PyPI API 获取实时数据
"""

import requests
from datetime import datetime, timedelta
from dataclasses import dataclass
from typing import Optional


@dataclass
class TechValidationResult:
    name: str
    version: str
    category: str
    
    # 维度分数 (1-5)
    version_freshness: float
    maintenance_activity: float
    community_health: float
    security: float
    industry_adoption: float
    compatibility: float
    
    # 综合结果
    overall_score: float
    recommendation: str  # recommend/cautionary/not_recommended/must_replace
    
    # 详细数据
    latest_version: str
    last_release_date: Optional[datetime]
    last_commit_date: Optional[datetime]
    github_stars: int
    monthly_downloads: int
    open_issues: int
    cve_count: int
    
    # 风险标记
    risks: list[str]
    alternatives: list[str]


class TechValidator:
    """技术验证器"""
    
    def __init__(self):
        self.github_token = None  # 可选，提高 API 限制
        
    async def validate(self, tech_name: str, version: str, 
                       category: str, github_repo: Optional[str] = None,
                       pypi_package: Optional[str] = None) -> TechValidationResult:
        """
        验证单个技术
        
        Args:
            tech_name: 技术名称
            version: 项目指定的版本
            category: 类别 (language/framework/database/tool)
            github_repo: GitHub 仓库 (如 "tiangolo/fastapi")
            pypi_package: PyPI 包名 (如 "fastapi")
        """
        result = TechValidationResult(
            name=tech_name,
            version=version,
            category=category,
            risks=[],
            alternatives=[]
        )
        
        # 1. GitHub 数据
        if github_repo:
            await self._check_github(github_repo, result)
        
        # 2. PyPI/npm 数据
        if pypi_package and category in ("framework", "library", "tool"):
            await self._check_pypi(pypi_package, result)
        
        # 3. 安全检查
        await self._check_security(tech_name, result)
        
        # 4. 计算综合评分
        self._calculate_scores(result)
        
        return result
    
    async def _check_github(self, repo: str, result: TechValidationResult):
        """获取 GitHub 仓库数据"""
        url = f"https://api.github.com/repos/{repo}"
        headers = {}
        if self.github_token:
            headers["Authorization"] = f"token {self.github_token}"
        
        resp = requests.get(url, headers=headers, timeout=10)
        if resp.status_code == 200:
            data = resp.json()
            result.github_stars = data.get("stargazers_count", 0)
            result.open_issues = data.get("open_issues_count", 0)
            
            # 解析最后推送时间
            pushed_at = data.get("pushed_at")
            if pushed_at:
                result.last_commit_date = datetime.fromisoformat(
                    pushed_at.replace("Z", "+00:00")
                )
            
            # 获取最新 release
            releases_url = f"{url}/releases/latest"
            rel_resp = requests.get(releases_url, headers=headers, timeout=10)
            if rel_resp.status_code == 200:
                rel_data = rel_resp.json()
                result.latest_version = rel_data.get("tag_name", "").lstrip("v")
                published_at = rel_data.get("published_at")
                if published_at:
                    result.last_release_date = datetime.fromisoformat(
                        published_at.replace("Z", "+00:00")
                    )
    
    async def _check_pypi(self, package: str, result: TechValidationResult):
        """获取 PyPI 下载数据"""
        url = f"https://pypi.org/pypi/{package}/json"
        resp = requests.get(url, timeout=10)
        if resp.status_code == 200:
            data = resp.json()
            result.latest_version = data.get("info", {}).get("version", "")
    
    async def _check_security(self, tech_name: str, result: TechValidationResult):
        """检查安全漏洞"""
        # 这里可以接入 NVD API 或 Snyk API
        # 简化版：基于已知问题列表
        known_deprecated = {
            "python3.7": "Python 3.7 已于 2023-06 到达 EOL",
            "python3.8": "Python 3.8 将于 2024-10 到达 EOL",
            "python3.9": "Python 3.9 将于 2025-10 到达 EOL",
            "django2.2": "Django 2.2 LTS 已 EOL",
            "mysql5.7": "MySQL 5.7 已 EOL",
        }
        
        key = tech_name.lower().replace(" ", "").replace(".", "")
        for dep_key, warning in known_deprecated.items():
            if dep_key in key or key in dep_key:
                result.risks.append(warning)
                result.security = min(result.security, 2.0)
    
    def _calculate_scores(self, result: TechValidationResult):
        """计算各维度分数"""
        
        # 维度 1: 版本新鲜度
        if result.last_release_date:
            days_since_release = (datetime.now() - result.last_release_date).days
            if days_since_release < 30:
                result.version_freshness = 5.0
            elif days_since_release < 90:
                result.version_freshness = 4.0
            elif days_since_release < 180:
                result.version_freshness = 3.0
            elif days_since_release < 365:
                result.version_freshness = 2.0
            else:
                result.version_freshness = 1.0
        else:
            result.version_freshness = 3.0  # 无法判断，给中等分
        
        # 维度 2: 维护活跃度
        if result.last_commit_date:
            days_since_commit = (datetime.now() - result.last_commit_date).days
            if days_since_commit < 7:
                result.maintenance_activity = 5.0
            elif days_since_commit < 30:
                result.maintenance_activity = 4.0
            elif days_since_commit < 90:
                result.maintenance_activity = 3.0
            elif days_since_commit < 180:
                result.maintenance_activity = 2.0
            else:
                result.maintenance_activity = 1.0
        else:
            result.maintenance_activity = 3.0
        
        # 维度 3: 社区健康度（基于 stars）
        if result.github_stars >= 50000:
            result.community_health = 5.0
        elif result.github_stars >= 10000:
            result.community_health = 4.0
        elif result.github_stars >= 1000:
            result.community_health = 3.0
        elif result.github_stars >= 100:
            result.community_health = 2.0
        else:
            result.community_health = 1.5  # 小项目不一定不好
        
        # 维度 4: 安全性（初始值，会被 _check_security 降低）
        result.security = 5.0
        
        # 维度 5 & 6: 给默认中等分（需要人工判断补充）
        result.industry_adoption = 3.5
        result.compatibility = 3.5
        
        # 综合评分
        scores = [
            result.version_freshness,
            result.maintenance_activity,
            result.community_health,
            result.security,
            result.industry_adoption,
            result.compatibility,
        ]
        result.overall_score = sum(scores) / len(scores)
        
        # 推荐决策
        if result.overall_score >= 4.5:
            result.recommendation = "recommend"
        elif result.overall_score >= 3.5:
            result.recommendation = "recommend"
        elif result.overall_score >= 2.5:
            result.recommendation = "cautionary"
        elif result.overall_score >= 1.5:
            result.recommendation = "not_recommended"
        else:
            result.recommendation = "must_replace"


# 使用示例
if __name__ == "__main__":
    import asyncio
    
    async def main():
        validator = TechValidator()
        
        # 验证 FastAPI
        result = await validator.validate(
            tech_name="FastAPI",
            version="0.100+",
            category="framework",
            github_repo="tiangolo/fastapi",
            pypi_package="fastapi"
        )
        
        print(f"=== {result.name} 验证结果 ===")
        print(f"综合评分: {result.overall_score:.1f}/5.0")
        print(f"推荐决策: {result.recommendation}")
        print(f"GitHub Stars: {result.github_stars:,}")
        if result.risks:
            print(f"⚠️ 风险: {'; '.join(result.risks)}")
    
    asyncio.run(main())
```

---

## 📝 验证报告模板

### 完整报告结构

```markdown
# 技术栈验证报告

**项目**: [项目名称]
**功能**: [功能名称]
**验证日期**: YYYY-MM-DD HH:MM
**验证人**: AI (WebSearch 实时数据)

---

## 执行摘要

| 指标 | 结果 |
|-----|------|
| 总技术项 | X |
| ✅ 推荐 | X (X%) |
| ⚠️ 有条件推荐 | X (X%) |
| ❌ 不推荐 | X (X%) |
| 🔴 必须替换 | X (X%) |

**关键结论**: [一句话总结]

---

## 详细验证结果

（按类别分组展示每个技术的验证详情）

---

## 风险与建议

### 必须立即处理

### 建议本迭代内处理

### 可以观察

---

## 最终技术栈确认

（列出经过验证后的最终技术栈列表）

---

## 附录：原始数据来源
```

---

## ⚠️ 常见过时技术黑名单（2026 年更新）

以下技术**不建议在新项目中使用**：

### 已 EOL（End of Life）的语言/运行时
- ❌ Python ≤ 3.9（安全更新已停止）
- ❌ Node.js ≤ 18（LTS 周期结束）
- ❌ Go ≤ 1.20（不再收到安全补丁）
- ❌ Java 8 / 11（Oracle 官方不支持）

### 已停止维护的框架
- ❌ Flask-RESTful（已被 FastAPI 取代）
- ❌ Tornado（维护停滞，性能不如 ASGI）
- ❌ Pyramid（社区极小）
- ❌ Express.js 4.x（Express 5 已发布多年）

### 已废弃的数据库
- ❌ MySQL 5.7（EOL，安全风险）
- ❌ MongoDB 4.4 及更早（缺少重要安全特性）
- ❌ Redis 6.2 及更早（缺少 ACL 改进）

### 不推荐使用的工具
- ❌ XML-RPC / SOAP（已被 REST/gRPC 取代）
- ❌ jQuery（现代框架已内置 DOM 操作）
- ❌ Gulp（Webpack/Vite 已取代）
- ❌ Babel（现代浏览器已原生支持 ES6+）

---

**版本**: 1.0.0  
**最后更新**: 2026-04-02  
**下次审查**: 每季度或启动新项目前  
**状态**: 🟢 生效中
