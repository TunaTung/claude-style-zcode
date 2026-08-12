# Claude Style ZCode · 浅色皮肤包

给 [Dream Work Theme](https://github.com/xxxhh336/dream-work-theme) 用的 ZCode 浅色主题包：Claude 官方色系（珊瑚橙 + 品牌蓝 + 暖白层级）。非 Anthropic 官方产品，不修改官方安装包 / `app.asar` / WindowsApps。

包含两个版本：

| 版本 | 目录 | 特点 |
| --- | --- | --- |
| **Claude Eva Official**（明日香版） | 根目录 | 动漫少女背景 + 透明消息，氛围感强 |
| **Claude Eva Clean**（纯净版） | `clean/` | 细腻暖色渐变背景 + 透明消息，更克制 |

**纯净版（Claude Eva Clean）效果：**

![纯净版实际界面预览](docs/clean.png)

**明日香版（Claude Eva Official）效果：**

![明日香版实际界面预览](docs/asuka.png)

> 预览图为真实 ZCode 界面截图（浅色模式），仅作展示。

## 依赖

- [Dream Work Theme](https://github.com/xxxhh336/dream-work-theme)（CDP 注入换肤工具，Apache-2.0）
- ZCode 桌面端，且已在 ZCode「设置 → 外观」切换到浅色模式

> ⚠️ **本主题需要 generic 应用的 `theme.css` 注入能力**（输入框圆角、消息透明、侧边栏指示条、背景图透出）。上游原版对 ZCode 这类 generic 应用只注入自动生成的通用兜底皮肤，**不读取 `theme.css`**——直接用上游原版只能得到基础四色配色，没有组件级样式。
>
> 上游补丁见 [xxxhh336/dream-work-theme#1](https://github.com/xxxhh336/dream-work-theme/pull/1)（open，未合并）。**在补丁合并前，请使用下方「方式 A」的打包版，或「方式 B」的 fork 分支。**

## 安装

> 主题放进 Dream Work Theme 的**用户主题目录**即可被识别。主题目录不会自动创建，需要手动新建 `themes` 文件夹。各平台位置见下表：

| 平台 | 用户主题目录（需手动新建 `themes` 文件夹） |
| --- | --- |
| **macOS** | `~/Library/Application Support/dream-work-theme/themes/` |
| **Windows** | `%APPDATA%\dream-work-theme\themes\`（即 `C:\Users\<用户名>\AppData\Roaming\dream-work-theme\themes\`） |
| **Linux** | `~/.config/dream-work-theme/themes/` |

### 第一步：找到用户主题目录

**macOS**（Finder 默认隐藏 `Library`，用下面的方法直达）：

1. 打开 Finder，按 `Cmd + Shift + G`（前往文件夹）
2. 粘贴并回车：`~/Library/Application Support/dream-work-theme/`
3. 在该目录下手动新建 `themes` 文件夹

**Windows**：文件资源管理器地址栏粘贴 `%APPDATA%\dream-work-theme\`，回车后新建 `themes` 文件夹。

### 第二步：放入主题

**明日香版**：把 `theme.json`、`theme.css`、`hero.webp` 三个文件放进

```
.../dream-work-theme/themes/claude-eva-official/
```

**纯净版**：把本仓库 `clean/` 目录里的三个文件放进

```
.../dream-work-theme/themes/claude-eva-official-clean/
```

> 目录结构必须是 `themes/<主题名>/theme.json` 这样的层级，不要把文件直接散在 `themes/` 下，也不要套多余一层。

### 第三步：启动注入

**方式 A（推荐，Windows）：下载 fork 打包版**

从 [TunaTung/dream-work-theme Releases](https://github.com/TunaTung/dream-work-theme/releases) 下载最新的 `Dream-Work-Theme-*-win-x64.exe`（已内置 generic 应用 `theme.css` 注入补丁），安装后：

1. 启动 Dream Work Theme
2. 选择 ZCode
3. 选择主题 `claude-eva-official`（明日香版）或 `claude-eva-official-clean`（纯净版）
4. 点击「应用主题」

> fork 的 Release 会自动跟随上游同步并叠加本补丁；`theme.css` 生效后，输入框圆角、消息透明、侧边栏指示条均可见。

**方式 B（开发者 / 其他平台）：clone fork 分支运行源码**

```bash
git clone --branch feat/generic-theme-css-injection https://github.com/TunaTung/dream-work-theme
cd dream-work-theme
pnpm install
```

然后启动注入：

```bash
# 明日香版
npx electron . --launch=zcode:claude-eva-official

# 纯净版
npx electron . --launch=zcode:claude-eva-official-clean
```

> 本主题为 ZCode（generic-work 应用）提供了精细的组件级样式（输入框圆角、消息透明、侧边栏指示条等），需要 Dream Work Theme 支持 generic 应用的 `theme.css` 注入（见上方「依赖」与「上游说明」）。

## 文件结构

```
.
├── theme.json       # 明日香版主题声明（Claude 色系 palette）
├── theme.css        # 明日香版组件级样式（composer / message / sidebar / 微交互）
├── hero.webp        # 明日香版背景图（动漫少女，2848×1600）
├── clean/           # 纯净版（渐变背景）
│   ├── theme.json
│   ├── theme.css
│   └── hero.webp
├── docs/clean.png     # 纯净版效果图
└── docs/asuka.png     # 明日香版效果图
```

## 主题信息

- `id`：`claude-eva-official`（明日香版）/ `claude-eva-official-clean`（纯净版）
- 外观：`light`
- 支持：ZCode（`apps.zcode.compat: true`）
- 能力：`background` / `safe-css`

### 配色（Claude 官方 `data-theme=claude` light 变量转译）

| 键 | 色值 | 用途 |
| --- | --- | --- |
| `accent` | `#D97757` | 珊瑚橙主强调（按钮 / 指示条 / 输入框描边） |
| `secondary` | `#2E82DA` | 品牌蓝（链接 / hover 点缀） |
| `surface` | `#FAF9F5` | 暖白兜底底色 |
| `text` | `#211F1C` | 暖黑正文 |

### 组件细节

- 输入框：珊瑚橙圆角描边（伪元素实现，规避 sticky 合成下 `border-radius` 渲染异常），底色与顶部栏一致
- 消息容器：全透明，文字直接落在背景上
- 侧边栏：任务行珊瑚左指示条、hover 微光、功能区按钮蓝色 hover
- 微交互：图标位移 2px / 按钮按压 0.98 / 气泡 hover 珊瑚边

## 素材来源与权利声明

背景图（`hero.webp`，明日香版）基于 Claude EVA 主题素材包为基底，经 AI 再生成，公开再分发 / 商用前请自行确认素材、肖像与商标权利。背景不代表 Anthropic / Claude 官方视觉或背书。纯净版背景为程序生成的渐变图，无第三方素材。

## 上游说明

- 本项目基于 [Dream Work Theme](https://github.com/xxxhh336/dream-work-theme)（Apache-2.0）开发，主题格式与代码参考其通用写法（`themes/<id>/theme.json` + `theme.css` + hero）。
- ZCode 属于 generic-work 应用：Dream Work Theme 原版对 generic 应用只注入自动生成的通用兜底皮肤，不读取 `theme.css`。本主题的组件级样式需要上游支持 generic 应用的 `theme.css` 注入，对应的上游补丁见 [PR 链接](https://github.com/xxxhh336/dream-work-theme/pull/1)（`readThemeCss` / blob 修复 / 注入后自动退出）。
- **补丁尚未被上游合并**：合并前，Windows 用户请使用 [TunaTung/dream-work-theme](https://github.com/TunaTung/dream-work-theme) 的 Release 打包版（自动同步上游 + 叠加补丁）；其他平台或开发者可 clone 其 `feat/generic-theme-css-injection` 分支。上游合并后本主题将完全兼容官方原版。

## 许可

本主题包代码与声明文件采用 [MIT License](LICENSE)。背景图素材按上方的权利声明处理，请自行确认再分发权利。
