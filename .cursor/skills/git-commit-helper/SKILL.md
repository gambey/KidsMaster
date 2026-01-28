---
name: git-commit-helper
description: Generate descriptive commit messages using Conventional Commits format by analyzing git diffs. Automatically suggests type and scope based on changed files. Use when the user asks for help writing commit messages, mentions git commit, or when reviewing staged changes.
---

# Git Commit Message Helper

## Quick Start

When the user needs help with commit messages:

1. Analyze the git diff (staged or unstaged changes)
2. Identify the change type and scope from file paths
3. Generate a commit message following Conventional Commits format
4. Provide both subject line and optional body

## Commit Format

Use Conventional Commits format:

```
<type>(<scope>): <subject>

[optional body]
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `refactor`: Code refactoring without changing functionality
- `style`: Formatting, missing semicolons, etc. (no code change)
- `docs`: Documentation changes
- `test`: Adding or updating tests
- `chore`: Build process, tooling, dependencies
- `perf`: Performance improvements
- `ci`: CI/CD changes

### Scopes (based on project structure)

Infer scope from file paths:

- `home`: Changes in `pages/home/`
- `game`: Changes in `pages/game/` (including subdirectories)
- `mine`: Changes in `pages/mine/`
- `community`: Changes in `pages/community/`
- `utils`: Changes in `utils/`
- `config`: Changes in `pages.json`, `manifest.json`, `App.uvue`
- `static`: Changes in `static/`
- `build`: Changes in build/config files

If multiple scopes are involved, use the most significant one or omit scope.

### Subject Line Rules

- Use imperative mood ("add" not "added" or "adds")
- No period at the end
- First letter lowercase (unless starting with proper noun)
- Keep under 72 characters
- Be specific and descriptive

### Body (Optional)

Include body when:
- The change needs explanation
- Multiple related changes
- Breaking changes (start with `BREAKING CHANGE:`)

## Workflow

1. **Get the diff**:
   ```bash
   git diff --cached  # staged changes
   git diff          # unstaged changes
   ```

2. **Analyze changes**:
   - Identify modified files
   - Determine primary change type
   - Infer scope from file paths
   - Summarize what changed

3. **Generate commit message**:
   - Format: `type(scope): concise subject`
   - Add body if needed for clarity

## Examples

**Example 1: New feature**
```
Input: Added calendar functionality to home page
Files: pages/home/home.uvue

Output:
feat(home): add calendar component with stamp tracking

Implement monthly calendar view with child/parent stamp indicators
and navigation controls
```

**Example 2: Bug fix**
```
Input: Fixed date formatting issue in edit child page
Files: pages/mine/edit-child.uvue

Output:
fix(mine): correct date formatting in edit child form

Fix timezone conversion issue causing incorrect date display
```

**Example 3: Multiple files**
```
Input: Updated API calls and child management UI
Files: utils/api.uts, pages/mine/child-management.uvue

Output:
refactor(mine): update child management API integration

- Standardize API error handling in utils/api.uts
- Update child-management UI to use new API structure
```

**Example 4: Configuration**
```
Input: Updated app manifest settings
Files: manifest.json

Output:
chore(config): update manifest configuration

Update app version and permissions settings
```

## Trigger Scenarios

Apply this skill when:
- User explicitly asks: "help me write commit message", "生成提交信息", "/commit-msg"
- User mentions: "git commit", "提交", "commit message"
- User is reviewing staged changes and needs commit message
- User asks about commit format or conventions

## Language Support

- Support both English and Chinese (中文) in commit messages
- Prefer English for type/scope keywords (standard convention)
- Subject and body can be in either language based on user preference
