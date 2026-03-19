# FitTrack PWA 部署指南

## 📁 文件清单
```
fittrack-pwa/
├── index.html      ← 主应用（已内置 IndexedDB 存储）
├── manifest.json   ← PWA 配置
├── sw.js           ← Service Worker（离线缓存）
├── icon-192.png    ← 应用图标
├── icon-512.png    ← 应用图标（大）
└── README.md       ← 本文件
```

## 🚀 部署到 GitHub Pages（5 分钟）

### 第一步：创建 GitHub 账号
如果没有：去 https://github.com 注册（免费）

### 第二步：创建仓库
1. 登录 GitHub → 点右上角 **+** → **New repository**
2. 仓库名填 `fittrack`（或任意名字）
3. 勾选 **Public**（GitHub Pages 免费版需要 Public）
4. 点 **Create repository**

### 第三步：上传文件
1. 在新仓库页面点 **uploading an existing file**
2. 把这 5 个文件全部拖进去（index.html, manifest.json, sw.js, icon-192.png, icon-512.png）
3. 点 **Commit changes**

### 第四步：开启 GitHub Pages
1. 进入仓库 → **Settings** → 左侧 **Pages**
2. Source 选 **Deploy from a branch**
3. Branch 选 **main** → 文件夹选 **/ (root)** → 点 **Save**
4. 等 1-2 分钟，页面顶部会出现：
   **Your site is live at https://你的用户名.github.io/fittrack/**

### 第五步：添加到手机桌面
**iPhone：**
1. 用 Safari 打开上面的链接
2. 点分享按钮 ↑ → **添加到主屏幕**
3. 确认名称 → **添加**

**Android：**
1. 用 Chrome 打开链接
2. 点菜单 ⋮ → **添加到主屏幕** 或 **安装应用**

## 💾 数据安全说明

### 数据存在哪里？
- 所有数据存储在你手机浏览器的 **IndexedDB** 中
- 这是浏览器的本地数据库，比 localStorage 更持久
- **没有任何服务器存储你的数据**，GitHub Pages 只托管代码文件

### 什么情况会丢数据？
- ❌ 清除浏览器所有数据/缓存（Safari → 设置 → 清除历史记录和网站数据）
- ❌ 卸载浏览器
- ❌ 恢复出厂设置
- ✅ 正常关闭/重启 app → 数据不会丢
- ✅ 断网使用 → 数据不会丢
- ✅ 手机重启 → 数据不会丢

### 如何防止丢失？
**定期备份！** 进入 设置 → 数据备份 → 导出备份
- 会下载一个 `.json` 文件，包含你所有的运动记录、体重、档案
- 建议保存到 iCloud Drive / 百度网盘 / 微信文件传输助手

### 如何在另一台设备上恢复？
1. 在新设备上用浏览器打开同一个网址
2. 添加到桌面
3. 进入 设置 → 数据备份 → 导入恢复 → 选择之前的 `.json` 文件
4. 自动恢复所有数据

## ⚠️ 关于多设备同步
目前**不支持自动实时同步**。原因：
- 实时同步需要后端服务器，会产生费用和隐私风险
- 当前方案是纯本地存储，最大程度保护隐私

**替代方案：** 通过备份文件手动同步
1. 设备 A：导出备份 → 通过 AirDrop/微信/网盘 发送
2. 设备 B：收到文件 → 导入恢复

## 🔒 隐私保障
- ✅ 所有健身数据、体重、月经周期等只存在你的设备上
- ✅ GitHub Pages 是纯静态文件托管，不运行任何后端代码
- ✅ 唯一的网络请求是 AI 建议功能（调用 Anthropic API），且不传输你的身份信息
- ✅ 断网时 AI 建议会使用本地 fallback 算法，其余功能完全正常

## 🔄 如何更新应用
如果后续有新版本：
1. 把新文件上传到同一个 GitHub 仓库（覆盖旧文件）
2. GitHub Pages 会自动更新
3. 手机上打开 app 时会自动获取新版本
4. **你的数据不会受影响**（数据在 IndexedDB，代码在 GitHub）
