---
name: git-workflow
description: "Git and GitHub workflow operations. Use when committing code, pushing changes, checking status, creating branches, or managing the repository. Covers common git commands, conventional commits, and safe push practices."
---

# Git Workflow Skill

## When to Use
- Committing and pushing prototype files to GitHub
- Checking repository status before/after changes
- Creating feature branches for new prototypes
- Resolving common git issues (merge conflicts, untracked files)

## Prerequisites
- `git` must be installed and configured with user name/email
- The repository must have a remote named `origin` pointing to GitHub
- SSH key or HTTPS credentials must be set up for push access

## Common Workflows

### 1. Commit All Changes (Most Common)
After building or updating prototypes, commit everything:

```bash
# 1. Check what's changed
git status

# 2. Stage all changes
git add -A

# 3. Commit with a descriptive message
git commit -m "feat: add capacity planning prototype v3"

# 4. Push to remote
git push origin main
```

### 2. Commit Specific Files
When only certain files should be committed:

```bash
# Stage specific files
git add prototypes/version-3.html
git add .github/agents/new-agent.agent.md

# Commit
git commit -m "feat: add version 3 prototype and new agent"

# Push
git push origin main
```

### 3. First-Time Setup (New Project)
When plugging this agent system into a brand new project:

```bash
# Initialize git (if not already)
git init

# Add remote
git remote add origin https://github.com/{user}/{repo}.git

# Stage everything
git add -A

# Initial commit
git commit -m "feat: initialize agent pipeline and design system"

# Push (set upstream)
git push -u origin main
```

### 4. Create Feature Branch
For working on a new prototype without affecting main:

```bash
# Create and switch to new branch
git checkout -b prototype/feature-name

# ... do work ...

# Commit and push the branch
git add -A
git commit -m "feat: build feature-name prototype"
git push -u origin prototype/feature-name
```

## Conventional Commit Messages

Always use this format: `type: short description`

| Type | When to Use | Example |
|------|------------|---------|
| `feat` | New prototype or agent added | `feat: add capacity planning prototype v2` |
| `fix` | Bug fix in existing prototype | `fix: correct grid column alignment in v2` |
| `style` | DS token or visual-only changes | `style: replace Supply tokens with MH equivalents` |
| `refactor` | Code restructuring, no visual change | `refactor: extract grid component into separate section` |
| `docs` | README, SETUP, or instruction updates | `docs: update SETUP.md with new agent descriptions` |
| `chore` | Config, tooling, or maintenance | `chore: add .gitkeep to prototypes folder` |

## Pre-Push Checklist

Before pushing, verify:

1. **No sensitive data** — no API keys, tokens, or passwords in committed files
2. **No node_modules** — should be in `.gitignore` (not applicable for CDN projects)
3. **All files intentional** — run `git status` to review staged files
4. **Meaningful commit message** — follows conventional commit format
5. **Correct branch** — verify you're on the right branch with `git branch`

## Troubleshooting

### "rejected — non-fast-forward"
Remote has changes you don't have locally:
```bash
git pull --rebase origin main
# Resolve any conflicts, then:
git push origin main
```

### "untracked files"
New files that need to be staged:
```bash
git add -A  # Add everything
# OR
git add path/to/specific/file  # Add selectively
```

### "nothing to commit"
All changes are already committed. Just push:
```bash
git push origin main
```

### Check What Will Be Pushed
```bash
git log origin/main..HEAD --oneline
```

## Safety Rules
- **NEVER** use `git push --force` without explicit user confirmation
- **NEVER** use `git reset --hard` without explicit user confirmation
- **ALWAYS** run `git status` before committing to verify what's staged
- **ALWAYS** use descriptive commit messages, never empty or "update"
- **PREFER** `git pull --rebase` over `git pull` to keep history clean
