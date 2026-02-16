# .github Directory - Repository Configuration

[English](#english) | [中文](#中文)

---

## 中文

### 📋 目录内容

本目录包含 GitHub 仓库的配置文件、工作流程和模板。

### 🛡️ 分支保护机制

#### 1. 文档和配置文件

- **`CODEOWNERS`** - 定义代码所有者，要求 @lynx009 审批所有 PR
- **`settings.yml`** - 自动化配置文件（需要安装 Probot Settings App）
- **`REPOSITORY_SETTINGS.md`** - 详细的设置文档
- **`SETUP_GUIDE.md`** - 分步设置指南

#### 2. 自动化监控

**`workflows/branch-protection-monitor.yml`**
- 每日自动检查分支保护设置
- 验证是否禁用了强制推送和删除
- 如果发现配置问题，自动创建 Issue 提醒管理员

#### 3. 关键保护设置

要保护 main 分支免受强制推送和删除，**必须**在 GitHub 设置中配置：

1. 访问: Settings → Branches → Add branch protection rule
2. 分支名称模式: `main`
3. **关键设置**:
   - ❌ **Allow force pushes**: 必须**取消勾选** - 防止强制推送覆盖历史
   - ❌ **Allow deletions**: 必须**取消勾选** - 防止分支被删除

### ⚠️ 重要说明

> **`.github/` 目录中的文件是文档和模板**
> 
> 实际的分支保护只有在 GitHub 网页设置中配置后才会生效！
> 
> 文件的作用：
> - `settings.yml` - 可被 Probot Settings App 使用自动配置
> - `REPOSITORY_SETTINGS.md` - 文档说明需要什么设置
> - `branch-protection-monitor.yml` - 监控设置是否正确
> 
> 但最终保护必须通过 GitHub UI 设置！

### 🔍 如何验证保护是否启用

1. **手动检查**:
   - 访问: `https://github.com/lynx009/ai-engineering-lab/settings/branches`
   - 查看 main 分支是否有保护规则
   - 确认 "Allow force pushes" 和 "Allow deletions" 都未勾选

2. **自动检查**:
   - 查看 Actions → Branch Protection Monitor
   - 如果有问题，会自动创建 Issue

### 📁 文件清单

```
.github/
├── CODEOWNERS                        # 代码所有者定义
├── settings.yml                      # Probot Settings 配置
├── REPOSITORY_SETTINGS.md            # 设置文档
├── SETUP_GUIDE.md                    # 设置指南
├── README.md                         # 本文件
├── workflows/
│   ├── ai-code-review.yml           # AI 代码审查
│   ├── pr-validation.yml            # PR 验证
│   └── branch-protection-monitor.yml # 分支保护监控 🆕
├── ISSUE_TEMPLATE/
│   ├── bug_report.md
│   └── feature_request.md
└── PULL_REQUEST_TEMPLATE/
    └── pull_request_template.md
```

---

## English

### 📋 Directory Contents

This directory contains GitHub repository configuration files, workflows, and templates.

### 🛡️ Branch Protection Mechanisms

#### 1. Documentation and Configuration Files

- **`CODEOWNERS`** - Defines code owners, requires @lynx009 approval on all PRs
- **`settings.yml`** - Automated configuration file (requires Probot Settings App)
- **`REPOSITORY_SETTINGS.md`** - Detailed settings documentation
- **`SETUP_GUIDE.md`** - Step-by-step setup guide

#### 2. Automated Monitoring

**`workflows/branch-protection-monitor.yml`**
- Automatically checks branch protection settings daily
- Verifies force pushes and deletions are disabled
- Automatically creates Issues to alert admins if configuration problems detected

#### 3. Critical Protection Settings

To protect the main branch from force pushes and deletion, you **MUST** configure in GitHub settings:

1. Visit: Settings → Branches → Add branch protection rule
2. Branch name pattern: `main`
3. **Critical Settings**:
   - ❌ **Allow force pushes**: Must be **UNCHECKED** - Prevents force pushing history rewrites
   - ❌ **Allow deletions**: Must be **UNCHECKED** - Prevents branch deletion

### ⚠️ Important Notice

> **Files in `.github/` directory are documentation and templates**
> 
> Actual branch protection only takes effect when configured in GitHub web settings!
> 
> What the files do:
> - `settings.yml` - Can be used by Probot Settings App for auto-configuration
> - `REPOSITORY_SETTINGS.md` - Documents what settings are needed
> - `branch-protection-monitor.yml` - Monitors if settings are correct
> 
> But the final protection must be set through GitHub UI!

### 🔍 How to Verify Protection is Enabled

1. **Manual Check**:
   - Visit: `https://github.com/lynx009/ai-engineering-lab/settings/branches`
   - Check if main branch has protection rules
   - Confirm "Allow force pushes" and "Allow deletions" are both unchecked

2. **Automatic Check**:
   - View Actions → Branch Protection Monitor
   - If there are issues, it will automatically create an Issue

### 📁 File List

```
.github/
├── CODEOWNERS                        # Code owner definitions
├── settings.yml                      # Probot Settings configuration
├── REPOSITORY_SETTINGS.md            # Settings documentation
├── SETUP_GUIDE.md                    # Setup guide
├── README.md                         # This file
├── workflows/
│   ├── ai-code-review.yml           # AI code review
│   ├── pr-validation.yml            # PR validation
│   └── branch-protection-monitor.yml # Branch protection monitor 🆕
├── ISSUE_TEMPLATE/
│   ├── bug_report.md
│   └── feature_request.md
└── PULL_REQUEST_TEMPLATE/
    └── pull_request_template.md
```

---

## 🚨 Quick Start for Repository Owner

### To Enable Branch Protection:

1. **Go to Settings** → **Branches** → **Add branch protection rule**
2. **Branch pattern**: `main`
3. **Enable all protections** as documented in `SETUP_GUIDE.md`
4. **Critical**: Ensure these are **DISABLED**:
   - ❌ Allow force pushes
   - ❌ Allow deletions
5. **Click "Create"**

### To Enable Automated Configuration (Optional):

1. Install Probot Settings App: https://github.com/apps/settings
2. The app will automatically read `settings.yml` and apply configurations

### To Verify:

1. Run the Branch Protection Monitor workflow manually
2. Check if any Issues are created about configuration problems
3. If all is well, the workflow will show ✅ green status

---

For detailed instructions, see:
- [SETUP_GUIDE.md](SETUP_GUIDE.md) - Complete setup walkthrough
- [REPOSITORY_SETTINGS.md](REPOSITORY_SETTINGS.md) - All settings explained
