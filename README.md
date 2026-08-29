# fs² 的个人博客

一个使用 Astro 构建的个人博客。

博客主要用于记录：

- 编程学习
- Web 开发
- 游戏开发
- AI / Agent
- 工作经历
- 生活与随想

首页采用全屏封面设计，以 `home.png` 作为背景。

封面显示：

> fs² 的个人博客

并通过打字效果显示：

> 让这梦做的够长让梦中人求疯得疯

向下滚动进入博客正文。

---

# 一、项目结构

```text
my-blog/
│
├── public/
│   └── home.png
│
├── src/
│   │
│   ├── assets/
│   │   ├── astro.svg
│   │   └── background.svg
│   │
│   ├── components/
│   │   ├── HomeCover.astro
│   │   ├── PostItem.astro
│   │   └── PostList.astro
│   │
│   ├── content/
│   │   └── posts/
│   │       ├── 2026-08-18-learning-agent.md
│   │       ├── 2026-08-21-wukong-game.md
│   │       └── 2026-08-24-about-blog.md
│   │
│   ├── layouts/
│   │   ├── BaseLayout.astro
│   │   └── Layout.astro
│   │
│   ├── pages/
│   │   ├── index.astro
│   │   │
│   │   └── posts/
│   │       └── [...slug].astro
│   │
│   ├── styles/
│   │   └── global.css
│   │
│   └── content.config.ts
│
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── README.md
````

---

# 二、项目根目录

## `astro.config.mjs`

Astro 项目的核心配置文件。

用于配置 Astro 本身，例如：

* Astro 集成
* 构建配置
* 输出模式
* 部署相关配置

目前项目主要使用 Astro 默认配置。

---

## `package.json`

Node.js 项目的配置文件。

主要记录：

* 项目名称
* 项目版本
* npm scripts
* 项目依赖

例如：

```bash
npm run dev
```

启动开发服务器。

```bash
npm run build
```

构建项目。

```bash
npm run preview
```

预览构建结果。

---

## `tsconfig.json`

TypeScript 配置文件。

用于控制：

* TypeScript 编译规则
* 类型检查
* 模块解析
* Astro 项目的 TypeScript 支持

---

## `README.md`

项目说明文档。

用于记录：

* 项目介绍
* 项目结构
* 文件用途
* 开发方式
* 后续计划

---

# 三、`public/`

```text
public/
└── home.png
```

`public` 用于存放可以直接被浏览器访问的静态资源。

---

## `public/home.png`

博客首页封面背景图。

目前博客封面使用它作为背景：

```css
background-image: url("/home.png");
```

因为文件位于 `public`，所以浏览器访问路径是：

```text
/home.png
```

---

# 四、`src/assets/`

```text
src/assets/
├── astro.svg
└── background.svg
```

这里存放 Astro 项目使用的资源文件。

目前：

* `astro.svg`
* `background.svg`

属于 Astro 初始化项目时产生的资源。

如果后续确认不再使用，可以删除。

---

# 五、`src/components/`

这里存放博客中的可复用组件。

目前有三个组件：

```text
components/
├── HomeCover.astro
├── PostItem.astro
└── PostList.astro
```

---

## `HomeCover.astro`

负责博客首页的封面。

主要功能：

* `home.png` 背景
* `fs² 的个人博客`
* 打字效果
* `让这梦做的够长让梦中人求疯得疯`
* 向下滚动箭头
* 封面背景渐渐透明
* 鼠标滚轮进入正文
* 正文顶部向上滚动返回封面
* 封面与正文之间的平滑过渡
* 滚动动画

封面是博客首页最主要的视觉部分。

目前封面本身已经完成。

---

## `PostList.astro`

负责显示博客文章列表。

它从 Astro Content Collection 中读取文章：

```ts
const posts = await getCollection("posts");
```

然后：

1. 获取所有文章
2. 按日期倒序排列
3. 根据年份进行分组
4. 将每篇文章交给 `PostItem.astro` 显示

结构大致为：

```text
PostList
│
├── 2026
│   ├── PostItem
│   ├── PostItem
│   └── PostItem
│
├── 2025
│   ├── PostItem
│   └── PostItem
│
└── ...
```

因此以后新增 Markdown 文章后，文章列表可以自动更新。

---

## `PostItem.astro`

负责显示一篇文章在文章列表中的样子。

目前包含：

* 文章日期
* 文章标题
* 文章简介
* 文章链接

例如：

```text
08.24    关于这个博客
         从一张封面开始，给自己留一个可以慢慢写下去的地方。
```

点击文章后进入对应的文章详情页面。

---

# 六、`src/content/`

这里存放博客真正的文章内容。

```text
src/content/
└── posts/
```

---

## `src/content/posts/`

每一个 `.md` 文件代表一篇博客文章。

目前：

```text
posts/
├── 2026-08-18-learning-agent.md
├── 2026-08-21-wukong-game.md
└── 2026-08-24-about-blog.md
```

以后写新文章时，只需要在这里增加新的 Markdown 文件。

例如：

```text
2026-08-30-my-new-post.md
```

---

## Markdown 文章结构

一篇文章通常由两部分组成：

### Frontmatter

例如：

```yaml
---
title: "关于这个博客"
date: 2026-08-24
description: "从一张封面开始，给自己留一个可以慢慢写下去的地方。"
tags:
  - 随笔
---
```

用于描述文章的基本信息。

包括：

```text
title
文章标题

date
文章日期

description
文章简介

tags
文章标签
```

---

### Markdown 正文

Frontmatter 后面的内容就是文章正文。

例如：

```md
## 为什么做这个博客

有些东西如果不记录，很快就会忘记。

所以我想给它们留一个地方。
```

Astro 会负责将 Markdown 转换为网页。

---

# 七、`src/content.config.ts`

这是 Astro Content Collection 的配置文件。

它定义博客文章的数据结构。

目前：

```ts
const posts = defineCollection({
  type: "content",

  schema: z.object({
    title: z.string(),
    date: z.coerce.date(),
    description: z.string().optional(),
    tags: z.array(z.string()).optional(),
  }),
});
```

也就是说，每篇文章至少需要：

```text
title
date
```

以下字段是可选的：

```text
description
tags
```

---

## 为什么需要 `content.config.ts`

它可以让 Astro 知道：

> `src/content/posts/` 里面的 Markdown 文件是一组博客文章。

并且规定文章的数据格式。

例如：

```yaml
title: "关于这个博客"
date: 2026-08-24
```

符合定义。

如果写成错误的数据类型，Astro 在构建时可以发现问题。

---

# 八、`src/layouts/`

```text
layouts/
├── BaseLayout.astro
└── Layout.astro
```

Layout 用于定义页面的整体 HTML 结构。

---

## `BaseLayout.astro`

目前博客主要使用的基础布局。

负责：

```html
<html>
<head>
<body>
```

以及：

* 页面标题
* description
* 全局 CSS
* 页面内容插槽

首页：

```text
index.astro
    ↓
BaseLayout
    ↓
HomeCover
    ↓
PostList
```

以后可以在这里继续增加：

* favicon
* SEO
* Open Graph
* RSS
* 网站统计代码

---

## `Layout.astro`

这是 Astro 项目早期创建时可能留下的布局文件。

如果项目中已经没有任何地方引用：

```text
Layout.astro
```

那么后续可以删除。

目前暂时保留，避免在重构阶段误删正在使用的代码。

---

# 九、`src/pages/`

Astro 使用文件系统路由。

也就是说：

```text
src/pages/index.astro
```

对应：

```text
/
```

而：

```text
src/pages/posts/[...slug].astro
```

负责文章页面路由。

---

## `src/pages/index.astro`

博客首页。

现在它已经非常简单：

```astro
<BaseLayout>

  <HomeCover />

  <PostList />

</BaseLayout>
```

也就是说：

```text
首页
│
├── HomeCover
│
└── PostList
```

`index.astro` 本身不负责封面的具体实现，也不负责文章列表的具体实现。

它只负责把组件组合起来。

---

## `src/pages/posts/[...slug].astro`

负责博客文章详情页。

例如：

```text
/posts/2026-08-24-about-blog
```

最终由这个页面处理。

它会根据文章 slug 找到对应的 Markdown 文件，然后将 Markdown 渲染成网页。

---

# 十、`src/styles/`

```text
styles/
└── global.css
```

---

## `global.css`

全局 CSS。

用于定义整个网站共同的样式，例如：

* body
* html
* 全局字体
* 链接
* 图片
* 选择文字颜色
* 页面基础颜色

例如正文背景目前使用：

```css
background: rgb(252, 252, 252);
```

组件自己的特殊样式则尽量写在对应的 `.astro` 文件中。

例如：

```text
HomeCover.astro
    ↓
封面专属 CSS

PostList.astro
    ↓
文章列表专属 CSS

PostItem.astro
    ↓
文章项目专属 CSS
```

这样可以避免一个 CSS 文件越来越庞大。

---

# 十一、页面之间的关系

目前博客的整体结构：

```text
                    index.astro
                         │
                         ▼
                  BaseLayout.astro
                         │
                ┌────────┴────────┐
                ▼                 ▼
         HomeCover.astro    PostList.astro
                                  │
                     ┌────────────┼────────────┐
                     ▼            ▼            ▼
                 PostItem     PostItem     PostItem
                     │            │            │
                     └────────────┼────────────┘
                                  │
                                  ▼
                         content/posts/*.md
```

---

# 十二、访问文章的流程

当用户打开首页：

```text
/
```

执行：

```text
index.astro
```

然后：

```text
HomeCover
    ↓
PostList
```

---

当用户点击某篇文章：

```text
文章列表
    ↓
/posts/xxx
    ↓
posts/[...slug].astro
    ↓
对应 Markdown
    ↓
完整文章
```

---

# 十三、目前博客的设计思路

博客目前不使用传统的顶部导航栏。

首页：

```text
┌──────────────────────────────┐
│                              │
│        fs² 的个人博客         │
│                              │
│   让这梦做的够长让梦中人求疯得疯 │
│                              │
│              ↓               │
│                              │
│          home.png            │
│                              │
└──────────────────────────────┘
              ↓
            滚动
              ↓
┌──────────────────────────────┐
│                              │
│  2026                        │
│                              │
│  08.24   关于这个博客         │
│          ……                  │
│                              │
│  08.21   做游戏的一些记录     │
│          ……                  │
│                              │
│  08.18   最近在学习什么       │
│          ……                  │
│                              │
└──────────────────────────────┘
```

正文采用时间线思路。

左侧主要负责表达：

```text
时间
```

而不是：

```text
目录
文件夹
分类导航
```

这样整个博客会更像个人记录，而不是传统内容管理网站。

---

# 十四、开发命令

安装依赖：

```bash
npm install
```

启动开发服务器：

```bash
npm run dev
```

构建：

```bash
npm run build
```

预览生产版本：

```bash
npm run preview
```

---

# 十五、后续计划

目前已经完成：

* [x] Astro 项目建立
* [x] 全屏首页封面
* [x] `home.png` 背景
* [x] 博客标题
* [x] 打字效果
* [x] 封面滚动动画
* [x] 封面淡出
* [x] 正文顶部返回封面
* [x] Markdown 文章目录结构
* [x] Content Collection 基础结构
* [x] 首页组件拆分

后续计划：

* [ ] 完善文章列表视觉效果
* [ ] 完善文章详情页
* [ ] 优化时间轴
* [ ] Markdown 代码高亮
* [ ] 文章上一篇 / 下一篇
* [ ] RSS
* [ ] SEO
* [ ] Open Graph
* [ ] favicon
* [ ] 移动端优化
* [ ] 部署到公网

```