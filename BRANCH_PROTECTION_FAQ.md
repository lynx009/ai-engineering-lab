# 分支保护问题解答 / Branch Protection Q&A

[中文](#中文) | [English](#english)

---

## 中文

### ❓ 问题：现在这套规则集可以保护main分支吗，不被强制推送和删除？

### ✅ 答案：可以，但需要正确配置！

这套规则集**提供了完整的保护机制**，但需要在 GitHub 设置中正确配置才能生效。

### 🛡️ 保护机制说明

#### 1. 文档层面（已完成）

我们提供了完整的文档和配置模板：

- ✅ **`.github/CODEOWNERS`** - 定义代码所有者
- ✅ **`.github/settings.yml`** - 自动化配置文件
- ✅ **`.github/REPOSITORY_SETTINGS.md`** - 详细设置文档
- ✅ **`.github/SETUP_GUIDE.md`** - 分步设置指南
- ✅ **`.github/README.md`** - 保护机制说明

这些文件明确标注了需要禁用：
- ❌ **Allow force pushes** (禁止强制推送)
- ❌ **Allow deletions** (禁止删除分支)

#### 2. 监控层面（已完成）

新增的 **`branch-protection-monitor.yml`** 工作流：

- 🔍 每天自动检查分支保护设置
- ⚠️ 如果发现以下问题，会自动创建 Issue 提醒：
  - 强制推送被允许
  - 分支删除被允许
  - 缺少必需的审查
  - 未启用线性历史
- ✅ 配置正确时自动关闭相关 Issue

#### 3. 执行层面（需要手动配置）

⚠️ **关键步骤** - 必须由仓库所有者在 GitHub 网页界面配置：

1. **访问**: `https://github.com/lynx009/ai-engineering-lab/settings/branches`

2. **添加分支保护规则**:
   - 点击 "Add branch protection rule"
   - Branch name pattern: `main`

3. **配置关键保护设置**:
   - ❌ **Allow force pushes**: 取消勾选 ⭐ **必须**
   - ❌ **Allow deletions**: 取消勾选 ⭐ **必须**
   - ✅ Require pull request reviews
   - ✅ Require review from Code Owners
   - ✅ Require status checks to pass
   - ✅ Require linear history
   - ✅ Restrict who can push (仅 lynx009)

4. **点击 "Create"** 保存设置

### 🚨 为什么需要手动配置？

GitHub 的分支保护是在**仓库设置层面**控制的，不能仅通过代码文件来强制执行。

- `.github/` 目录中的文件是**文档和配置模板**
- 实际保护必须通过 **GitHub 网页界面设置**
- 可选：安装 [Probot Settings App](https://github.com/apps/settings) 自动应用 `settings.yml`

### ✅ 如何验证保护已启用？

#### 方法 1: 手动检查
1. 访问 Settings → Branches
2. 查看是否有 `main` 分支保护规则
3. 确认 "Allow force pushes" 和 "Allow deletions" 都未勾选

#### 方法 2: 自动检查
1. 等待 `branch-protection-monitor` 工作流运行（每天自动）
2. 或手动触发：Actions → Branch Protection Monitor → Run workflow
3. 查看是否有警告 Issue 被创建

### 📝 保护效果

配置完成后：

| 操作 | 结果 |
|------|------|
| 直接推送到 main | ❌ 被拒绝 |
| 强制推送到 main | ❌ 被拒绝 |
| 删除 main 分支 | ❌ 被拒绝 |
| 未经审查合并 PR | ❌ 被拒绝 |
| 通过审查的 PR | ✅ 允许合并 |

### 🎯 总结

**规则集本身**：✅ 完整且正确
**当前状态**：⚠️ 需要在 GitHub 设置中激活
**最终效果**：✅ 配置后可完全保护 main 分支

请按照 `.github/SETUP_GUIDE.md` 中的步骤完成配置！

---

## English

### ❓ Question: Can this rule set protect the main branch from force pushes and deletion?

### ✅ Answer: Yes, but requires proper configuration!

This rule set **provides complete protection mechanisms**, but they need to be configured in GitHub settings to take effect.

### 🛡️ Protection Mechanisms Explained

#### 1. Documentation Level (Complete)

We provide comprehensive documentation and configuration templates:

- ✅ **`.github/CODEOWNERS`** - Defines code owners
- ✅ **`.github/settings.yml`** - Automated configuration file
- ✅ **`.github/REPOSITORY_SETTINGS.md`** - Detailed settings documentation
- ✅ **`.github/SETUP_GUIDE.md`** - Step-by-step setup guide
- ✅ **`.github/README.md`** - Protection mechanism explanation

These files clearly specify disabling:
- ❌ **Allow force pushes** (Prevent force pushing)
- ❌ **Allow deletions** (Prevent branch deletion)

#### 2. Monitoring Level (Complete)

New **`branch-protection-monitor.yml`** workflow:

- 🔍 Automatically checks branch protection settings daily
- ⚠️ Automatically creates Issues to alert if problems detected:
  - Force pushes are allowed
  - Branch deletions are allowed
  - Required reviews are missing
  - Linear history not enforced
- ✅ Automatically closes related Issues when configuration is correct

#### 3. Enforcement Level (Requires Manual Configuration)

⚠️ **Critical Step** - Must be configured by repository owner in GitHub web interface:

1. **Visit**: `https://github.com/lynx009/ai-engineering-lab/settings/branches`

2. **Add Branch Protection Rule**:
   - Click "Add branch protection rule"
   - Branch name pattern: `main`

3. **Configure Critical Protection Settings**:
   - ❌ **Allow force pushes**: Uncheck ⭐ **MUST**
   - ❌ **Allow deletions**: Uncheck ⭐ **MUST**
   - ✅ Require pull request reviews
   - ✅ Require review from Code Owners
   - ✅ Require status checks to pass
   - ✅ Require linear history
   - ✅ Restrict who can push (only lynx009)

4. **Click "Create"** to save settings

### 🚨 Why Manual Configuration Required?

GitHub's branch protection is controlled at the **repository settings level** and cannot be enforced solely through code files.

- Files in `.github/` directory are **documentation and configuration templates**
- Actual protection must be set through **GitHub web interface settings**
- Optional: Install [Probot Settings App](https://github.com/apps/settings) to auto-apply `settings.yml`

### ✅ How to Verify Protection is Enabled?

#### Method 1: Manual Check
1. Visit Settings → Branches
2. Check if `main` branch protection rule exists
3. Confirm "Allow force pushes" and "Allow deletions" are both unchecked

#### Method 2: Automatic Check
1. Wait for `branch-protection-monitor` workflow to run (daily automatic)
2. Or manually trigger: Actions → Branch Protection Monitor → Run workflow
3. Check if any warning Issues are created

### 📝 Protection Effects

After configuration:

| Action | Result |
|--------|--------|
| Direct push to main | ❌ Rejected |
| Force push to main | ❌ Rejected |
| Delete main branch | ❌ Rejected |
| Merge PR without review | ❌ Rejected |
| Merge reviewed PR | ✅ Allowed |

### 🎯 Summary

**Rule set itself**: ✅ Complete and correct
**Current state**: ⚠️ Needs activation in GitHub settings
**Final effect**: ✅ Can fully protect main branch after configuration

Please follow the steps in `.github/SETUP_GUIDE.md` to complete the configuration!

---

## Quick Reference Links

- [Setup Guide (SETUP_GUIDE.md)](.github/SETUP_GUIDE.md) - Detailed setup instructions
- [Repository Settings (REPOSITORY_SETTINGS.md)](.github/REPOSITORY_SETTINGS.md) - All settings explained
- [.github README](.github/README.md) - Protection mechanisms overview
- [GitHub Branch Protection Docs](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)
