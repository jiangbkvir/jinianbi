# 纪念币预约辅助工具

> 一个强大的 Tampermonkey 用户脚本，帮助您快速预约纪念币，支持多家银行官网。

[![Version](https://img.shields.io/badge/version-2.0-blue.svg)](https://github.com/your-repo)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![GreasyFork](https://img.shields.io/badge/GreasyFork-Download-orange.svg)](https://greasyfork.org/scripts/521357)

## 📖 介绍

纪念币预约辅助工具是一款专为纪念币预约场景设计的浏览器扩展脚本。通过提前录入预约人信息、一键智能填充表单、数据批量管理等功能，大幅提升预约效率，让您的纪念币预约体验更加流畅。

### ✨ 核心特性

- 🚀 **智能填充** - 一键自动填充姓名、身份证、手机号、网点、数量等信息
- 💾 **数据管理** - 支持数据导入/导出 JSON 格式，方便备份和迁移
- 🔄 **自动保存** - 所有数据实时保存到本地，无需担心丢失
- ✅ **格式验证** - 自动验证身份证（15/18位）和手机号（11位）格式
- 🎯 **数据去重** - 智能识别并去除重复数据（基于姓名+身份证+手机号）
- 🎨 **拖拽浮动** - 可拖拽浮动窗口，支持折叠/展开，不遮挡页面内容
- 📋 **快速复制** - 每个字段独立复制按钮，灵活使用

## 🏦 支持的银行

理论上支持所有银行的纪念币预约系统，已测试兼容的银行包括：

| 银行 | 移动端 | PC端 |
|------|--------|------|
| **工商银行** | [预约入口](https://static.jnb.icbc.com.cn/ICBC/ICBCCOIN/roccentry.html) | [预约入口](https://static.jnb.icbc.com.cn/ICBC/ICBCCOIN/roccentryPC.html) |
| **建设银行** | [预约入口](https://m2.ccb.com/cn/jnb/mobilev3/subject/index.html) | [预约入口](https://sinfo2.ccb.com/cn/jnb/subject/index.html) |
| **交通银行** | [预约入口](https://apply.95559.com.cn/personbank/commemorativeOrderCoins/index.html#/order) | - |
| **华夏银行** | [预约入口](https://mcm.hxb.com.cn/m/coin/#/coinAct?publish_channel_id=003) | - |
| **浦发银行** | [预约入口](https://wap.spdb.com.cn/mspmk-cli-coinrsv/CoinHome) | - |
| **邮政储蓄银行** | [预约入口](https://wap.psbc.com/mobilebank/commemorativeCoinMenu.do) | [预约入口](https://pbank.psbc.com/perbank/commemorativeCoinMake.gate) |
| **农业银行** | [预约入口](https://coin.abchina.com.cn/static/mbank/index.html#/) | [预约入口](https://eapply.abchina.com/coin/) |
| **中国银行** | [预约入口](https://mbas.cmcoins.boc.cn/CoinSeller/coinNew/index.html) | [预约入口](https://cmcoins.boc.cn/BOC15_CoinSeller/welcome.html) |
| **徽商银行** | [预约入口](https://wxyh.hsbank.cc:10443/GATEWAYPZB-SERVER/index.html) | - |
| **晋商银行** | [预约入口](https://upbp.startbank.com.cn/rvcc/JNB/index.html) | - |
| **陕西农信** | - | [预约入口](https://www.96262.com/xh/jnb/index.shtml) |

> 💡 **提示**：点击链接即可直接跳转到对应银行的预约页面。建议使用电脑端浏览器配合手机端同时预约，提高成功率。

## 📦 安装

### 1. 安装 Tampermonkey

首先需要在浏览器中安装 Tampermonkey 扩展：

- **Chrome/Edge**: [Chrome Web Store](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo)
- **Firefox**: [Firefox Add-ons](https://addons.mozilla.org/firefox/addon/tampermonkey/)
- **Safari**: [App Store](https://apps.apple.com/app/tampermonkey/id1482490089)

### 2. 安装脚本

**方式一：从 GreasyFork 安装（推荐）**

1. 访问 [GreasyFork 脚本页面](https://greasyfork.org/scripts/521357)
2. 点击 "安装此脚本" 按钮
3. 确认安装

**方式二：手动安装**

1. 打开 Tampermonkey 管理面板
2. 点击 "+" 创建新脚本
3. 复制 [index.js](index.js) 的内容
4. 粘贴到编辑器中
5. 按 `Ctrl+S` (Mac: `Cmd+S`) 保存

## 🎯 使用指南

### 基础操作

#### 1. 添加预约人信息

1. 打开支持的银行预约页面
2. 点击页面右侧的浮动窗口
3. 点击 **"+ 添加"** 按钮
4. 填写预约人信息：
   - **姓名** (必填)
   - **身份证** (必填，支持15位或18位)
   - **手机号** (必填，11位)
   - **网点** (可选)
   - **数量** (可选)
5. 点击任意输入框外完成保存

#### 2. 一键填充表单

1. 确保已添加预约人信息
2. 点击预约人姓名按钮
3. 脚本会自动填充页面的预约表单：
   - ✅ 姓名
   - ✅ 身份证号
   - ✅ 手机号
   - ✅ 网点（延迟600ms）
   - ✅ 数量（延迟900ms）

#### 3. 复制单个字段

每个字段旁边都有 **"复制"** 按钮，点击即可复制该字段内容到剪贴板。

#### 4. 删除预约人

1. 展开预约人卡片
2. 点击右上角的 **"×"** 按钮
3. 确认删除

### 数据管理

#### 导出数据

1. 点击 **"导出"** 按钮
2. 自动下载 `form_data.json` 文件
3. 文件包含所有预约人信息（不包含内部索引字段）

#### 导入数据

1. 点击 **"导入"** 按钮
2. 选择之前导出的 JSON 文件
3. 脚本会自动：
   - ✅ 过滤无效数据（三个主字段全为空）
   - ✅ 去除重复数据（基于姓名+身份证+手机号）
   - ✅ 统计格式错误数量
   - ✅ 显示导入结果

#### 数据格式

导出的 JSON 文件格式：

```json
[
  {
    "name": "张三",
    "idCard": "110101199001011234",
    "mobile": "13800138001",
    "branch": "工商银行北京朝阳支行",
    "amount": "20"
  }
]
```

## 🔧 功能详解

### 格式验证

脚本会自动验证输入格式，并通过背景颜色提示：

| 颜色 | 含义 |
|------|------|
| 🟩 白色 | 格式正确 |
| 🟧 橙色 | 必填字段为空 |
| 🟥 红色 | 格式错误 |

**身份证验证规则**：
- ✅ 15位纯数字：`110101900101123`
- ✅ 18位数字：`110101199001011234`
- ✅ 18位+X：`11010119900101123X`
- ✅ 18位+x：`11010119900101123x`

**手机号验证规则**：
- ✅ 11位，1开头，第二位3-9：`13800138000`

### 数据去重

去重逻辑：**姓名 + 身份证 + 手机号** 三个字段完全相同才视为重复。

## 📊 技术架构

### 技术栈

- **语言**: JavaScript (ES6+)
- **平台**: Tampermonkey / Greasemonkey
- **存储**: GM_setValue / GM_getValue
- **API**: Clipboard API, FileReader API

### 代码结构

```
index.js (2,017 行)
├── 配置模块
│   ├── ELEMENT_SELECTORS (表单选择器)
│   ├── STYLES (样式配置)
│   └── bankObj (银行地址)
├── 工具模块
│   ├── UIUtils (UI工具)
│   ├── ValidationUtils (验证工具)
│   ├── DataManager (数据管理)
│   └── FormCard (卡片组件)
├── 核心功能
│   ├── fillForm (填充表单)
│   ├── findElement (查找元素)
│   ├── findElementSmart (智能查找)
│   └── Message (消息提示)
└── 主程序
    ├── 数据导入/导出
    ├── 卡片管理
    └── 事件监听
```

## 🐛 常见问题

### 1. 脚本无法运行？

**可能原因**：
- Tampermonkey 未正确安装
- 脚本未正确安装
- 网页不在支持列表中

**解决方法**：
1. 检查 Tampermonkey 图标是否显示脚本正在运行
2. 刷新页面
3. 查看浏览器控制台是否有错误

### 2. 填充失败？

**可能原因**：
- 页面表单元素选择器不匹配
- 页面加载未完成

**解决方法**：
1. 等待页面完全加载后再填充
2. 使用单个字段复制功能

### 3. 数据丢失？

**解决方法**：
1. 定期导出数据进行备份
2. 从备份文件导入恢复

## 📝 更新日志

<details open>
<summary><b>查看所有版本 (4个版本)</b></summary>

---

<details>
<summary>v2.1 (2026-01-09) - 体验优化</summary>

- ✨ **Tab 键导航优化**
  - 优化 Tab 键导航，现在按 Tab 键会在输入框之间切换，不会跳到复制按钮
  - 为复制、折叠、删除按钮添加 `tabindex="-1"`，提升表单填写体验
  - 优化键盘操作流畅度

</details>

---

<details>
<summary>v2.0 (2026-01-09) - 重大更新</summary>

- ✨ **代码重构**
  - 重构代码架构，模块化设计
  - 修复所有作用域问题
  - 更新 @include 规则，支持更多银行
  - 优化描述信息

- 🎨 **功能优化**
  - 添加输入防抖，减少保存频率
  - 保留用户输入，验证失败不清空
  - 完善测试报告

</details>

---

<details>
<summary>v1.4 - 功能增强</summary>

- 添加索引管理功能
- 优化卡片序号显示
- 修复数据导入问题

</details>

---

<details>
<summary>v1.0 - 初始版本</summary>

- 初始版本发布
- 基础的添加、编辑、复制功能
- 数据导入导出

</details>

---

</details>

## 🔐 隐私与安全

- ✅ 所有数据仅保存在本地浏览器中
- ✅ 不上传任何个人信息到服务器
- ✅ 开源代码，可自行审查
- ✅ 使用 MIT 许可证

## 📄 许可证

MIT License

---

<div align="center">

**如果这个工具对您有帮助，请给个 ⭐Star 支持一下！**

Made with ❤️ by [jiangbkvir](https://github.com/jiangbkvir)

</div>
