# Git Branch Naming Convention

## General Structure

```
<type>/<reference>/<short-description>
```

## Branch Types

### Main Branches
- **`main`** - Production branch
- **`develop`** - Development branch

### Work Branches

#### Features (New functionality)
```
feat/<ticket-id>/<description>
```
**Examples:**
- `feat/USER-123/oauth-authentication`
- `feat/TASK-456/payment-api-integration`
- `feat/improvement/performance-optimization`

#### Bugfixes (Bug corrections)
```
fix/<ticket-id>/<description>
hotfix/<ticket-id>/<description>  // For urgent fixes
```
**Examples:**
- `fix/BUG-789/tax-calculation-error`
- `hotfix/CRITICAL-101/login-security-flaw`

#### Releases (Version preparation)
```
release/<version>
```
**Examples:**
- `release/v1.2.0`
- `release/v2.0.0-beta`

#### Support and maintenance
```
support/<version>/<description>
chore/<description>
```
**Examples:**
- `support/v1.0/legacy-maintenance`
- `chore/update-dependencies`

## Naming Rules

### Accepted Formats
- **All lowercase**
- **Use hyphens (-) to separate words**
- **No spaces, accents, or special characters**
- **Maximum 50 characters**

### Descriptions
- Use **imperative** form for actions
- Be **descriptive but concise**
- Avoid ambiguous abbreviations

## Examples by Context

### Feature Development
```bash
# New user page
feat/USER-234/create-profile-page

# API integration
feat/API-567/notification-service-integration

# UX improvement
feat/UX-890/mobile-navigation-redesign
```

### Bug Fixes
```bash
# Standard bug
fix/BUG-123/table-display-issue

# Critical bug requiring hotfix
hotfix/SECURITY-456/sql-injection-fix

# Minor bug
fix/minor/button-typo-correction
```

### Maintenance and Technical Tasks
```bash
# Dependencies update
chore/update-spring-boot

# CI/CD configuration
chore/jenkins-pipeline-config

# Documentation
chore/rest-api-documentation
```

### Releases and Versions
```bash
# Major version
release/v2.0.0

# Minor version with fixes
release/v1.3.1

# Beta version
release/v2.0.0-beta
```

## Recommended Workflow

### 1. Branch Creation
```bash
# Start from develop for features
git checkout develop
git pull origin develop
git checkout -b feat/USER-123/oauth-authentication

# Start from main for hotfixes
git checkout main
git pull origin main
git checkout -b hotfix/CRITICAL-456/security-flaw
```

### 2. Working on Branch
```bash
# Regular commits with clear messages
git add .
git commit -m "feat: add OAuth authentication service"
git push origin feat/USER-123/oauth-authentication
```

### 3. Merging
```bash
# Create Pull Request to develop (or main for hotfix)
# After validation and tests, merge and delete branch
git branch -d feat/USER-123/oauth-authentication
git push origin --delete feat/USER-123/oauth-authentication
```

## Forbidden Branches

❌ **Absolutely avoid:**
- `test`
- `temp`
- `fix` (without ticket reference)
- `new-feature`
- `dev-john`
- `working`
- `patch`

## Tools and Automation

### Git Hooks (optional)
Create a hook to automatically validate branch name format:

```bash
#!/bin/sh
# .git/hooks/pre-push

branch=$(git rev-parse --abbrev-ref HEAD)
valid_pattern="^(feat|fix|hotfix|release|chore|support)\/[a-z0-9-]+\/[a-z0-9-]+$|^(main|develop)$"

if [[ ! $branch =~ $valid_pattern ]]; then
  echo "❌ Invalid branch name: $branch"
  echo "Expected format: <type>/<reference>/<description>"
  exit 1
fi
```

## Special Cases

### Collaboration Branches
For team work on the same feature:
```
feat/USER-123/oauth-authentication
feat/USER-123/oauth-authentication-john
feat/USER-123/oauth-authentication-mary
```

### Experimentation Branches
```
experiment/<description>
spike/<description>
```
**Examples:**
- `experiment/new-ui-library-test`
- `spike/microservices-evaluation`

### Documentation Branches
```
docs/<topic>
```
**Examples:**
- `docs/installation-guide`
- `docs/api-reference`

---

**Note:** This convention should be adapted according to your ticket management tools (Jira, GitHub Issues, etc.) and team specifics.
