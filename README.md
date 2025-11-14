# 💉 疫苗RCT志愿者发送统计系统

[English](#english) | [中文](#chinese)

---

<a name="chinese"></a>

## 📋 简介

一个优雅的Web应用，用于统计和管理疫苗RCT实验中63名志愿者的邮件发送情况。通过粘贴群接龙数据，系统自动分析哪些志愿者已完成发送任务，哪些尚未发送，并实时生成可视化统计报告。

## ✨ 功能特点

### 🎯 核心功能
- **📊 智能数据分析** - 自动解析群接龙格式数据
- **👥 内置志愿者数据库** - 预置63名志愿者完整名单
- **🔍 状态精准识别** - 自动区分"无退订"、"退订未发送"等状态
- **📈 实时可视化** - 动态图表展示统计结果
- **🎨 分类筛选** - 支持按状态筛选查看详细列表
- **💾 数据导出** - 一键导出CSV格式统计报告

### 🛡️ 数据处理
- ✅ 自动过滤非人名内容（如"#接龙"标记）
- ✅ 智能识别多种状态格式
- ✅ 支持序号自动清理
- ✅ 空格/逗号分隔符兼容

### 📊 统计维度
- **已发送** 📤 - 在接龙中出现的志愿者
- **未发送** ❌ - 数据库中有但接龙未提及的志愿者
- **无退订** 💚 - 成功发送且受众无退订
- **退订未发送** 🚫 - 因受众退订而未能发送

## 🚀 快速开始

### 方式一：直接使用
1. 📂 在浏览器中打开 `index.html` 文件
2. 📋 将群接龙数据粘贴到输入框
3. 🔮 点击"开始分析"按钮
4. 📊 查看统计结果

### 方式二：本地服务器
```bash
# 使用Python启动本地服务器
python -m http.server 8000

# 或使用Node.js
npx serve
```

然后在浏览器访问 `http://localhost:8000`

## 📝 使用说明

### 数据格式示例

```
#接龙
1. 郑嘉诚 已发送,退订的未发送
2. 尹力慧 已发送 无退订
3. 郭雅森 已发送 退订未发送
4. 战友欣 已发送,退订的未发送
...
```

### 操作步骤

1. **📥 输入数据**
   - 点击"粘贴"按钮或直接使用 `Ctrl+V` 粘贴群接龙数据
   - 或点击"加载示例接龙"测试功能

2. **🔍 分析数据**
   - 点击"开始分析"按钮
   - 系统自动识别姓名和状态信息

3. **📊 查看结果**
   - 顶部卡片显示四类统计数据
   - 圆环图直观展示已发送/未发送比例
   - 详细列表显示每个志愿者的具体状态

4. **🎯 筛选查看**
   - 使用下拉菜单按状态筛选
   - 底部显示所有未发送志愿者名单

5. **💾 导出数据**
   - 点击"导出"按钮生成CSV文件
   - 包含所有63名志愿者的完整统计信息

## 🎨 界面预览

### 主要区域
- **左侧** 📝 数据输入区 + 志愿者名单
- **右侧** 📊 统计概览 + 详细列表
- **底部** ⚠️ 未发送人员警示卡片

### 统计卡片
- 🔵 已发送 - 蓝色主题
- 🔴 未发送 - 红色主题
- 🟢 无退订 - 绿色主题
- 🟠 退订未发送 - 橙色主题

## 🛠️ 技术栈

- **HTML5** - 页面结构
- **Tailwind CSS** - 现代化UI样式
- **Vanilla JavaScript** - 核心逻辑（无框架依赖）
- **Chart.js** - 数据可视化
- **Font Awesome** - 图标库

## 📦 内置志愿者数据库

系统内置63名志愿者完整名单：

```
郑嘉诚、尹力慧、郭雅森、战友欣、郭虔、田馨、王旭、闫政婷、
王琦、郭晓林、李怡菡、刘丞哲、何瑞、柯尚冶、黄俊森、张紫钰、
姚盼玉、张晓歌、黄曼轩、钟士秦、全文海、张玉娇、朱郑昊、施云峰、
杨昊、赖伟丽、王晓妍、石松、谈潭、乔浩森、张钧玮、李晨曦、
董边昕、郭湘、张译心、彭瑶、邱阅、阳文佩、刘晨桐、张绩伟、
周梦竺、马晴、于江媛、王伊、刘钥珊、许梦晗、陈文凯、刘一、
谷正、吴佳琪、赵卓异、孙嘉晨、陈颖、马浩钧、李雅霏、张英特、
高飞、罗立心、陈政、葛晨曦、曹宇晴、王维秀、郭佳
```

## 🎯 核心算法

### 状态识别逻辑

```javascript
// 关键：先检查"无退订"（更具体），再检查"退订"（更宽泛）
if (statusText.includes('无退订')) {
    detailStatus = 'no-unsubscribe';
} else if (statusText.includes('退订')) {
    detailStatus = 'unsubscribed';
}
```

### 数据过滤

```javascript
// 自动过滤非人名内容
lines.filter(line => {
    if (!line) return false;
    if (line.includes('#接龙') || line.includes('#')) return false;
    return true;
});
```

## ⚙️ 配置说明

### 修改志愿者名单

在 `index.html` 中找到 `this.database` 数组，修改志愿者名单：

```javascript
this.database = [
    "新志愿者1", "新志愿者2", "新志愿者3", 
    // ... 添加更多志愿者
];
```

### 自定义主题颜色

在 `tailwind.config` 中修改配色方案：

```javascript
colors: {
    primary: '#165DFF',    // 主色调
    secondary: '#36D399',  // 辅助色
    warning: '#FFAB00',    // 警告色
    danger: '#F87272',     // 危险色
    success: '#10B981',    // 成功色
}
```

## 📱 浏览器兼容性

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## 🔒 隐私说明

- ✅ 所有数据处理在本地完成
- ✅ 不上传任何信息到服务器
- ✅ 不使用Cookies或本地存储
- ✅ 完全离线可用

## 🤝 贡献指南

欢迎提交问题和改进建议！

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证

## 🙏 致谢

感谢所有参与疫苗RCT实验的志愿者！

---

<a name="english"></a>

# 💉 Vaccine RCT Volunteer Tracking System

## 📋 Introduction

An elegant web application for tracking and managing email delivery status of 63 volunteers in a vaccine RCT experiment. Simply paste group chain message data, and the system automatically analyzes which volunteers have completed their tasks and generates real-time visual statistical reports.

## ✨ Features

### 🎯 Core Functions
- **📊 Intelligent Data Analysis** - Auto-parse group chain message format
- **👥 Built-in Volunteer Database** - Pre-loaded list of 63 volunteers
- **🔍 Precise Status Recognition** - Auto-distinguish "No Unsubscribe", "Unsubscribed" etc.
- **📈 Real-time Visualization** - Dynamic charts for statistics
- **🎨 Category Filtering** - Filter by status for detailed view
- **💾 Data Export** - One-click CSV export

### 🛡️ Data Processing
- ✅ Auto-filter non-name content (e.g., "#接龙" markers)
- ✅ Smart recognition of multiple status formats
- ✅ Automatic number prefix cleaning
- ✅ Space/comma delimiter compatible

### 📊 Statistical Dimensions
- **Sent** 📤 - Volunteers appearing in the chain message
- **Not Sent** ❌ - Volunteers in database but not in chain
- **No Unsubscribe** 💚 - Successfully sent, no unsubscribes
- **Unsubscribed** 🚫 - Not sent due to recipient unsubscribe

## 🚀 Quick Start

### Method 1: Direct Use
1. 📂 Open `index.html` in browser
2. 📋 Paste chain message data into input box
3. 🔮 Click "Start Analysis" button
4. 📊 View statistics

### Method 2: Local Server
```bash
# Start local server with Python
python -m http.server 8000

# Or use Node.js
npx serve
```

Then visit `http://localhost:8000` in browser

## 📝 Usage Guide

### Data Format Example

```
#接龙
1. 郑嘉诚 已发送,退订的未发送
2. 尹力慧 已发送 无退订
3. 郭雅森 已发送 退订未发送
4. 战友欣 已发送,退订的未发送
...
```

### Operation Steps

1. **📥 Input Data**
   - Click "Paste" button or use `Ctrl+V`
   - Or click "Load Sample" to test

2. **🔍 Analyze Data**
   - Click "Start Analysis" button
   - System auto-recognizes names and status

3. **📊 View Results**
   - Top cards show 4 categories of statistics
   - Doughnut chart visualizes sent/not sent ratio
   - Detailed list shows each volunteer's status

4. **🎯 Filter View**
   - Use dropdown to filter by status
   - Bottom section shows all volunteers not sent

5. **💾 Export Data**
   - Click "Export" to generate CSV
   - Includes complete stats for all 63 volunteers

## 🎨 Interface Preview

### Main Areas
- **Left** 📝 Data input + Volunteer list
- **Right** 📊 Statistics overview + Detailed list
- **Bottom** ⚠️ Not sent volunteers alert card

### Statistics Cards
- 🔵 Sent - Blue theme
- 🔴 Not Sent - Red theme
- 🟢 No Unsubscribe - Green theme
- 🟠 Unsubscribed - Orange theme

## 🛠️ Tech Stack

- **HTML5** - Page structure
- **Tailwind CSS** - Modern UI styling
- **Vanilla JavaScript** - Core logic (no framework)
- **Chart.js** - Data visualization
- **Font Awesome** - Icon library

## 📦 Built-in Volunteer Database

System includes complete list of 63 volunteers:

```
郑嘉诚, 尹力慧, 郭雅森, 战友欣, 郭虔, 田馨, 王旭, 闫政婷,
王琦, 郭晓林, 李怡菡, 刘丞哲, 何瑞, 柯尚冶, 黄俊森, 张紫钰,
姚盼玉, 张晓歌, 黄曼轩, 钟士秦, 全文海, 张玉娇, 朱郑昊, 施云峰,
杨昊, 赖伟丽, 王晓妍, 石松, 谈潭, 乔浩森, 张钧玮, 李晨曦,
董边昕, 郭湘, 张译心, 彭瑶, 邱阅, 阳文佩, 刘晨桐, 张绩伟,
周梦竺, 马晴, 于江媛, 王伊, 刘钥珊, 许梦晗, 陈文凯, 刘一,
谷正, 吴佳琪, 赵卓异, 孙嘉晨, 陈颖, 马浩钧, 李雅霏, 张英特,
高飞, 罗立心, 陈政, 葛晨曦, 曹宇晴, 王维秀, 郭佳
```

## 🎯 Core Algorithm

### Status Recognition Logic

```javascript
// Key: Check "无退订" (more specific) before "退订" (more general)
if (statusText.includes('无退订')) {
    detailStatus = 'no-unsubscribe';
} else if (statusText.includes('退订')) {
    detailStatus = 'unsubscribed';
}
```

### Data Filtering

```javascript
// Auto-filter non-name content
lines.filter(line => {
    if (!line) return false;
    if (line.includes('#接龙') || line.includes('#')) return false;
    return true;
});
```

## ⚙️ Configuration

### Modify Volunteer List

Find `this.database` array in `index.html` and update:

```javascript
this.database = [
    "New Volunteer 1", "New Volunteer 2", "New Volunteer 3", 
    // ... add more volunteers
];
```

### Customize Theme Colors

Modify color scheme in `tailwind.config`:

```javascript
colors: {
    primary: '#165DFF',    // Primary color
    secondary: '#36D399',  // Secondary color
    warning: '#FFAB00',    // Warning color
    danger: '#F87272',     // Danger color
    success: '#10B981',    // Success color
}
```

## 📱 Browser Compatibility

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## 🔒 Privacy Notice

- ✅ All data processing is local
- ✅ No data uploaded to servers
- ✅ No cookies or local storage used
- ✅ Fully offline capable

## 🤝 Contributing

Welcome to submit issues and improvement suggestions!

1. Fork the project
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License

This project is licensed under the MIT License

## 🙏 Acknowledgments

Thanks to all volunteers participating in the vaccine RCT experiment!
For questions or suggestions, please open an issue on GitHub.

Made with ❤️ for vaccine research volunteers
