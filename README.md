# 宇宙级 3D 卡牌抽取

基于 Three.js + GSAP + MediaPipe 的宇宙主题 3D 卡牌抽取网页应用。支持手势识别、稀有度系统、粒子特效等丰富交互。

## 功能特性

### 抽卡系统
- **5 级稀有度**：普通 (★) / 稀有 (★★) / 史诗 (★★★) / 传说 (★★★★) / 神话 (★★★★★)
- **加权概率**：普通 40% → 稀有 30% → 史诗 18% → 传说 9% → 神话 3%
- **20 张宇宙主题卡牌**：星尘、流星、星云、超新星、银河核心、创世之光等
- **彩虹卡模式**：可切换彩虹主题卡面

### 3D 视觉效果
- **Three.js WebGL 渲染**：3D 卡牌在星空场景中展示
- **Bloom 后处理**：UnrealBloomPass 发光效果
- **卡牌翻转动画**：弹性翻转揭示 (GSAP Elastic ease)
- **粒子爆炸特效**：抽卡时喷射稀有度颜色粒子，带重力下落
- **轨道卡牌阵列**：已抽取卡牌在 3D 轨道中排列展示
- **星空视差**：鼠标/触摸移动时星空背景偏移

### 交互方式
- **手势识别**：MediaPipe Hands 手势操控 (需 HTTPS)
  - 捏合：抽卡
  - 横向挥手：切卡
  - 保持开掌：连抽
- **触控/鼠标**：点击抽卡、拖拽切卡、滚轮切卡
- **键盘**：空格/D 抽卡、B 连抽、← → 切卡
- **连击系统**：快速连续抽卡触发 COMBO 连击显示

### 音效系统
- Web Audio API 合成音效，无需外部文件
- 稀有度越高音调越高
- 传说/神话级有和弦音效

### UI 特性
- **全屏闪光**：史诗+级别抽到时屏幕光效
- **可折叠面板**：移动端自动收起，点击展开
- **抽卡记录**：最近 5 条记录，按稀有度颜色显示
- **HUD 轨道信息**：底部显示当前卡牌和轨道导航
- **加载进度条**：带超时兜底的加载动画

## 快速开始

### 本地直接打开
```bash
# 双击 index.html 即可在桌面浏览器中运行
open index.html
```

### 局域网手机测试 (摄像头功能需要 HTTPS)

```bash
# 1. 生成自签名证书
openssl req -x509 -newkey rsa:2048 -keyout key.pem -out cert.pem -days 365 -nodes -subj "/CN=YOUR_IP"

# 2. 启动 HTTPS 服务器
node serve.js

# 3. 手机访问 https://YOUR_IP:8443
```

### Android Chrome 免 HTTPS 测试
1. 手机 Chrome 打开 `chrome://flags/#unsafely-treat-insecure-origin-as-secure`
2. 添加 `http://YOUR_IP:8080`
3. 设为 Enabled 并重启 Chrome

## 技术栈

| 技术 | 用途 |
|------|------|
| [Three.js](https://threejs.org/) r128 | 3D 渲染、Bloom 后处理 |
| [GSAP](https://greensock.com/gsap/) 3.12 | 动画系统、时间轴 |
| [MediaPipe Hands](https://google.github.io/mediapipe/) | 手势识别 |
| Web Audio API | 合成音效 |
| Canvas 2D | 卡牌纹理生成 |

## 项目结构

```
index.html          # 主页面 (单文件，所有代码内联)
serve.js            # HTTPS 开发服务器 (Node.js)
key.pem / cert.pem  # 自签名 SSL 证书 (gitignore)
```

## 操作说明

| 操作 | 桌面 | 移动端 |
|------|------|--------|
| 抽卡 | 点击画面 / 空格键 / D 键 | 点击画面 / 手势捏合 |
| 切卡 | 左右方向键 / 滚轮 / 拖拽 | 左右拖拽 / 手势挥手 |
| 连抽 | B 键 / 连抽按钮 | 手势开掌保持 |
| 手势模式 | 点击"唤醒手势抽卡" | 需 HTTPS 环境 |

## 注意事项

- 手势识别需要 HTTPS 或 localhost 环境（浏览器安全策略）
- 移动端 MediaPipe 会自动降低模型复杂度以保证性能
- CDN 资源 (Three.js / GSAP / MediaPipe) 需要网络连接
- 卡牌上限 36 张，超出自动移除最旧的
