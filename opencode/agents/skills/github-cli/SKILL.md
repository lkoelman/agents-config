---
name: github-cli
description: Use GitHub CLI
compatibility: opencode
allowed-tools:
  - bash
  - question
---

## When to use me

When using the GitHub CLI (`gh` command) to perform GitHub-related actions.
Ask user for confirmation before replying to comments or pushing any information to github.

## Common GitHub Actions


### PR Review

```bash
# view PR thread as markdown, without inline review comments
gh pr view <pr-number>

# Get PR reviews as JSON - use for retrieving comment ids
gh pr-review review view --pr <pr-number> -R <owner/repo>

# retrieve inline review comments that are unresolved
# get owner/repo using `git remote get-url $(git remote)`
gh pr-review review view --pr <pr-number> -R <owner/repo> --unresolved | jq '.reviews[].comments[]? | select(.is_resolved == false)'

# Reply to review comment
gh pr-review comments reply -R owner/repo --pr 123 --thread-id PRRT_kwDOAAABbcdEFG12 --body "Follow-up addressed in commit abc123"
```

### Find repos with specific files/directories

```bash
gh search code "path:.skilz" --json repository --jq '.[].repository.fullName'
gh search code --filename SKILL.md
gh search code --filename Dockerfile --language python
```

### Create resources

```bash
gh pr create --title "Feature" --body "Description" --reviewer @user
gh issue create --title "Bug" --label bug,urgent --assignee @me
gh repo fork owner/repo --clone
```