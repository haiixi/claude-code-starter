# Claude Code Starter Kit — 使用说明

本说明由 `/claude-starter` 自动生成，记录了你当前已配置的规则、推荐的 skills 和 plugins。

## 快速开始

```text
# 新机器/全局配置
/claude-starter global

# 给当前项目生成 CLAUDE.md
/claude-starter project

# 仅刷新这份使用说明
/claude-starter docs
```

## 推荐 Skills 速查

| Skill | 触发方式 | 什么时候用 |
|---|---|---|
| using-agent-skills | 自动或 `/using-agent-skills` | 不确定该用哪个 skill 时 |
| context-engineering | `/context-engineering` | 开始新会话、切换任务、上下文质量下降 |
| spec-driven-development | `/spec-driven-development` | 新项目/新功能/重大改动，先写 spec |
| planning-and-task-breakdown | `/planning-and-task-breakdown` | 有 spec 后拆成可执行任务 |
| incremental-implementation | `/incremental-implementation` | 多文件实现，切片交付 |
| test-driven-development | `/test-driven-development` | 写逻辑、修 bug、改行为 |
| code-review-and-quality | `/code-review-and-quality` | 合并前做代码审查 |
| security-and-hardening | `/security-and-hardening` | 处理用户输入、认证、外部 API |
| code-simplification | `/code-simplification` | 代码能跑但可读性差 |
| git-workflow-and-versioning | `/git-workflow-and-versioning` | 提交、分支、合并 |
| documentation-and-adrs | `/documentation-and-adrs` | 写文档、做架构决策记录 |
| debugging-and-error-recovery | `/debugging-and-error-recovery` | 测试失败、构建报错、行为异常 |
| frontend-ui-engineering | `/frontend-ui-engineering` | 构建或修改用户界面 |

## 推荐 Plugins 速查

| Plugin | 安装命令 | 用途 |
|---|---|---|
| commit-commands | `/plugin install commit-commands@claude-plugins-official` | `/commit`、`/commit-push-pr` |
| pr-review-toolkit | `/plugin install pr-review-toolkit@claude-plugins-official` | PR 审查 agent |
| code-review | `/plugin install code-review@claude-plugins-official` | 自动化代码审查 |
| code-simplifier | `/plugin install code-simplifier@claude-plugins-official` | 重构简化代码 |
| frontend-design | `/plugin install frontend-design@claude-plugins-official` | 高质量 UI 组件 |
| feature-dev | `/plugin install feature-dev@claude-plugins-official` | 端到端功能开发 |
| hookify | `/plugin install hookify@claude-plugins-official` | 自动化规则/Hook |

## 典型新手工作流

```text
1. 进入新项目 → /claude-starter project
2. 需求不清楚 → /idea-refine
3. 有需求后  → /spec-driven-development
4. 拆任务    → /planning-and-task-breakdown
5. 写代码    → /incremental-implementation + /test-driven-development
6. 提交前    → /code-review-and-quality
7. 提交      → /commit
```

## 更新本套件

1. 修改 `~/.claude/skills/claude-code-starter/recommended-skills.md` 或 `recommended-plugins.md`。
2. 运行 `/claude-starter docs` 重新生成使用说明。
3. 运行 `/claude-starter global` 或 `/claude-starter project` 更新对应的 `CLAUDE.md`。

## 可选增强

- `/graphify` — 把代码库/文档转成知识图（需已安装 Graphify）。
- `Superpowers` — 高级 agent 能力（如需要请自行安装）。
