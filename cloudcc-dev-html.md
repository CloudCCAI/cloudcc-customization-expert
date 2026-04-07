---
name: cloudcc-dev-html
description: 指导在 CloudCC 相关仓库中编写单个 HTML 入口页：推荐 Tailwind（tailwindcss-browser）、Alpine.js、ECharts（BootCDN）、可使用 window.$CCDK。用户提到单页 HTML、html/index、BootCDN、Tailwind、Alpine、ECharts、CCDK、$CCDK 时使用。
---

# CloudCC 单 HTML 页面开发规范

版本信息见同目录 [config.json](config.json)。

## 1. 技能用途：创建单个 HTML 页面

- 本技能用于在项目中编写**单个 HTML 入口文件**（通常为 **`html/index.html`**），在 CloudCC 内嵌或单独打开，与 `plugins/` 等业务源码区分存放。
- 静态依赖（样式、脚本、字体等）**优先使用线上绝对地址**（`https://...`）引入；**公有云**推荐 [BootCDN](https://www.bootcdn.cn/) 等中国大陆可稳定访问的源；**私有云 / 内网**可将所需文件下载后上传到组织静态资源，再改为静态资源 URL。
- 平台业务接口与模块说明以 **cloudcc-dev-skill**（`cloudcc doc <module>`）为准；本技能不替代平台开发指南。

## 2. 页面推荐的样式与交互库

以下为独立页**推荐**组合（通过 BootCDN 固定版本，升级时改 URL 中版本号；私有云按上一节改链）。

**样式：Tailwind CSS（tailwindcss-browser，浏览器端编译）**

```html
<script src="https://cdn.bootcdn.net/ajax/libs/tailwindcss-browser/4.1.13/index.global.min.js"></script>
```

**交互：Alpine.js v3（CDN 构建，使用 `defer`，放在 `head`；与 Tailwind 同页时 Tailwind 在前、Alpine 在后）**

```html
<script defer src="https://cdn.bootcdn.net/ajax/libs/alpinejs/3.15.0/cdn.min.js"></script>
```

**图表：ECharts（按需引入；与 Tailwind、Alpine 同页时，建议放在二者之后，在初始化图表的脚本之前加载）**

```html
<script src="https://cdn.bootcdn.net/ajax/libs/echarts/6.0.0/echarts.min.js"></script>
```

## 3. 页面可使用 CCDK

- 在 CloudCC 运行环境（自定义页面、内嵌 HTML 等）中，可通过 **`window.$CCDK`** 使用平台提供的 **CCDK** 能力；脚本应通过该入口调用，不依赖未文档化的其它全局名。
- 在浏览器中直接打开本地文件时通常**没有** `$CCDK`，须做存在性判断或区分环境，避免报错。
- CCDK 具体 API 以平台文档及 **cloudcc-dev-skill** 中相关说明为准。
