# 🎄 头像圣诞树（手势控制 · 照片拼成树）

一个纯前端的交互式 3D 圣诞树网页：**上传照片，照片会拼成一棵圣诞树；用摄像头手势隔空控制**——握拳收拢、张开炸开、捏合随机放大照片。

基于开源项目 [electronicminer/gesture-Christmas_tree-3d_with_photo](https://github.com/electronicminer/gesture-Christmas_tree-3d_with_photo)（MIT 协议）改造。

## 文件说明

```
christmas-tree-avatar/
├── index.html   # 全部代码（单文件，方便改）
└── README.md    # 本说明
```

- 依赖全部走 CDN（Three.js 0.160 + MediaPipe tasks-vision 0.10.3），无需安装任何东西。
- 手势模型 `hand_landmarker.task` 由 MediaPipe 自动从 Google 服务器下载。

## 电脑上本地运行

```bash
cd christmas-tree-avatar
python -m http.server 8080
# 或者：npx serve .
```

然后浏览器打开 **http://localhost:8080**

> ⚠️ 摄像头（getUserMedia）只在 **localhost 或 HTTPS** 下可用。直接用文件方式打开（file://）会拿不到摄像头。

## 玩法

1. 点右上角「📷 开启手势」，允许摄像头权限，把手放到摄像头前。
2. 点「选择照片」（或「选择文件夹」）上传头像/照片，照片会自动铺满圣诞树。

| 手势 | 效果 |
| --- | --- |
| ✊ 握拳 | 粒子收拢、拼成圣诞树 |
| ✋ 张开手掌 | 树炸开成星云 |
| 🤏 拇指+食指捏合 | 随机放大一张照片 |
| 👆 拖动屏幕 | 旋转视角 |

## 部署成链接

### GitHub Pages（推荐，免费长期）
1. 在 GitHub 新建仓库，把 `index.html` 传上去。
2. Settings → Pages → Source 选 `main` 分支根目录 → Save。
3. 得到 `https://你的用户名.github.io/仓库名/`，手机电脑都能开。

### Vercel / Netlify（更快）
- Vercel：导入 GitHub 仓库（或直接拖这个文件夹到 vercel.com）→ Deploy。
- Netlify：拖整个文件夹到 app.netlify.com/drop 即可。

## 用 DSH 修改：改哪里

代码里关键位置都有中文注释，直接对 `index.html` 说“改 XX”即可：

| 想改什么 | 位置 |
| --- | --- |
| 树的密度/高度/半径、粒子数量、雪量 | `CONFIG` 的 `particles`（文件内搜「可调参数」） |
| 照片叶子密度（现在每张照片约铺 150 片） | `rebuildPhotoLeaves` 里的 `150` |
| 手势灵敏度 | `processGestures`（搜「手势判定」），阈值 `1.5 / 0.35 / 1.7` |
| 颜色/黑金配色 | `CONFIG.colors` 和 `setupLights` |
| 标题、按钮文案 | `<h1>` 和 `.control-btn` 区域 |
