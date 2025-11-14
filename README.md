# RCT Mail Tracker - 项目结构说明

## 文件结构
```
rct-mail-tracker/
├── index.html           # 主应用程序文件
├── README.md            # 项目说明文档（中英文）
```

## 主要文件说明

### 1. index.html
- 包含完整的HTML、CSS和JavaScript代码
- 使用Tailwind CSS进行样式设计
- 集成Chart.js进行数据可视化
- 包含所有交互功能和业务逻辑

### 2. README.md
- 详细的中英文项目说明
- 功能介绍和使用指南
- 技术特性和开发指南
- 贡献指南和许可证信息

### 3. LICENSE
- MIT开源许可证
- 允许自由使用、修改和分发

## 技术栈
- **前端框架**: HTML5 + Tailwind CSS v3 + JavaScript ES6+
- **图表库**: Chart.js 4.4.8
- **图标库**: Font Awesome 4.7.0
- **存储方案**: localStorage本地存储

## 部署方式
1. **静态部署**: 直接部署index.html文件
2. **本地使用**: 双击打开index.html文件
3. **服务器部署**: 上传到任何Web服务器

## 浏览器兼容性
- Chrome 88+
- Firefox 85+
- Safari 14+
- Edge 88+
- 其他现代浏览器

## 数据安全
- 所有数据存储在用户本地浏览器
- 不涉及服务器端数据传输
- 支持数据导出和备份
