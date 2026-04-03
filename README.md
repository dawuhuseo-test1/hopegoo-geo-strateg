# HopeGoo GEO 战略中心 — 部署指南

## 🚀 快速部署到 GitHub Pages（5分钟）

### 第一步：创建 GitHub 仓库
1. 打开 https://github.com/new
2. 仓库名填写：`hopegoo-geo-strategy`（或任意名称）
3. 选择 **Public**（公开）
4. 勾选 **Add a README file**
5. 点击 **Create repository**

### 第二步：上传文件
1. 在仓库页面点击 **Add file** → **Upload files**
2. 把 `index.html` 文件拖拽上传
3. 点击 **Commit changes**

### 第三步：启用 GitHub Pages
1. 进入仓库 **Settings**（设置）
2. 左侧菜单找到 **Pages**
3. Source 选择 **Deploy from a branch**
4. Branch 选择 **main**，文件夹选择 **/ (root)**
5. 点击 **Save**

### 第四步：获取链接
- 等待1-2分钟后，页面顶部会出现：
  `Your site is live at https://你的用户名.github.io/hopegoo-geo-strategy/`
- 这个链接可以直接分享给团队，**无需登录**即可访问

---

## 🔄 启用团队数据同步（可选）

默认情况下，数据存储在每个人的浏览器本地（localStorage）。
如果你需要团队成员之间**实时同步**（A领取任务后B能立即看到），
需要配置 Firebase：

### 配置 Firebase Realtime Database
1. 打开 https://console.firebase.google.com
2. 点击 **创建项目**（免费）
3. 进入项目后，左侧菜单点 **Build** → **Realtime Database**
4. 点 **创建数据库** → 选择区域 → **以测试模式启动**
5. 复制数据库 URL（类似：`https://your-project-default-rtdb.firebaseio.com`）

### 修改 index.html
打开 `index.html`，找到以下注释部分，取消注释并填入你的 URL：

```html
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/8.10.1/firebase-database.js"></script>
<script>
  firebase.initializeApp({
    databaseURL: "https://YOUR-PROJECT.firebaseio.com"  // ← 替换这里
  });
  window._fbDb = firebase.database();
</script>
```

然后重新上传到 GitHub，团队数据就会实时同步了。

---

## 📁 文件说明

| 文件 | 说明 |
|------|------|
| `index.html` | 完整的战略中心网页（单文件，含全部功能） |
| `README.md` | 本部署指南 |

## ⚠️ 注意事项

- GitHub Pages 部署可能需要 1-2 分钟才会生效
- 首次访问如果显示 404，等几分钟再试
- Firebase 测试模式默认30天后过期，届时需要去 Firebase 控制台更新安全规则
- 如果不配置 Firebase，每个人的数据独立存储在各自浏览器中
