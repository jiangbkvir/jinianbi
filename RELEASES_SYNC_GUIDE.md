# GitHub Releases 与脚本平台同步说明

> 版本: 1.0
> 更新时间: 2026-01-14

---

## 🎯 功能概述

### 已实现功能

当脚本版本更新时，自动执行以下操作：

1. ✅ **检查版本号更新**
2. ✅ **触发 Greasy Fork Webhook 同步**
3. ✅ **自动创建 GitHub Release**
4. ✅ **生成 Release Notes**
5. ✅ **附加脚本文件到 Release**

### 工作流程

```
推送到 main 分支
        ↓
检测 .user.js 文件修改
        ↓
    版本号更新？
   ↙          ↘
 是            否
 ↓             ↓
执行同步     跳过同步
 ↓
1. Greasy Fork Webhook
2. 创建 GitHub Release
   ├─ 生成版本标签
   ├─ 生成 Release Notes
   └─ 附加脚本文件
```

---

## ❓ Releases 能否同步到脚本平台？

### Greasy Fork

**答案: ❌ 不直接支持从 GitHub Releases 同步**

#### Greasy Fork 支持的同步方式

| 方式 | 支持 | 说明 |
|------|------|------|
| **GitHub Webhook** | ✅ | 监听仓库 push 事件（当前使用） |
| **手动同步按钮** | ✅ | 在 Greasy Fork 网站手动点击 |
| **定时同步** | ✅ | 每天自动检查一次 |
| **GitHub Releases** | ❌ | 不支持 |
| **Git Tags** | ❌ | 不支持 |

#### Greasy Fork 同步机制

```
GitHub 仓库 push
        ↓
    Webhook 触发
        ↓
Greasy Fork 接收通知
        ↓
拉取最新的 .user.js 文件
        ↓
    解析元数据
        ↓
  更新脚本版本
```

**关键点：**
- Greasy Fork 直接从 GitHub 仓库的 **分支** 拉取文件
- 不会读取 GitHub Releases 的附件
- Webhook 监听的是 `push` 事件，不是 `release` 事件

---

## 🔄 当前配置详解

### Workflow: sync-greasyfork.yml

```yaml
on:
  push:
    branches:
      - main
    paths:
      - '纪念币预约辅助工具.user.js'

jobs:
  sync:
    steps:
      # 1. 检查版本号
      - name: 检查版本号是否更新
        # 比较当前版本 vs 上一个提交版本

      # 2. 同步到 Greasy Fork
      - name: 触发 Greasy Fork 同步
        if: 版本号已更新
        # 发送 Webhook 请求

      # 3. 创建 GitHub Release
      - name: 创建 GitHub Release
        if: 版本号已更新
        uses: softprops/action-gh-release@v1
        with:
          tag_name: v2.2.0
          files: 纪念币预约辅助工具.user.js
```

### 同步流程时序图

```
时间线：0秒 ────────→ 10秒 ────────→ 完成

开发者 push
    ↓
GitHub Actions 触发
    ↓
版本检查 (1-2秒)
    ↓
    ├─→ Greasy Fork Webhook (3-5秒)
    │        ↓
    │   Greasy Fork 拉取文件
    │        ↓
    │   Greasy Fork 更新完成
    │
    └─→ 创建 GitHub Release (2-3秒)
             ↓
        上传脚本文件
             ↓
        Release 创建完成
```

---

## 💡 为什么要创建 GitHub Releases？

### 虽然不能同步到 Greasy Fork，但 Releases 仍然有价值

#### 1. 版本归档

- 📦 完整的版本历史记录
- 🔖 每个版本都有独立的下载链接
- 📝 自动生成的 Release Notes

#### 2. 备用分发渠道

**场景 1: Greasy Fork 不可用**
```
用户访问 Greasy Fork → 网站故障/维护
            ↓
    查看 GitHub Releases
            ↓
    直接下载 .user.js 文件
            ↓
        手动安装
```

**场景 2: 用户不使用 Greasy Fork**
- 部分用户偏好直接从 GitHub 安装
- 企业内网环境无法访问 Greasy Fork
- Releases 提供了可靠的下载源

#### 3. 版本回退

```
用户安装了 v2.2.0 → 发现问题
            ↓
    访问 GitHub Releases
            ↓
    下载 v2.1.2 版本
            ↓
        回退安装
```

#### 4. SEO 和发现性

- GitHub Releases 可被搜索引擎索引
- 提高项目可见性
- 方便用户发现和下载

---

## 🚀 多渠道分发策略

### 推荐配置

```
主渠道: Greasy Fork
├─ 自动更新
├─ 用户评论
├─ 评分系统
└─ 安装统计

备用渠道: GitHub Releases
├─ 版本归档
├─ 直接下载
├─ 历史版本
└─ 离线安装
```

### 用户安装流程对比

| 方式 | Greasy Fork | GitHub Releases |
|------|------------|-----------------|
| **安装步骤** | 1. 点击安装 | 1. 下载文件<br>2. 拖入浏览器 |
| **自动更新** | ✅ 支持 | ❌ 需手动更新 |
| **版本选择** | ❌ 仅最新版 | ✅ 任意版本 |
| **网络要求** | 需访问 GF | 仅需 GitHub |
| **推荐程度** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

---

## 📋 Release Notes 内容

### 自动生成的内容

```markdown
## 🎉 版本 2.2.0

### 📝 更新内容
[从 Git 提交信息自动提取]

### 📦 安装方式

**Greasy Fork (推荐):**
https://greasyfork.org/zh-CN/scripts/521357

**直接安装:**
点击下方的 `纪念币预约辅助工具.user.js` 文件即可安装

### 🔗 相关链接
- [使用文档](https://github.com/jiangbkvir/jinianbi)
- [问题反馈](https://github.com/jiangbkvir/jinianbi/issues)

---
🤖 此版本已自动同步到 Greasy Fork
```

### 附件文件

每个 Release 自动附加：
- `纪念币预约辅助工具.user.js` - 脚本文件

用户可以直接点击下载并安装。

---

## 🔧 其他脚本平台支持

### OpenUserJS

**同步方式:** ❌ 不支持 GitHub Releases

**支持的方式:**
- Webhook (类似 Greasy Fork)
- 手动上传

### ScriptCat (脚本猫)

**同步方式:** ❌ 不支持 GitHub Releases

**支持的方式:**
- 手动上传
- 可能支持 Webhook (需确认)

### 总结

**没有主流脚本平台支持从 GitHub Releases 同步**

原因：
1. Releases 是 GitHub 特有功能
2. 脚本平台需要实时获取最新代码
3. Webhook + 分支文件是更直接的方式
4. Releases 更适合软件发布，不适合脚本同步

---

## ✅ 最佳实践建议

### 1. 主要渠道: Greasy Fork

配置 Webhook 自动同步：
```
✅ 已配置
✅ 版本更新时自动触发
✅ 用户自动获取更新
```

### 2. 备用渠道: GitHub Releases

自动创建 Release：
```
✅ 版本归档
✅ 直接下载链接
✅ 完整的版本历史
```

### 3. 多平台发布

如果需要覆盖更多平台：

| 平台 | 配置方式 |
|------|---------|
| Greasy Fork | ✅ 自动 (Webhook) |
| GitHub Releases | ✅ 自动 (Actions) |
| OpenUserJS | ⚠️ 手动上传 |
| ScriptCat | ⚠️ 手动上传 |

### 4. 在 README 中引导用户

```markdown
## 📦 安装

### 方式 1: Greasy Fork (推荐)
[点击安装](https://greasyfork.org/zh-CN/scripts/521357)
- ✅ 自动更新
- ✅ 安装统计
- ✅ 用户反馈

### 方式 2: GitHub Releases
[查看所有版本](https://github.com/jiangbkvir/jinianbi/releases)
- 📦 版本归档
- 🔙 版本回退
- 📥 离线安装
```

---

## 🎯 总结

### Releases 同步到脚本平台？

| 问题 | 答案 |
|------|------|
| Greasy Fork 支持 Releases 同步？ | ❌ 不支持 |
| OpenUserJS 支持 Releases 同步？ | ❌ 不支持 |
| 其他平台支持 Releases 同步？ | ❌ 都不支持 |

### Releases 的价值

虽然不能直接同步到脚本平台，但 GitHub Releases 仍然有重要价值：

1. ✅ **版本归档** - 完整的历史记录
2. ✅ **备用下载** - Greasy Fork 不可用时的备选
3. ✅ **版本管理** - 方便回退和对比
4. ✅ **提高可见性** - SEO 优化

### 当前配置已达最佳

```
Greasy Fork Webhook ←─┐
                       ├── 自动同步 ✅
GitHub Releases    ←───┘

用户可以：
1. 从 Greasy Fork 安装 (推荐) → 自动更新
2. 从 GitHub Releases 下载 (备用) → 手动更新
```

---

**最后建议:** 保持当前配置，无需额外同步工作。Greasy Fork Webhook 已经是最优解。

