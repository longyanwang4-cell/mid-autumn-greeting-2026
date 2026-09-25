# 月满中秋 · 课题组祝福网页

一个**单文件**的中秋祝福网页（`index.html`，零依赖、无需构建），为课题组中秋祝福定制：
夜空明月 + 水面倒影 + 诗词逐字入场 + **祝福语文字烟花**（「科研顺利」「论文高中」「数据漂亮」…在夜空中绽放）+ 孔明灯 + 交互放烟花。

## 创意来源（GitHub 开源项目复现与融合）

| 参考项目 | 借鉴的创意 | 原始实现位置 |
|---|---|---|
| [shaochidianhehe-glitch/zhongqiu](https://github.com/shaochidianhehe-glitch/zhongqiu)（花好月圆·中秋贺卡） | Canvas 多层视差夜景：月面环形山、云层、山峦、水面月光倒影、逐字诗词入场、印章盖章动画 | `reference/zhongqiu.html` |
| [aiyoudiao/Qxy-Mid-Autumn-Festival-Fireworks](https://github.com/aiyoudiao/Qxy-Mid-Autumn-Festival-Fireworks)（中秋烟花） | **文字烟花**：把祝福语画到离屏画布上，采样像素点作为粒子目标，烟花炸开后汇聚成文字 | `reference/firework.js`、`reference/night-sky.js` |
| [nuo-huang/mid-autumn-wishes](https://github.com/nuo-huang/mid-autumn-wishes)（月夜来信·孔明灯贺卡） | 全屏孔明灯从水面升起、灯焰闪烁与水面倒影 | `reference/nuo-huang-kongminglantern.html` |

本项目在上述技术方案基础上重新实现并融合，增加了课题组专属祝福语文案、开场编排、
纯净录屏模式、URL 参数自定义等能力。

## 本地运行（三选一）

1. **直接双击** `index.html`（所有资源内联，双击即可完整运行）；
2. 或起个本地服务器（推荐，地址更好看）：
   ```bash
   cd "E:\zcode project\中秋快乐"
   python -m http.server 8000
   # 浏览器打开 http://127.0.0.1:8000
   ```
3. 或 VS Code 安装 Live Server 插件后右键 Open with Live Server。

## 自定义祝福语

打开 `index.html`，找到脚本开头的 `CONFIG`：

```js
var CONFIG = {
  group: '',   // 课题组名称，如 '智能计算课题组' → 顶部显示 “智能计算课题组 · 中秋敬贺”
  from:  '',   // 落款，如 '智能计算课题组全体师生' → 右下角替换“敬颂秋祺”
  wishes: [ '中秋快乐', '花好月圆', '科研顺利', '论文高中', ... ]  // 文字烟花轮播的祝福语
};
```

也可以**不改代码**，用网址参数临时覆盖（发给不同的人可以定制不同署名）：

```
index.html?group=XX课题组&from=XX课题组全体师生&wish=中秋快乐,论文高中,毕业顺利
```

## 声音

- **真实音效（已内置）**：烟花升空与炸裂使用**真实录音**（来源 [Mixkit](https://mixkit.co)，免费授权、无需署名），文件为 `sfx-launch.mp3`（升空哨声）、`sfx-burst.mp3` 与 `sfx-burst2.mp3`（两种炸裂随机轮换，播放时轻微变速，每次听感不完全一样）。文件缺失时自动静默，不影响页面。
- **背景音乐（可选）**：把任意 mp3 命名为 `bgm.mp3` 放到 `index.html` 同目录，首次点击/按键后自动循环播放（音量已压低）。免版权古风曲可在 pixabay music、爱给网等找；**公开发布**时注意曲子授权，发群里随意。
- **想换音效**：用同名 mp3 替换那三个文件即可（升空声建议选 2~4 秒的哨声/嗖声类素材）。
- **浏览器限制**：声音要等第一次点击/按键才出声（安全策略），首次交互自动解锁。
- **静音控制**：右上角 🔊 按钮 / 快捷键 `M` / 网址加 `&mute`；选择会记住（localStorage）。

## 录屏建议（发群里）

1. 浏览器按 `F11` 全屏，分辨率建议 1920×1080；
2. 按 `H`（或点右上角“纯净模式”）隐藏右上角按钮，画面更干净；
3. 点击页面任意处触发「重播」即可从头开始录制，整个开场编排约 15 秒（诗词 → 标题停留数秒 → 标题隐入月色），之后进入赏月烟花模式：每 7~9 秒一朵文字烟花在高空绽放；期间可手动点击夜空放烟花、点水面或点「🏮 放一盏灯」放孔明灯；
4. 录制 40~60 秒可以覆盖 4~5 句祝福语的轮放；期间可手动点击夜空放烟花、点水面或点「🏮 放一盏灯」放孔明灯；
5. 背景音乐建议录屏后在剪辑软件里加（浏览器自动播放音乐限制多，故未内置）。

**快捷键**：`空格` 随机放烟花 · `L` 放孔明灯 · `H` 纯净模式 · `M` 音乐开关 · `R` 重播

## 部署到服务器（可选）

整个网站就是**一个 `index.html`**，任何静态托管都能放：

**方式 A：GitHub Pages（免费、最快）**
```bash
# 在 GitHub 新建仓库后：
git init && git add index.html README.md
git commit -m "中秋祝福网页"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
# 仓库 Settings → Pages → Branch 选 main / root → 得到
# https://<用户名>.github.io/<仓库名>/
```

**方式 B：自己的服务器（nginx）**
```bash
scp index.html user@your-server:/var/www/mid-autumn/
# nginx 配置：
# location /mid-autumn/ { alias /var/www/mid-autumn/; }
```

**方式 C：其他静态托管** —— Vercel / Netlify / 云对象存储(COS/OSS) 静态网站，拖入 `index.html` 即可。

部署后把链接（可带 `?group=...&from=...` 参数）直接发到课题组群里，手机打开效果已适配。

## 目录说明

```
中秋快乐/
├── index.html                  # 主页面
├── sfx-launch.mp3              # 真实录音音效：烟花升空哨声（Mixkit 免费授权）
├── sfx-burst.mp3               # 真实录音音效：炸裂（与下面一条随机轮换）
├── sfx-burst2.mp3              # 真实录音音效：炸裂 2
├── bgm.mp3                     # （可选）自己放的背景音乐，无此文件不影响运行
├── README.md                   # 本说明
└── reference/                  # 调研的 GitHub 参考项目源码（仅本地存档，不入仓库、运行不需要）
    ├── zhongqiu.html
    ├── fireworks-main.js / night-sky.js / firework.js / firework-particle.js
    └── nuo-huang-kongminglantern.html
```

## 已验证

- Windows + Chrome/Edge 双击直接打开 ✅
- 开场编排：星空→明月→山水→诗词→标题→祝福语→印章→标题隐入月色→高空文字烟花 ✅
- 文字烟花成形、普通烟花、孔明灯、流星、萤火虫、桂花瓣 ✅
- 手机竖屏（390×844）适配 ✅
- 真实音效（加载 / 首次交互解锁 / 静音记忆 / 文件缺失容错）与 BGM 机制 ✅
- `prefers-reduced-motion` 下自动降级为静态画面 ✅

> 提示：改过 `index.html` 后浏览器可能用缓存的旧版，本地看效果请按 `Ctrl+F5` 强制刷新。
