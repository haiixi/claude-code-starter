---
name: code-review
description: Conducts multi-axis code review. Use before merging any change, when reviewing code written by yourself, another agent, or a human.
triggers:
  - /code-review
  - 代码审查
  - review
---

# Code Review

## Overview

Multi-dimensional code review with quality gates. Every change gets reviewed before merge — no exceptions. Review covers five axes: correctness, readability, architecture, security, and performance.

**The approval standard:** Approve a change when it definitely improves overall code health, even if it isn't perfect.

## When to Use

- Before merging any PR or change
- After completing a feature implementation
- When another agent or model produced code you need to evaluate
- When refactoring existing code
- After any bug fix (review both the fix and the regression test)

## The Five-Axis Review

### 1. Correctness

- Does it match the spec or task requirements?
- Are edge cases handled (null, empty, boundary values)?
- Are error paths handled (not just the happy path)?
- Does it pass all tests? Are the tests actually testing the right things?

### 2. Readability & Simplicity

- Are names descriptive and consistent with project conventions?
- Is the control flow straightforward?
- Is the code organized logically?
- Could this be done in fewer lines?
- Are abstractions earning their complexity?

### 3. Architecture

- Does it follow existing patterns or introduce a new one?
- Does it maintain clean module boundaries?
- Is there code duplication that should be shared?
- Are dependencies flowing in the right direction?
- Is the abstraction level appropriate?

### 4. Security

- Is user input validated and sanitized?
- Are secrets kept out of code, logs, and version control?
- Is authentication/authorization checked where needed?
- Are SQL queries parameterized (no string concatenation)?
- Are outputs encoded to prevent XSS?
- Is data from external sources treated as untrusted?

### 5. Performance

- Any N+1 query patterns?
- Any unbounded loops or unconstrained data fetching?
- Any synchronous operations that should be async?
- Any missing pagination on list endpoints?
- Any large objects created in hot paths?

## Security Scan Focus

- 硬编码密钥 / token / 密码
- SQL 注入（字符串拼接）
- 命令注入（`os.system`、`subprocess shell=True`）
- 不安全反序列化（`pickle.loads`）
- `eval()` / `exec()` 调用
- 路径穿越

## Review Findings Severity

Label every comment with its severity:

| Prefix | Meaning | Action |
|--------|---------|--------|
| **Critical:** | Blocks merge | Security vulnerability, data loss, broken functionality |
| **Important:** | Should fix before merge | Logic error, maintainability issue |
| **Nit:** | Minor, optional | Formatting, style preferences |
| **Optional:** / **Consider:** | Suggestion | Worth considering but not required |
| **FYI** | Informational only | No action needed |

## Output Format

```markdown
## Review: [Change title]

### Summary
[Brief overall assessment]

### Findings

| Severity | Axis | Issue | Location | Suggestion |
|----------|------|-------|----------|------------|
| Critical | Security | 硬编码 API key | src/config.ts | 改用环境变量 |
| Important | Correctness | 未处理空值 | src/user.ts:42 | 添加 null check |
| Nit | Readability | 变量名 temp | src/utils.ts:15 | 改为具体名称 |

### Verdict
- [ ] Approve — Ready to merge
- [ ] Request changes — Issues must be addressed
```

## Review Checklist

- [ ] I understand what this change does and why
- [ ] Change matches spec/task requirements
- [ ] Edge cases handled
- [ ] Error paths handled
- [ ] Tests cover the change adequately
- [ ] Names are clear and consistent
- [ ] No unnecessary complexity
- [ ] Follows existing patterns
- [ ] No secrets in code
- [ ] Input validated at boundaries
- [ ] No N+1 patterns
- [ ] Tests pass
- [ ] Build succeeds

## Red Flags

- PRs merged without any review
- "LGTM" without evidence of actual review
- Security-sensitive changes without security-focused review
- Large PRs that are "too big to review properly" (split them)
- No regression tests with bug fix PRs
- Accepting "I'll fix it later" — it rarely happens
