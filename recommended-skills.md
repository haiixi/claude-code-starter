# 推荐 Skills

以下 skill 可从对应来源安装。安装方式：将 skill 文件夹复制到 `~/.claude/skills/<name>/`。

## 核心工作流

| Skill | 作用 | 安装来源 |
|-------|------|----------|
| `using-agent-skills` | 发现并调用合适的 workflow skill | 官方 marketplace 或社区 skill 合集 |
| `context-engineering` | 在合适时机加载合适上下文 | https://agentcookbooks.com/skills/context-engineering/ |
| `spec-driven-development` | 先写规格再编码 | https://agentcookbooks.com/skills/spec-driven-development/ |
| `incremental-implementation` | 分小步骤交付 | https://agentcookbooks.com/skills/incremental-implementation/ |
| `test-driven-development` | 先写失败测试，再让它通过 | https://agentcookbooks.com/skills/test-driven-development/ |

## 代码质量

| Skill | 作用 | 安装来源 |
|-------|------|----------|
| `code-review-and-quality` | 合并前多维度审查 | 社区 skill 合集 |
| `security-and-hardening` | OWASP 防御与输入验证 | 社区 skill 合集 |
| `code-simplification` | 简化代码同时保持行为不变 | 社区 skill 合集 |
| `frontend-ui-engineering` | 生产级 UI 构建 | 社区 skill 合集 |

## Git 与协作

| Skill | 作用 | 安装来源 |
|-------|------|----------|
| `git-workflow-and-versioning` | 规范提交和历史 | 社区 skill 合集 |
| `documentation-and-adrs` | 记录决策和文档 | 社区 skill 合集 |

## 规划与调试

| Skill | 作用 | 安装来源 |
|-------|------|----------|
| `planning-and-task-breakdown` | 把工作拆成有序任务 | 社区 skill 合集 |
| `debugging-and-error-recovery` | 系统性根因调试 | 社区 skill 合集 |

## 内置保底 Skills

如果外部 skill 暂时无法下载，以下技能随本配置包提供：

| Skill | 触发词 |
|-------|--------|
| `coding-standards` | `/coding-standards` |
| `test-workflow` | `/test-workflow` |
| `git-commit` | `/git-commit` |
| `code-review` | `/code-review` |
| `refactor-clean` | `/refactor-clean` |
