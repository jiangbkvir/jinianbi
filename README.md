# 纪念币预约辅助工具

> 一个强大的 Tampermonkey 用户脚本，帮助您快速预约纪念币，支持多家银行官网。

[![Version](https://img.shields.io/badge/version-2.2.8-blue.svg)](https://github.com/jiangbkvir/jinianbi)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![GreasyFork](https://img.shields.io/badge/GreasyFork-Install-orange.svg)](https://greasyfork.org/zh-CN/scripts/521357-%E7%BA%AA%E5%BF%B5%E5%B8%81%E9%A2%84%E7%BA%A6%E8%BE%85%E5%8A%A9%E5%B7%A5%E5%85%B7)

## 📖 介绍

纪念币预约辅助工具是一款专为纪念币预约场景设计的浏览器扩展脚本。通过提前录入预约人信息、一键智能填充表单、数据批量管理等功能，大幅提升预约效率，让您的纪念币预约体验更加流畅。
## ✅ 已完成功能

- [x] 基础数据管理（增删改查）
- [x] 数据导入导出
- [x] 格式验证
- [x] 自动填充表单
- [x] 拖拽浮窗
- [x] 数据去重
- [x] 快速复制
- [x] 折叠展开
- [x] 自动保存
- [ ] 自动填充网点

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

### 🧪 测试预约页面

**想要测试脚本功能？** 我们提供了模拟的银行预约页面供您测试：

👉 **[访问测试页面](https://jiangbkvir.github.io/jinianbi/)**

- ✅ 包含多个银行的模拟预约页面
- ✅ 无需等待真实预约开始
- ✅ 安全测试脚本功能
- ✅ 熟悉操作流程

## 📦 安装

> 🌐 **Greasy Fork 页面**: [https://greasyfork.org/zh-CN/scripts/521357-纪念币预约辅助工具](https://greasyfork.org/zh-CN/scripts/521357-%E7%BA%AA%E5%BF%B5%E5%B8%81%E9%A2%84%E7%BA%A6%E8%BE%85%E5%8A%A9%E5%B7%A5%E5%85%B7)

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

<details>
<summary><strong>📝 基础操作</strong></summary>

### 1. 添加预约人信息

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

### 2. 一键填充表单

1. 确保已添加预约人信息
2. 点击预约人姓名按钮
3. 脚本会自动填充页面的预约表单：
   - ✅ 姓名
   - ✅ 身份证号
   - ✅ 手机号
   - ✅ 网点（延迟600ms）
   - ✅ 数量（延迟900ms）

### 3. 复制单个字段

每个字段旁边都有 **"复制"** 按钮，点击即可复制该字段内容到剪贴板。

### 4. 删除预约人

1. 展开预约人卡片
2. 点击右上角的 **"×"** 按钮
3. 确认删除

</details>

<details>
<summary><strong>💾 数据管理</strong></summary>

### 导出数据

1. 点击 **"导出"** 按钮
2. 自动下载 `form_data.json` 文件
3. 文件包含所有预约人信息（不包含内部索引字段）

### 导入数据

1. 点击 **"导入"** 按钮
2. 选择之前导出的 JSON 文件
3. 脚本会自动：
   - ✅ 过滤无效数据（三个主字段全为空）
   - ✅ 去除重复数据（基于姓名+身份证+手机号）
   - ✅ 统计格式错误数量
   - ✅ 显示导入结果

### 数据格式

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

</details>

## 🎯 使用指南

<details>
<summary><strong>🔧 功能详解</strong></summary>

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

</details>

<details>
<summary><strong>🐛 常见问题</strong></summary>

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

</details>
## 🔐 隐私与安全

- ✅ 所有数据仅保存在本地浏览器中
- ✅ 不上传任何个人信息到服务器
- ✅ 开源代码，可自行审查
- ✅ 使用 MIT 许可证

<details>
<summary><strong>⚠️ 免责声明</strong></summary>

- **预约成功不确定性**：本工具仅为辅助工具，不保证预约成功率。预约成功与否取决于银行系统、网络状况、库存等多个因素。
- **数据安全责任**：虽然数据仅保存在本地，但用户应定期备份重要数据。脚本因系统错误、浏览器崩溃等导致的数据丢失，作者不承担责任。
- **适用条款变化**：各银行的预约规则可能随时变化，导致脚本失效，建议定期检查脚本更新。
- **用户责任**：用户应确保预约信息真实有效，由虚假信息导致的后果自行承担。

</details>

<details>
<summary><strong>📧 反馈与报告</strong></summary>

### 反馈模板

如遇到问题或有功能建议，请按以下模板提交 Issue：

```markdown
## 问题类型
- [ ] Bug 报告
- [ ] 功能建议
- [ ] 文档改进
- [ ] 其他

## 描述
简要描述您遇到的问题或建议

## 复现步骤（仅适用于 Bug）
1. 
2. 
3. 

## 环境信息
- 浏览器：Chrome / Firefox / Safari / Edge
- 脚本版本：
- 银行网站：

## 附件（可选）
💡 **建议附加截图或录屏**，以便更快速地定位问题
```

### 正确示例 ✅

```markdown
## 问题类型
- [x] Bug 报告

## 描述
在建设银行移动端，点击填充按钮时，手机号字段无法正常填充

## 复现步骤
1. 打开建设银行预约页面
2. 添加预约人信息（包含手机号）
3. 点击姓名按钮填充
4. 发现手机号字段没有被填入

## 环境信息
- 浏览器：Chrome 120
- 脚本版本：2.2.0
- 银行网站：建设银行移动端
- 页面地址：https://m2.ccb.com/cn/jnb/mobilev3/subject/index.html

## 附件
[附上填充前后的截图]
```

### 错误示例 ❌

```markdown
## 问题类型
- [x] Bug 报告

## 描述
不能用

## 复现步骤
不知道

## 实际结果
坏了

## 环境信息
浏览器：Chrome
```

</details>

## 📄 许可证

MIT License

---

<div align="center">

**如果这个工具对您有帮助，请给个 ⭐Star 支持一下！**

Made with ❤️ by [jiangbkvir](https://github.com/jiangbkvir)

</div>
