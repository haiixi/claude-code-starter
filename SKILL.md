---
name: claude-code-starter
description: 一键初始化 Claude Code 最佳实践配置，安装 CLAUDE.md、推荐 Skills、Plugins 和 MCP，并生成使用说明。
triggers:
  - /claude-starter
  - /claude-code-starter
  - 初始化 claude code
  - 配置 claude code
  - 新电脑 claude code
disable-model-invocation: true
---

# /claude-starter

在新电脑或新项目中快速搭建 Claude Code 最佳实践环境。

## 使用场景

- 新机器或刚安装 Claude Code
- 新成员入职
- 希望统一规则、Skills、Plugins 和文档基线

## 用法

```text
/claude-starter              # 交互式向导
/claude-starter global       # 安装用户级 CLAUDE.md + 使用说明
/claude-starter project      # 为当前项目生成 CLAUDE.md + 使用说明
/claude-starter docs         # 仅刷新使用说明
```

## 安装内容

1. **CLAUDE.md** — 全局或项目级规则文件
2. **MCP 配置** — 连接 GitHub、文件系统、网页抓取
3. **推荐 Skills** — 验证是否已安装，缺失时给出安装命令
4. **推荐 Plugins** — 生成 `/plugin install` 命令（需手动在 Claude Code 中执行）
5. **USAGE.md** — 当前环境的快速参考手册

## 安全规则

- 覆盖已有文件前必须征求确认
- 覆盖前先读取原文件内容
- 如需备份，先复制到 `target.<timestamp>.bak`
- 不自动执行 `/plugin install`，只生成命令
- 不自动修改 `settings.json`，只生成建议配置

## 步骤工作流

### 步骤 1 — 确定模式

如果 `ARGUMENTS` 为空，询问用户：

- `global` — 配置 `~/.claude/CLAUDE.md`
- `project` — 为当前工作目录生成 `./.claude/CLAUDE.md`
- `docs` — 仅刷新使用说明

### 步骤 2 — 检测环境

```bash
mkdir -p "$HOME/.claude/claude-starter"
echo "$HOME/.claude"
```

设置：

- `CLAUDE_HOME = $HOME/.claude`
- `SKILL_DIR = $CLAUDE_HOME/skills/claude-code-starter`

### 步骤 3 — 安装 CLAUDE.md

根据模式选择模板：

| 模式 | 源模板 | 目标路径 |
|------|--------|----------|
| global | `$SKILL_DIR/templates/global-claude.md` | `$CLAUDE_HOME/CLAUDE.md` |
| project | `$SKILL_DIR/templates/project-claude.md` | `./.claude/CLAUDE.md` |
| docs | 跳过 | — |

操作逻辑：

- 目标不存在：直接写入
- 目标已存在：展示前 40 行或 diff 摘要，询问 `overwrite / skip / backup-and-overwrite`
- 备份：先复制为 `target.<timestamp>.bak`

完成后输出：

```text
已安装 <mode> CLAUDE.md 位于 <path>
```

### 步骤 4 — 验证推荐 Skills

读取 `$SKILL_DIR/recommended-skills.md`。对每个 skill：

- 检查 `$CLAUDE_HOME/skills/<name>/SKILL.md` 是否存在
- 记录状态：present / missing

不自动安装缺失的 skill，而是生成一个安装表，包含：

- skill 名称
- 当前状态
- 安装来源（GitHub URL 或 marketplace 命令）

### 步骤 5 — 生成 Plugin 安装命令

读取 `$SKILL_DIR/recommended-plugins.md`，为每个 plugin 生成：

```text
/plugin install commit-commands@claude-plugins-official
```

注意：这些命令需要在 **Claude Code 会话内** 运行，不能直接放到 shell 脚本里执行。

生成文件：

- `$CLAUDE_HOME/claude-starter/install-plugins.md` — Claude Code 中粘贴执行的命令列表

### 步骤 6 — 安装 MCP 配置

将 `$SKILL_DIR/recommended-mcp.json` 中的配置合并到 `$CLAUDE_HOME/settings.json`。

合并规则：

- 如果 `settings.json` 不存在，直接写入
- 如果已存在，合并 `mcpServers`，不覆盖现有的 server
- 需要用户确认后才修改

完成后提醒用户：

- 填充 GitHub token
- 填充 filesystem 允许访问的路径

### 步骤 7 — 生成使用文档

基于 `$SKILL_DIR/USAGE.md` 生成：

- `$CLAUDE_HOME/claude-starter/USAGE.md`
- 如果模式是 `project`，同时生成 `./CLAUDE_USAGE.md`

附加：

- 生成时间
- CLAUDE.md 安装状态
- Skills 验证表
- Plugin 安装命令
- MCP 配置状态

### 步骤 8 — 最终报告

输出简洁摘要：

- 哪些文件已创建/更新
- 哪些步骤被跳过
- 接下来需要手动执行的命令
- 如何继续使用（`/claude-starter docs` 刷新文档）

## 失败处理

- 如果 `$SKILL_DIR` 或任何必需的打包文件缺失，停止并报告缺失路径
- 如果读写操作失败，报告错误并停止
- 如果用户拒绝覆盖，跳过该步骤并继续
