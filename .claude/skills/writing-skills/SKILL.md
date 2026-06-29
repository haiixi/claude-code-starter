---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment.
triggers:
  - /writing-skills
  - /skill-guide
---

# Writing Skills

## Overview

Writing skills is Test-Driven Development applied to process documentation.

You write test cases (pressure scenarios), watch them fail (baseline behavior), write the skill (documentation), watch tests pass (compliance), and refactor (close loopholes).

**Core principle:** If you didn't watch an agent fail without the skill, you don't know if the skill teaches the right thing.

## What is a Skill?

A **skill** is a reference guide for proven techniques, patterns, or tools.

**Skills are:** Reusable techniques, patterns, tools, reference guides

**Skills are NOT:** Narratives about how you solved a problem once

## When to Create a Skill

**Create when:**
- Technique wasn't intuitively obvious
- You'd reference this again across projects
- Pattern applies broadly (not project-specific)
- Others would benefit

**Don't create for:**
- One-off solutions
- Standard practices well-documented elsewhere
- Project-specific conventions (put in CLAUDE.md)
- Mechanical constraints (automate those instead)

## Skill Types

| Type | Description | Example |
|------|-------------|---------|
| **Technique** | Concrete method with steps | condition-based-waiting |
| **Pattern** | Way of thinking about problems | flatten-with-flags |
| **Reference** | API docs, syntax guides | office docs |

## Directory Structure

```
skills/
  skill-name/
    SKILL.md              # Main reference (required)
    supporting-file.*     # Only if needed
```

**Keep inline:**
- Principles and concepts
- Code patterns (< 50 lines)

**Separate files for:**
- Heavy reference (100+ lines)
- Reusable tools/scripts

## SKILL.md Structure

### Frontmatter

```yaml
---
name: skill-name
description: Use when [triggering condition]. [More context].
triggers:
  - /skill-name
  - keyword
---
```

- `name`: letters, numbers, hyphens only
- `description`: Third-person, describes ONLY when to use
- `description` max 1024 characters
- Start description with "Use when..."

### Body Structure

```markdown
# Skill Title

## Overview
One paragraph: what this skill does and why.

## When to Use
- Bullet list of specific situations
- When NOT to use

## Steps / Process
1. Step one
2. Step two
3. Step three

## Output Format
Template or example of expected output.

## Examples
### Good
...

### Bad
...

## Checklist
- [ ] Item one
- [ ] Item two

## Red Flags
- Warning sign one
- Warning sign two
```

## Writing Tips

1. **Be specific, not abstract**
   - Bad: "Be careful with errors"
   - Good: "Check for null before accessing user.email"

2. **Lead with action**
   - Bad: "This skill explains how to..."
   - Good: "Use this skill when you see..."

3. **Include examples**
   - Every rule needs a Good/Bad example

4. **Use checklists**
   - They force completeness

5. **Close loopholes**
   - List common rationalizations and why they're wrong

6. **Keep it scannable**
   - Use tables, lists, and clear headings

## Verification

Before considering a skill done:

- [ ] Skill has clear trigger conditions
- [ ] Steps are actionable without interpretation
- [ ] Examples show both good and bad cases
- [ ] Common mistakes are addressed
- [ ] A subagent or another model can follow it successfully
