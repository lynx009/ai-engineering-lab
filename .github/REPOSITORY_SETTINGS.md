# Repository Settings Documentation

## Branch Protection Rules

This document describes the branch protection rules for this repository. These settings **must be configured** in GitHub repository settings to provide actual protection.

> **⚠️ IMPORTANT**: The files in `.github/` directory (including `settings.yml`) are documentation and configuration templates. The actual branch protection enforcement happens only when these settings are configured in GitHub's web interface at Settings → Branches.

### Automated Monitoring

A GitHub Actions workflow (`branch-protection-monitor.yml`) runs daily to verify that branch protection is correctly configured. If issues are detected, it will automatically create an issue to alert repository administrators.

### Main Branch Protection

The `main` branch should have the following protections enabled:

#### Required Settings:

1. **Require pull request reviews before merging**
   - Required approving reviews: 1
   - Dismiss stale pull request approvals when new commits are pushed: ✅
   - Require review from Code Owners: ✅ (enforces CODEOWNERS file)

2. **Require status checks to pass before merging**
   - Require branches to be up to date before merging: ✅
   - Status checks that are required:
     - `AI Code Review`
     - `PR Validation`
     - `Code Quality Analysis`

3. **Require conversation resolution before merging**: ✅

4. **Require signed commits**: Optional (recommended)

5. **Require linear history**: ✅ (prevents merge commits)

6. **Include administrators**: ❌ 
   - This allows repository owner @lynx009 to bypass protections when necessary

7. **Restrict who can push to matching branches**
   - People, teams, or apps allowed to push: @lynx009

8. **Allow force pushes**: ❌ **CRITICAL - MUST BE DISABLED**
   - This prevents anyone from force pushing to main, which could overwrite history
   - Force pushes can cause data loss and bypass code review

9. **Allow deletions**: ❌ **CRITICAL - MUST BE DISABLED**
   - This prevents the main branch from being deleted accidentally or maliciously
   - Deleting the main branch would cause severe disruption

### Collaborator Permissions

#### Repository Roles:

- **Owner (@lynx009)**: Full access including bypassing branch protections
- **Write Access (Collaborators)**: Can create branches and open PRs, but cannot push to `main` directly
- **Read Access (Contributors)**: Must fork the repository to contribute

#### Recommended Collaborator Workflow:

1. Collaborators can create feature branches directly in the repository
2. Push changes to feature branches
3. Open pull requests to merge into `main`
4. Wait for required reviews and status checks
5. Once approved, @lynx009 or designated reviewers can merge

#### New Contributor Workflow:

1. Fork the repository to their own account
2. Create feature branches in their fork
3. Open pull requests from their fork to the main repository
4. Follow the same review process as collaborators

### GitHub Apps and Bots

The following apps should have appropriate permissions:

1. **GitHub Copilot**: Code review and suggestions
2. **CodeQL**: Security scanning
3. **Dependabot**: Dependency updates and security alerts

### Webhook and Integration Settings

- Enable GitHub Actions
- Enable GitHub Copilot for the repository
- Configure OpenAI API key in repository secrets (for AI code review)

## Setup Instructions

### Critical: Configure Branch Protection

To apply these settings and **actually protect** the main branch:

1. **Go to repository Settings → Branches**
   - URL: `https://github.com/lynx009/ai-engineering-lab/settings/branches`

2. **Add branch protection rule for `main`**
   - Click "Add branch protection rule"
   - Branch name pattern: `main`

3. **Configure all protection settings** (see list above)
   - Pay special attention to:
     - ❌ Allow force pushes: **MUST BE UNCHECKED**
     - ❌ Allow deletions: **MUST BE UNCHECKED**

4. **Click "Create" or "Save changes"**

5. **Optional: Install Probot Settings App**
   - Install from: https://github.com/apps/settings
   - This will automatically apply settings from `.github/settings.yml`

### Additional Setup

6. Go to Settings → Manage access
7. Add collaborators with appropriate permissions
8. Go to Settings → Secrets and variables → Actions
9. Add `OPENAI_API_KEY` if using AI code review

### Verification

After configuring, the `branch-protection-monitor` workflow will verify settings daily. You can also run it manually:
- Go to Actions → Branch Protection Monitor → Run workflow

## Additional Security Settings

- **Dependency graph**: ✅ Enabled
- **Dependabot alerts**: ✅ Enabled  
- **Dependabot security updates**: ✅ Enabled
- **Code scanning**: ✅ Enabled via GitHub Actions
- **Secret scanning**: ✅ Enabled

---

For more information, see [CONTRIBUTING.md](../CONTRIBUTING.md)
