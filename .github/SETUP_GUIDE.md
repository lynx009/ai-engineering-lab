# Setup Guide for Repository Collaboration Rules

[English](#english) | [中文](#中文)

---

## 中文

### 仓库协作规则设置指南

本指南将帮助仓库管理员配置分支保护规则和协作权限。

### 1️⃣ 配置分支保护规则

#### 在 GitHub 仓库设置中配置主分支保护：

1. **进入仓库设置**
   - 访问: `https://github.com/lynx009/ai-engineering-lab/settings`
   - 点击左侧菜单的 "Branches"

2. **添加分支保护规则**
   - 点击 "Add branch protection rule"
   - Branch name pattern: `main`

3. **配置保护规则**
   - ✅ **Require a pull request before merging**
     - Required approving reviews: `1`
     - ✅ Dismiss stale pull request approvals when new commits are pushed
     - ✅ Require review from Code Owners
   - ✅ **Require status checks to pass before merging**
     - ✅ Require branches to be up to date before merging
     - 必需的状态检查:
       - `AI Code Review`
       - `Validate Pull Request`
       - `Code Quality Analysis`
   - ✅ **Require conversation resolution before merging**
   - ✅ **Require linear history**
   - ❌ **Include administrators** (允许 @lynx009 在必要时绕过保护)
   - ✅ **Restrict who can push to matching branches**
     - 允许推送的用户: `lynx009`
   - ❌ **Allow force pushes**
   - ❌ **Allow deletions**

### 2️⃣ 配置协作者权限

#### 访问权限管理：

1. **进入访问管理**
   - 访问: `https://github.com/lynx009/ai-engineering-lab/settings/access`

2. **邀请协作者**
   - 点击 "Invite a collaborator"
   - 输入用户名
   - 选择权限级别: **Write**

#### 权限说明：

- **Admin** (@lynx009): 完全访问权限，包括仓库设置
- **Write** (协作者): 可以创建分支和 PR，但不能直接推送到 `main`
- **Read** (公开): 任何人都可以查看和 fork

### 3️⃣ 配置 AI 代码审查

#### 设置 OpenAI API 密钥：

1. **获取 OpenAI API 密钥**
   - 访问: https://platform.openai.com/api-keys
   - 创建新的 API 密钥

2. **添加到 GitHub Secrets**
   - 访问: `https://github.com/lynx009/ai-engineering-lab/settings/secrets/actions`
   - 点击 "New repository secret"
   - Name: `OPENAI_API_KEY`
   - Value: [您的 OpenAI API 密钥]
   - 点击 "Add secret"

### 4️⃣ 启用 GitHub 功能

#### 启用必要的 GitHub 功能：

1. **GitHub Actions**
   - 访问: Settings → Actions → General
   - ✅ Allow all actions and reusable workflows

2. **GitHub Copilot** (可选)
   - 访问: Settings → Copilot
   - ✅ Enable for this repository

3. **安全功能**
   - 访问: Settings → Security & analysis
   - ✅ Dependency graph
   - ✅ Dependabot alerts
   - ✅ Dependabot security updates
   - ✅ Code scanning (通过 GitHub Actions)
   - ✅ Secret scanning

### 5️⃣ 测试配置

#### 验证设置是否正常工作：

1. **创建测试分支**
   ```bash
   git checkout -b test/branch-protection
   git push origin test/branch-protection
   ```

2. **尝试直接推送到 main** (应该被拒绝)
   ```bash
   git checkout main
   echo "test" >> test.txt
   git add test.txt
   git commit -m "Test direct push"
   git push origin main  # 应该失败
   ```

3. **创建 PR 并验证**
   - 从测试分支创建 PR
   - 检查 AI 代码审查是否运行
   - 检查是否需要审批

### 📝 文档说明

- **CODEOWNERS**: 定义代码所有者，确保 @lynx009 必须审批所有更改
- **CONTRIBUTING.md**: 贡献者指南，说明贡献流程
- **REPOSITORY_SETTINGS.md**: 仓库设置文档
- **Issue Templates**: 标准化 Issue 提交
- **PR Template**: 标准化 Pull Request

---

## English

### Repository Collaboration Rules Setup Guide

This guide will help repository administrators configure branch protection
rules and collaboration permissions.

### 1️⃣ Configure Branch Protection Rules

#### Configure main branch protection in GitHub repository settings:

1. **Go to Repository Settings**
   - Visit: `https://github.com/lynx009/ai-engineering-lab/settings`
   - Click "Branches" in the left menu

2. **Add Branch Protection Rule**
   - Click "Add branch protection rule"
   - Branch name pattern: `main`

3. **Configure Protection Rules**
   - ✅ **Require a pull request before merging**
     - Required approving reviews: `1`
     - ✅ Dismiss stale pull request approvals when new commits are pushed
     - ✅ Require review from Code Owners
   - ✅ **Require status checks to pass before merging**
     - ✅ Require branches to be up to date before merging
     - Required status checks:
       - `AI Code Review`
       - `Validate Pull Request`
       - `Code Quality Analysis`
   - ✅ **Require conversation resolution before merging**
   - ✅ **Require linear history**
   - ❌ **Include administrators** (allows @lynx009 to bypass when necessary)
   - ✅ **Restrict who can push to matching branches**
     - Allowed to push: `lynx009`
   - ❌ **Allow force pushes**
   - ❌ **Allow deletions**

### 2️⃣ Configure Collaborator Permissions

#### Access Management:

1. **Go to Access Management**
   - Visit: `https://github.com/lynx009/ai-engineering-lab/settings/access`

2. **Invite Collaborators**
   - Click "Invite a collaborator"
   - Enter username
   - Select permission level: **Write**

#### Permission Descriptions:

- **Admin** (@lynx009): Full access including repository settings
- **Write** (Collaborators): Can create branches and PRs, but cannot push
  directly to `main`
- **Read** (Public): Anyone can view and fork

### 3️⃣ Configure AI Code Review

#### Set up OpenAI API Key:

1. **Get OpenAI API Key**
   - Visit: https://platform.openai.com/api-keys
   - Create a new API key

2. **Add to GitHub Secrets**
   - Visit:
     `https://github.com/lynx009/ai-engineering-lab/settings/secrets/actions`
   - Click "New repository secret"
   - Name: `OPENAI_API_KEY`
   - Value: [Your OpenAI API Key]
   - Click "Add secret"

### 4️⃣ Enable GitHub Features

#### Enable necessary GitHub features:

1. **GitHub Actions**
   - Visit: Settings → Actions → General
   - ✅ Allow all actions and reusable workflows

2. **GitHub Copilot** (Optional)
   - Visit: Settings → Copilot
   - ✅ Enable for this repository

3. **Security Features**
   - Visit: Settings → Security & analysis
   - ✅ Dependency graph
   - ✅ Dependabot alerts
   - ✅ Dependabot security updates
   - ✅ Code scanning (via GitHub Actions)
   - ✅ Secret scanning

### 5️⃣ Test Configuration

#### Verify settings are working correctly:

1. **Create Test Branch**
   ```bash
   git checkout -b test/branch-protection
   git push origin test/branch-protection
   ```

2. **Try Direct Push to main** (should be rejected)
   ```bash
   git checkout main
   echo "test" >> test.txt
   git add test.txt
   git commit -m "Test direct push"
   git push origin main  # Should fail
   ```

3. **Create PR and Verify**
   - Create PR from test branch
   - Check if AI code review runs
   - Check if approval is required

### 📝 Documentation

- **CODEOWNERS**: Defines code owners, ensures @lynx009 must approve changes
- **CONTRIBUTING.md**: Contributor guide explaining contribution process
- **REPOSITORY_SETTINGS.md**: Repository settings documentation
- **Issue Templates**: Standardized Issue submission
- **PR Template**: Standardized Pull Request

---

## 常见问题 / FAQ

### Q: 如何允许新的协作者？
**A:** 访问 Settings → Manage access → Invite a collaborator

### Q: AI 代码审查需要付费吗？
**A:** 是的，需要 OpenAI API 密钥，根据使用量付费

### Q: 可以暂时禁用分支保护吗？
**A:** 管理员可以在 Settings → Branches 中编辑或删除保护规则

### Q: 如何更新工作流配置？
**A:** 编辑 `.github/workflows/` 中的 YAML 文件并提交 PR

---

## 支持 / Support

如有问题，请：
- 查看 [CONTRIBUTING.md](../CONTRIBUTING.md)
- 提交 [Issue](https://github.com/lynx009/ai-engineering-lab/issues)
- 联系仓库所有者 @lynx009
