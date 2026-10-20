# 个人实验室 · Personal Lab

一个用于展示个人简介、整理简历与分享学习笔记的个人网站。以深色科技实验室为视觉主题，记录学习过程中的问题、实践与思考。

**[访问网站](https://griffin-peng.github.io/)** · [查看简历](https://griffin-peng.github.io/resume/) · [阅读笔记](https://griffin-peng.github.io/notes/)

## 网站内容

| 页面 | 内容 |
| --- | --- |
| 首页 | 个人简介、关注方向与最新学习笔记 |
| 简历 | 教育背景、技能与项目经历，支持浏览器打印；提供真实 PDF 后可显示下载入口 |
| 学习笔记 | 按时间排列的笔记列表，展示分类、标签与摘要 |
| 笔记详情 | Markdown 正文、代码示例与可折叠的文章目录 |

当前个人资料与简历仍为待填写模板，示例笔记已在页面中标注，后续会逐步替换为真实内容。

## 设计与阅读体验

- **科技实验室风格**：深色背景、网格纹理与薄荷绿点缀。
- **响应式布局**：适配桌面和手机，照顾长标题与正文的阅读体验。
- **便捷阅读**：文章目录支持章节跳转，提供键盘导航与清晰的焦点样式。
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
├── notes/              # 笔记列表与文章详情
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
| `src/content/notes/*.md` | 学习笔记，每篇笔记一个文件 |
| `public/resume.pdf` | 可选的公开版简历 PDF |

笔记日期使用带引号的 `YYYY-MM-DD`，例如 `date: "2026-10-20"`。替换模板或示例内容后，将对应文件的 `sample` 改为 `false`。网站内容与简历 PDF 都会公开，请使用适合公开展示的版本。

## 发布与更新

1. 在源码项目中修改内容，使用 Node.js 22.22 或更新的受支持版本构建：

   ```sh
   npm run build -- --site https://griffin-peng.github.io/
   ```

2. 将生成的 `dist/` **内容**同步到本仓库根目录，保留 `.git/`、`README.md` 和 `.nojekyll`，同时移除因删文而失效的旧页面。
3. 提交并推送到 `main`。GitHub Pages 使用 **Deploy from a branch → main → /(root)** 发布。
4. 在 [Actions](https://github.com/Griffin-Peng/griffin-peng.github.io/actions) 查看发布结果，完成后访问网站确认更新。

编辑本地 Markdown 后需要重新构建、提交并发布；当前仓库的 Pages workflow 负责发布静态文件，源码项目单独维护。
