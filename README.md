# 个人实验室 · Personal Lab

一个用于展示个人简介、整理简历与分享学习笔记的个人网站。笔记按主题合集组织，以深色科技实验室为视觉主题，记录学习过程中的问题、实践与思考。

**[访问网站](https://griffin-peng.github.io/)** · [查看简历](https://griffin-peng.github.io/resume/) · [阅读笔记](https://griffin-peng.github.io/notes/)

## 网站内容

| 页面 | 内容 |
| --- | --- |
| 首页 | 个人简介、关注方向与最新学习笔记 |
| 简历 | 教育背景、技能与项目经历，支持浏览器打印；提供真实 PDF 后可显示下载入口 |
| 学习笔记 | 展示各个学习合集的名称、简介与篇数 |
| 合集详情 | 合集介绍与章节列表，文章按 Markdown 文件名前的数字排序 |
| 笔记详情 | Markdown 正文与代码示例，左侧本文目录由 Markdown 标题自动生成 |

当前个人资料与简历仍为待填写模板，示例笔记已在页面中标注，后续会逐步替换为真实内容。

## 设计与阅读体验

- **科技实验室风格**：深色背景、网格纹理与薄荷绿点缀。
- **响应式布局**：适配桌面和手机，照顾长标题与正文的阅读体验。
- **清晰导航**：全站主导航在顶部横排；从合集介绍和章节列表进入单篇文章。
- **便捷阅读**：桌面端左侧显示本文目录，手机上移到正文前并可折叠；支持章节跳转、键盘操作与清晰的焦点样式。
- **打印支持**：简历和笔记使用白底打印样式，方便打印或另存为 PDF。
- **轻量加载**：页面无需客户端 JavaScript，也不依赖外部字体、图片或第三方脚本。
- **搜索与分享**：包含 canonical、Open Graph、sitemap、robots 与自定义 404 页面。

## 技术栈

| 技术 | 用途 |
| --- | --- |
| Astro 7 | 构建静态多页面网站 |
| TypeScript | 构建期逻辑与内容处理 |
| HTML / CSS | 页面结构、视觉样式、响应式布局与打印样式 |
| Markdown / YAML | 维护简介、简历、笔记正文和元数据 |
| GitHub Pages | 托管静态文件，通过 HTTPS 公开访问 |

网站在构建时生成 HTML 和资源文件，无需数据库或应用后端。Node.js 用于源码项目的开发与构建，访客直接访问生成的网页。

## 仓库结构

本仓库保存 GitHub Pages 的**静态发布文件**。Astro / TypeScript 源码与 Markdown 内容在独立的源码项目中维护。

```text
.
├── index.html          # 首页
├── resume/             # 简历
├── notes/              # 合集列表与文章详情
│   └── collections/    # 各合集介绍与章节列表
├── _astro/             # 构建生成的样式资源
├── favicon.svg         # 网站图标
├── 404.html            # 自定义错误页
├── sitemap.xml         # 站点地图
├── robots.txt          # 爬虫访问规则
├── .nojekyll           # 保留 _astro 等以下划线开头的目录
└── README.md           # 项目介绍
```

## 内容维护

在源码项目中编辑以下文件：

| 文件 | 用途 |
| --- | --- |
| `src/content/profile/main.md` | 个人简介与学习方向 |
| `src/content/resume/main.md` | 简历内容 |
| `src/content/notebooks/*.md` | 合集名称、简介与介绍正文 |
| `src/content/notes/<合集名>/*.md` | 合集内的笔记，每篇一个文件 |
| `src/content/notes/*.md` | 根目录的通用笔记，保留原有文章链接 |
| `public/resume.pdf` | 可选的公开版简历 PDF |

例如，新建 MySQL 合集时，在源码项目中按下面的结构添加文件：

```text
src/content/
├── notebooks/
│   └── mysql.md
└── notes/
    └── mysql/
        ├── 1.MySQL入门.md
        ├── 2.基础查询.md
        └── 10.事务.md
```

`notebooks/mysql.md` 保存合集介绍：

```md
---
title: MySQL 学习笔记
description: 按章节整理基础查询、索引与事务。
---

这里写学习目标、参考资料和合集说明。
```

`notes/mysql/1.MySQL入门.md` 保存单篇笔记：

```md
---
title: MySQL 入门
description: 认识数据库、表与 SQL。
date: "2026-10-23"
category: 数据库
tags: [MySQL, SQL]
sample: false
---

## 学习内容

在这里记录你的学习过程。
```

合集介绍的文件名与笔记文件夹名保持完全一致。合集介绍页地址为 `/notes/collections/mysql/`，章节自动按文件编号 `1 → 2 → 10` 排列，兼容 `01.` 等补零形式；同编号按文件名自然排序，无编号文章放在末尾。首页最近记录仍按日期显示。

笔记日期使用带引号的有效 `YYYY-MM-DD`。替换模板或示例内容后，将对应文件的 `sample` 改为 `false`。文章的 `##`、`###` 标题自动生成本文目录；没有这些标题时不显示空目录。`category` 和 `tags` 描述文章，合集归属由文件夹决定。

文章 URL 由 Astro 根据相对文件路径生成，以网页中的链接为准。重命名文件或目录（包括调整编号）会改变文章地址；根目录已有示例文章仍保持原链接，归入“通用笔记”。`collections` 是保留路径，不作为合集名或笔记文件夹名。

网站内容与简历 PDF 都会公开，请使用适合公开展示的版本。

## 发布与更新

1. 在源码项目中修改内容，使用 Node.js 22.22 或更新的受支持版本构建：

   ```sh
   npm run build -- --site https://griffin-peng.github.io/
   ```

2. 将生成的 `dist/` **内容**同步到本仓库根目录，保留 `.git/`、`README.md` 和 `.nojekyll`，同时移除因删文而失效的旧页面。
3. 提交并推送到 `main`。GitHub Pages 使用 **Deploy from a branch → main → /(root)** 发布。
4. 在 [Actions](https://github.com/Griffin-Peng/griffin-peng.github.io/actions) 查看发布结果，完成后访问网站确认更新。

编辑本地 Markdown 后需要重新构建、提交并发布；当前仓库的 Pages workflow 负责发布静态文件，源码项目单独维护。
