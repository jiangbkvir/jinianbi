# 完整工作流程说明 - dev vs main 分支

> 更新时间: 2026-01-14
> 版本: 1.0

---

## 🎯 核心问题

**问题:** 现在的工作流是 dev 分支也会执行吗？还是合并到 main 分支执行？

**答案:** ✅ **只在合并到 main 分支时执行同步和 Release 创建**

---

## 📋 当前 Workflow 配置总览

### 1. 版本检查 Workflow

**文件:** `.github/workflows/check-version-conflict.yml`

**触发条件:**
```yaml
on:
  pull_request:
    types: [opened, synchronize]
    branches:
      - main  # 只检查到 main 的 PR
```

**执行时机:**
- ✅ 创建 PR 到 main 时
- ✅ 更新 PR 时（新的 commit push）
- ❌ dev 分支直接 push（不执行）
- ❌ 其他分支的 PR（不执行）

**作用:**
- 检查脚本文件是否修改
- 检查版本号是否更新
- 版本号相同 → 阻止合并

---

### 2. 同步和 Release Workflow

**文件:** `.github/workflows/sync-greasyfork.yml`

**触发条件:**
```yaml
on:
  push:
    branches:
      - main  # 只在 main 分支执行
    paths:
      - '纪念币预约辅助工具.user.js'  # 只在脚本文件变化时
```

**执行时机:**
- ✅ 合并 PR 到 main 后
- ✅ 直接 push 到 main（如果允许）
- ❌ dev 分支 push（不执行）
- ❌ 其他分支 push（不执行）
- ❌ 只修改其他文件（不执行）

**执行内容:**
1. 检查版本号是否更新
2. 版本更新 → 触发 Greasy Fork 同步
3. 版本更新 → 创建 GitHub Release

---

## 🔄 完整开发流程

### 阶段 1: 在 dev 分支开发

```bash
# 1. 切换到 dev 分支
git checkout dev

# 2. 修改代码
vim 纪念币预约辅助工具.user.js
# 更新 @version 2.2.0 → 2.2.1

# 3. 提交到 dev
git add .
git commit -m "feat: 新功能开发"
git push origin dev
```

**结果:**
- ❌ 不触发版本检查
- ❌ 不触发同步
- ❌ 不创建 Release
- ✅ 只是更新了 dev 分支代码

---

### 阶段 2: 创建 PR 到 main

```bash
# 创建 PR
gh pr create --base main --head dev --title "Release v2.2.1"
```

**触发:** ✅ `check-version-conflict` workflow

**执行流程:**
```
1. 检测脚本文件是否修改
   ├─ 未修改 → 跳过版本检查 → ✅ 允许合并
   └─ 已修改 → 继续
        ↓
2. 检查版本号
   ├─ dev: 2.2.1
   └─ main: 2.2.0
        ↓
3. 版本号对比
   ├─ 相同 → ❌ 检查失败 → 🔒 阻止合并
   └─ 不同 → ✅ 检查通过 → 允许合并
```

---

### 阶段 3: 合并 PR 到 main

```bash
# 合并 PR
gh pr merge --squash
```

**触发:** ✅ `sync-greasyfork` workflow

**执行流程:**
```
1. 检测到 push 到 main
   ↓
2. 检测到脚本文件变化
   ↓
3. 检查版本号是否更新
   ├─ 当前: 2.2.1
   └─ 上一个: 2.2.0
        ↓
4. 版本号已更新 → 执行同步
        ↓
   ┌────────┴────────┐
   ↓                 ↓
5a. Greasy Fork 同步  5b. 创建 GitHub Release
   ├─ 发送 Webhook      ├─ 标签: v2.2.1
   ├─ GF 拉取更新       ├─ Release Notes
   └─ 用户自动更新      └─ 附加脚本文件
```

---

## 📊 分支触发对比表

| 操作 | 分支 | 版本检查 | 同步 GF | 创建 Release |
|------|------|---------|---------|--------------|
| Push 到 dev | dev | ❌ | ❌ | ❌ |
| Push 到 main | main | ❌ | ✅* | ✅* |
| PR: dev→main (创建) | - | ✅ | ❌ | ❌ |
| PR: dev→main (合并) | main | ❌ | ✅* | ✅* |
| 只改 README → main | main | ❌ | ❌ | ❌ |

\* 仅当版本号更新时执行

---

## 💡 为什么这样设计？

### 1. 分离开发和生产环境

```
dev 分支 (开发环境)
├─ 频繁提交
├─ 可能有 bug
├─ 未完成的功能
└─ 不发布给用户

main 分支 (生产环境)
├─ 稳定版本
├─ 经过测试
├─ PR 审查通过
└─ ✅ 发布给用户
```

### 2. 避免重复同步

**❌ 如果 dev 也触发同步:**
```
开发者 push 到 dev
    ↓
同步到 Greasy Fork (第一次)
    ↓
用户收到更新 (可能有 bug)
    ↓
发现问题，修复后合并到 main
    ↓
再次同步到 Greasy Fork (第二次)
    ↓
用户又收到更新

问题：
1. 用户收到不稳定版本
2. 重复同步浪费资源
3. 版本混乱
```

**✅ 当前配置:**
```
开发者在 dev 开发
    ↓
测试完成，创建 PR
    ↓
版本检查通过
    ↓
合并到 main
    ↓
同步到 Greasy Fork (只一次)
    ↓
用户收到稳定版本

优势：
1. 用户只收到稳定版本
2. 只同步一次
3. 版本管理清晰
```

### 3. 强制 PR 审查流程

```
dev 直接 push → ❌ 不同步
         ↓
   必须创建 PR
         ↓
   版本检查 → 强制更新版本号
         ↓
   合并到 main
         ↓
   ✅ 才会同步

结果：
- 确保每次发布都经过审查
- 强制更新版本号
- 防止意外发布
```

---

## 🔧 特殊场景处理

### 场景 1: 紧急修复

如果需要紧急修复但不想走 PR 流程：

```bash
# ⚠️ 不推荐，但紧急情况可以用
git checkout main
git merge dev --no-ff
git push origin main

# 会触发同步，但跳过了 PR 检查
```

**建议:** 即使紧急修复也走 PR 流程，确保版本号检查。

---

### 场景 2: 测试版本

如果想在 dev 分支测试同步功能：

**方案 1: 创建测试 workflow**
```yaml
# .github/workflows/sync-greasyfork-dev.yml
on:
  push:
    branches:
      - dev
  workflow_dispatch:  # 手动触发
```

**方案 2: 手动触发同步**
- 在 Greasy Fork 网站手动点击同步按钮
- 临时测试，不影响主 workflow

---

### 场景 3: 只更新文档

```bash
# 只修改 README
vim README.md
git add README.md
git commit -m "docs: 更新文档"
git push origin main

# 不会触发同步（因为 paths 过滤）
```

**触发条件:**
- ✅ push 到 main
- ❌ 但没有修改 `.user.js` 文件
- 结果: 不触发同步 workflow

---

## 📈 推荐工作流程

### 日常开发

```bash
# 1. dev 分支开发
git checkout dev
# 修改代码，频繁提交
git add .
git commit -m "feat: 添加新功能"
git push origin dev

# 2. 功能完成，准备发布
# 更新版本号
vim 纪念币预约辅助工具.user.js
# @version 2.2.0 → 2.2.1

git add .
git commit -m "release: v2.2.1"
git push origin dev

# 3. 创建 PR
gh pr create --base main --head dev \
  --title "Release v2.2.1" \
  --body "新功能发布"

# 4. 等待检查通过
gh pr checks

# 5. 合并 PR
gh pr merge --squash

# 6. 自动触发
# - Greasy Fork 同步
# - GitHub Release 创建
```

### 版本发布检查清单

- [ ] 在 dev 分支完成开发
- [ ] 更新版本号
- [ ] 测试功能正常
- [ ] 创建 PR 到 main
- [ ] 版本检查通过（自动）
- [ ] 合并 PR
- [ ] 验证 Greasy Fork 同步成功
- [ ] 验证 GitHub Release 创建成功

---

## 🎯 总结

### 当前配置

| Workflow | 触发分支 | 触发事件 | 作用 |
|----------|---------|---------|------|
| `check-version-conflict` | PR → main | PR 创建/更新 | 版本检查 |
| `sync-greasyfork` | main | Push | 同步 + Release |

### 核心原则

1. **dev 分支** = 开发环境，不触发任何发布流程
2. **main 分支** = 生产环境，触发同步和发布
3. **PR 审查** = 强制版本检查，确保发布质量

### 优势

- ✅ 分离开发和生产环境
- ✅ 避免重复同步
- ✅ 强制 PR 审查流程
- ✅ 确保版本号正确更新
- ✅ 用户只收到稳定版本

---

**配置状态:** ✅ 最佳实践
**是否需要修改:** ❌ 当前配置已是最优解
