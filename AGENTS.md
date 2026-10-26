# AGENTS.md — 项目规则

> 本文件是 `D:/vscodehtml`（王梓杨的《高级网页设计》课堂实践）的项目规则，后续所有工作都必须遵守。
> 规则来源：opencode 教程「六）设置项目规则」、用户后续口头规则、以及从 TRAE 项目迁移的 Naming rules（`yl_` → `wzy_`）。

## 一、命名规则（Naming rules）

### 1. 命名前缀

所有 JS 变量名、CSS 类名、id 名称必须以 `wzy_` 开头。

```html
<div class="wzy_box" id="wzy_main-nav"></div>
```

```js
var wzy_index = 0;
```

### 2. 页面注释

每新建一个 `.html` 页面，都要在顶部加注释，必须写全四项：**姓名、建立时间、使用的大模型、功能名称**。

```html
<!-- 姓名：王梓杨，建立时间：2026-10-26 13:41，使用模型：DeepSeek-V4.1-Flash，功能名称：页面主题 - 一句话说明 -->
```

- 位置：`<!DOCTYPE html>` 之后、`<html>` 之前
- 建立时间：该页面创建的时间，格式 `YYYY-MM-DD HH:MM`
- 使用模型：实际生成该页面的大模型名称，不要省略、不要留空
- 功能名称：先写页面主题，再用 ` - ` 接一句话说明这个页面做什么

## 二、提示词规则

### 3. 提示词留痕

每次任务**执行之前**，先把提示词写入项目根目录 `wang prompt.md`：

- 采用**追加**方式，**不覆盖**已有内容
- 每条记录必须包含 **时间、使用的模型、提示词内容** 三项

### 4. 提示词不在网页里展示

提示词**只**写在 `wang prompt.md`。禁止往任何网页（`index.html` 或 `x-x` 页面）里放提示词原文、`PROMPT ·` 板块或复制按钮。

## 三、收录规则

### 5. x-x 系列一律并入 index

后续所有 `x-x` 系列页面，一律**按照 `index.html` 原有格式**收录进 `index.html`。
「原有格式」= 上传到 index 时使用的既有写法（无前缀的 `.card` 等类名），沿用即可，不要另创命名风格。

收录时需同步的位置：

1. 头部注释与 `<meta name="description">`：章节范围「第 2~N 章」与页面清单
2. 主视觉 lede：章节范围、页面清单、页面总数
3. idcard 芯片的「范围」
4. stats 的「课堂实践作品」数量（收录总数由 JS 自动算）
5. 「这次整合做了什么」note 追加本次条目
6. works 板块的 `sec-head` 标题与 `hint` 页面数，新增章节 `group` 与卡片
7. 卡片本体：`data-key` 检索词、`num` 编号、描述、路径、标签、大小与日期
8. 「其他页面」板块的 `idx` 编号整体顺延
9. 使用说明「目录结构一览」追加条目；新增素材目录也要写
10. 页脚「本目录 N 个课堂作品 + 其他 M 个已收录页面」

> ⚠️ `idx` 是纯数字行，逐条替换会连锁冲突。改编号时把 `old_string` 写成「编号行 + 紧随的 `<b>标题</b>` 两行」，用标题保证唯一。

## 四、署名规则

### 6. `wang` 只在需要署名的地方用

`wang` 作为**署名**使用，仅在需要署名的场景出现即可；不必过于严谨，不要给类名 / id / 变量批量加 `wang` 前缀。
（代码标识符的前缀规则见第 1 条 `wzy_`。）

## 五、实现约定（Conventions）

### 7. 纯原生实现

只使用原生 HTML、CSS、JavaScript，不引入第三方库、框架和 CDN 资源。

- 不使用 Vue / React / jQuery / Bootstrap 等框架或库
- 不通过 `<script src="https://…">`、`@import url(https://…)` 等方式引用远程资源
- 样式、脚本、图形尽量写在页面内（`<style>` / `<script>` / 内联 SVG），保证双击即可打开、断网可用

### 8. 图标来源

图标一律使用 `font/` 目录下的本地 iconfont（`font/iconfont.css` 等，相对路径 `./font/…`），不引入其他图标库或图标 CDN。

```html
<link rel="stylesheet" href="font/iconfont.css">
<i class="iconfont icon-home"></i>
```

> 现有 4 个图标：`icon-home` / `icon-message` / `icon-find` / `icon-user`（码位 E600~E603，字体在 `font/iconfont.woff2`）。

### 9. 数据请求

需要服务器端数据时使用原生 `fetch()` API，不用 jQuery / axios 之类的封装。

```js
fetch("./data.json")
  .then(function (res) { return res.json(); })
  .then(function (data) { /* … */ });
```

> **第 7、8 条的既有例外**：第十二章（`12-1` Font Awesome、`12-2` Lucide）与第十三章（`13-1` FA link 引入、`13-2` Lucide JS 运行时）
> 是课程指定的「字体图标 / 图标库」练习，必须使用 Font Awesome 与 Lucide。
> 其资源已**本地化**在 `cdn/`（`cdn/all.min.css`、`cdn/lucide.min.js` + 48 个 svg），不联网、可离线，**不是远程 CDN**。
> 这两章作为既定课程内容保留现状；**后续新增页面**按第 7、8 条执行。

## 六、适用范围与现状

- 第 1、2 条自 **2026-10-22** 起对**新增和修改**的页面生效。
- 既有 25 个课堂作品使用无前缀命名（如 `.card`、`id="themeBtn"`），**尚未回改**；
  回改需同步修改 CSS 选择器与 JS 引用，属独立重构任务。
- `14-1.html` 目前是空模板（227 B，`<title>Document</title>`），内容写好后需按第 1、2、5 条一并落实。
