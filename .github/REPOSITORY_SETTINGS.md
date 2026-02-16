# Repository Settings Documentation

## Branch Protection Rules

This document describes the branch protection rules for this repository. These settings should be configured in GitHub repository settings.

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

8. **Allow force pushes**: ❌

9. **Allow deletions**: ❌

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

To apply these settings:

1. Go to repository Settings → Branches
2. Add branch protection rule for `main`
3. Configure all the settings listed above
4. Go to Settings → Manage access
5. Add collaborators with appropriate permissions
6. Go to Settings → Secrets and variables → Actions
7. Add `OPENAI_API_KEY` if using AI code review

## Additional Security Settings

- **Dependency graph**: ✅ Enabled
- **Dependabot alerts**: ✅ Enabled  
- **Dependabot security updates**: ✅ Enabled
- **Code scanning**: ✅ Enabled via GitHub Actions
- **Secret scanning**: ✅ Enabled

---

For more information, see [CONTRIBUTING.md](../CONTRIBUTING.md)
