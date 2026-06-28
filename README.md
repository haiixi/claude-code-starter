# Claude Code Starter Kit

一键初始化 Claude Code 最佳实践配置。合并了两套方案的优势：

- 生产级 `CLAUDE.md` 模板（含验证清单、上下文层级、安全边界）
- 命令式 Skill `/claude-starter`（支持 `global / project / docs` 三种模式）
- 推荐的外部 Skills 和官方 Plugins
- MCP 配置（GitHub / filesystem / fetch）
- 5 个中文内置保底 Skills

## 安装

```bash
# 克隆到本地 skills 目录
git clone https://github.com/haiixi/claude-code-starter.git
cp -r claude-code-starter ~/.claude/skills/
```

Windows PowerShell:

```powershell
git clone https://github.com/haiixi/claude-code-starter.git
Copy-Item -Recurse -Force "claude-code-starter" "$env:USERPROFILE\.claude\skills"
```

## 使用

启动 Claude Code，运行：

```text
/claude-starter              # 交互式向导
/claude-starter global       # 安装用户级 CLAUDE.md + 使用说明
/claude-starter project      # 为当前项目生成 CLAUDE.md + 使用说明
/claude-starter docs         # 仅刷新使用说明
```

## 目录结构

```
.
├── SKILL.md                      # 主 Skill
├── USAGE.md                      # 使用说明模板
├── recommended-skills.md         # 推荐 Skills 及安装来源
├── recommended-plugins.md        # 推荐 Plugins 及安装命令
├── recommended-mcp.json          # MCP 配置建议
├── templates/
│   ├── global-claude.md          # 全局 CLAUDE.md 模板
│   └── project-claude.md         # 项目级 CLAUDE.md 模板
└── fallback-skills/              # 中文保底 Skills
    ├── coding-standards/
    ├── test-workflow/
    ├── git-commit/
    ├── code-review/
    └── refactor-clean/
```

## 配置完成后

1. 安装推荐的 Plugins（在 Claude Code 会话内执行）
2. 根据 `recommended-skills.md` 安装外部 Skills
3. 填充 MCP 配置中的 GitHub token 和文件系统路径
4. 如果外部 skill 缺失，可以使用 `fallback-skills/` 中的保底版本

## 更新历史

- 2026-06-28: 整合优化，修复 `trigger` 为 `triggers`，汉化，加入 MCP 和保底 Skills
