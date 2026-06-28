---
title: "Academic Pages 完整工作流程指南"
permalink: /step/
sitemap: false
---

# Academic Pages 个人学术网站 —— 完整工作流程指南

本仓库基于 **Academic Pages** 模板（Jekyll + GitHub Pages），用于搭建个人学术主页，托管在 GitHub Pages 上，**免费、无广告**。

> 📖 **核心思想**：内容与样式分离。你只需要编辑 Markdown 文件和 YAML 配置文件，Jekyll 会自动生成静态 HTML 页面。每次 `git push` 到 GitHub，GitHub Actions 会自动构建并发布网站。

---

## 📁 目录结构速览

| 目录 / 文件 | 作用 |
| --- | --- |
| `_config.yml` | **全局配置** — 网站标题、作者信息、社交媒体链接、主题等 |
| `_data/` | **结构化数据** — 导航栏、作者信息、评论、CV JSON |
| `_pages/` | **独立页面** — 首页、关于、CV 等 |
| `_posts/` | **博客文章** |
| `_publications/` | **论文列表** |
| `_talks/` | **学术报告 / 演讲** |
| `_teaching/` | **教学经历** |
| `_portfolio/` | **项目作品集** |
| `_drafts/` | **草稿**（本地预览时可见，不发布） |
| `images/` | **图片资源**（头像、文章配图等） |
| `files/` | **静态文件**（PDF 论文、幻灯片等） |
| `assets/` | **CSS、JS、字体等前端资源** |
| `markdown_generator/` | **批量生成工具**（Jupyter Notebook / Python 脚本） |
| `talkmap/` | **演讲地图**（通过 Jupyter Notebook 生成） |
| `_includes/` | **可复用的 HTML 片段**（页头、页脚、侧边栏等） |
| `_layouts/` | **页面布局模板** |
| `_sass/` | **样式文件**（可自定义主题颜色等） |

---

## 🚀 快速开始

### 1. Fork / Clone 本仓库

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_USERNAME.github.io.git
cd YOUR_USERNAME.github.io
```

### 2. 修改网站基本信息

编辑根目录下的 `_config.yml`，这是**最重要的配置文件**：

```yaml
# --- 基本设置 ---
title                    : "你的姓名 / 网站标题"
name                     : "你的姓名"
description              : "你的个人学术主页"
url                      : "https://你的用户名.github.io"
repository               : "你的用户名/你的用户名.github.io"

# --- 作者侧边栏信息 ---
author:
  avatar           : "profile.png"     # 头像图片，放在 images/ 目录下
  name             : "侧边栏显示的名字"
  bio              : "简短的个人介绍"
  location         : "所在城市/国家"
  employer         : "所在机构"
  email            : "your@email.com"

  # 学术平台（填入完整 URL 或用户名）
  googlescholar    : "https://scholar.google.com/citations?user=..."
  orcid            : "https://orcid.org/0000-0002-..."
  pubmed           : "https://www.ncbi.nlm.nih.gov/pubmed/?term=..."

  # 代码托管
  github           : "你的GitHub用户名"
  stackoverflow    : "你的StackOverflow编号"

  # 社交媒体
  bluesky          : "你的Bluesky用户名"
  linkedin         : "你的LinkedIn用户名"
  twitter          : "你的Twitter用户名"
  youtube          : "你的YouTube用户名"
  # ... 其他字段同理，留空则不显示
```

> 💡 **头像图片**：将你的头像命名为 `profile.png` 或 `profile.jpg`，放到 `images/` 目录下，然后在 `_config.yml` 中设置 `avatar` 路径。

### 3. 修改导航栏

编辑 `_data/navigation.yml`：

```yaml
main:
  - title: "Publications"    # 显示的文字
    url: /publications/      # 链接地址
  - title: "Talks"
    url: /talks/
  - title: "Teaching"
    url: /teaching/
  - title: "Portfolio"
    url: /portfolio/
  - title: "Blog Posts"
    url: /year-archive/
  - title: "CV"
    url: /cv/
  - title: "Guide"
    url: /markdown/
```

> 不需要的栏目直接删除整行即可，也可以添加自定义页面链接。

---

## ✍️ 如何发布博客文章

在 `_posts/` 目录下创建 Markdown 文件，命名规则必须为：

```
YYYY-MM-DD-标题-slug.md
```

例如：`2025-06-27-my-research-update.md`

文件内容格式：

```markdown
---
title: "博客文章标题"
date: 2025-06-27
permalink: /posts/2025/06/my-research-update/    # 自定义永久链接
tags:
  - 标签1
  - 标签2
  - 标签3
---

这里写正文，支持 Markdown 语法。

## 二级标题

可以写段落、列表、代码块等等。
```

> ⚠️ 文件名中的日期会覆盖 front matter 中的 `date` 字段。

---

## 📄 如何添加论文

在 `_publications/` 目录下创建 Markdown 文件：

```markdown
---
title: "论文标题"
collection: publications
category: conferences             # 或 manuscripts（期刊）、books（书籍）
permalink: /publication/2025-06-01-paper-title
excerpt: '简短摘要或描述'
date: 2025-06-01
venue: '发表期刊/会议名称'
paperurl: 'https://链接到论文.pdf'   # 或 /files/paper1.pdf（放在本地）
slidesurl: 'https://链接到幻灯片'    # 可选
citation: '作者名 (2025). &quot;论文标题&quot;. <i>期刊名</i>.'
---

这里可以写更详细的论文介绍，会显示在论文的独立详情页上。
```

> 📌 **上传 PDF**：把 PDF 文件放到 `files/` 目录，链接路径写 `/files/your-paper.pdf`。

### 论文分类

在 `_config.yml` 中定义分类：

```yaml
publication_category:
  books:
    title: 'Books'
  manuscripts:
    title: 'Journal Articles'     # 期刊论文
  conferences:
    title: 'Conference Papers'    # 会议论文
```

在每篇论文的 front matter 中设置 `category: manuscripts` 或 `category: conferences`，网站会自动按分类展示。

### 批量导入论文

1. 编辑 `markdown_generator/publications.tsv` 或 `.csv`
2. 运行 `markdown_generator/publications.ipynb`（Jupyter Notebook）或 `python publications.py`
3. 脚本会自动在 `_publications/` 生成对应的 Markdown 文件

TSV 格式：

```text
pub_date	title	venue	excerpt	citation	url_slug	paper_url	slides_url	category
2025-06-01	My Paper Title	Journal Name	Short excerpt	Author (2025). Title.	my-paper-title	/files/paper.pdf		manuscripts
```

---

## 🎤 如何添加演讲 / 学术报告

在 `_talks/` 目录下创建 Markdown 文件：

```markdown
---
title: "演讲标题"
collection: talks
type: "Talk"                     # 或 "Tutorial" 等
permalink: /talks/2025-06-01-talk-title
venue: "举办机构 / 会议名称"
date: 2025-06-01
location: "城市, 国家"
---

这里是演讲的详细描述，支持 Markdown。
```

> 演讲的 `location` 字段会被 talkmap 脚本用来生成地理地图，请填写真实的地点名称。

---

## 🏫 如何添加教学经历

在 `_teaching/` 目录下创建 Markdown 文件：

```markdown
---
title: "课程名称"
collection: teaching
type: "Undergraduate course"      # 本科生课程 / 研究生课程 / Workshop 等
permalink: /teaching/2025-spring-course-name
venue: "大学名称, 院系"
date: 2025-01-01
location: "城市, 国家"
---

课程描述、教学大纲、学生反馈等，支持 Markdown。
```

---

## 🖼️ 如何添加作品集

在 `_portfolio/` 目录下创建 `.md` 或 `.html` 文件：

```markdown
---
title: "项目名称"
excerpt: "简短描述，可以包含图片 <br/><img src='/images/project-image.png'>"
collection: portfolio
---

这里是项目的详细介绍，支持 Markdown。
```

> `.md` 文件用 Markdown 渲染，`.html` 文件用 HTML 渲染。

---

## 👤 如何修改个人资料（Profile）

### 修改侧边栏信息

编辑 `_config.yml` 中的 `author:` 部分（如上所述）。

### 修改首页内容

编辑 `_pages/about.md`（如果设置了 `permalink: /` 则为首页）：

```markdown
---
permalink: /
title: "欢迎来到我的个人主页"
author_profile: true
---

这里是首页正文内容...
```

### 修改 CV

**方式一：Markdown CV**
编辑 `_pages/cv.md`，用纯 Markdown 书写学历、工作经历、技能等。

**方式二：JSON CV**
编辑 `_data/cv.json`，这是一个结构化 JSON 文件，会被渲染为格式化的 CV 页面。

在 `_data/navigation.yml` 中选择使用哪一个：

```yaml
main:
  - title: "CV"
    url: /cv/          # Markdown CV
  # - title: "CV"
  #   url: /cv-json/   # JSON CV（取消注释）
```

也可以运行脚本从 Markdown 自动生成 JSON CV：

```bash
bash scripts/update_cv_json.sh
```

---

## 🖼️ 如何添加图片

1. 将图片文件放入 `images/` 目录
2. 在 Markdown 中引用：

```markdown
![图片描述](/images/your-image.png)

![带链接的图片](https://example.com/image.png)

![相对路径引用](/images/profile.png)
```

> 图片建议使用 PNG 或 JPG 格式，控制文件大小以提高加载速度。

---

## 📎 如何上传文件（PDF 等）

将文件放入 `files/` 目录，链接路径为：

```markdown
[查看论文 PDF](/files/paper1.pdf)

[下载幻灯片](/files/slides1.pdf)
```

文件会托管在 `https://你的用户名.github.io/files/文件名`。

---

## 🎨 如何更换主题

在 `_config.yml` 中修改：

```yaml
site_theme: "default"   # 可选值：default, air, sunrise, mint, dirt, contrast
```

每种主题都有深色和浅色两种模式，主题预览图在 `images/themes/` 目录下。

---

## 🗺️ 演讲地图（Talkmap）

本仓库支持将演讲地点生成一张集群地图。

### 手动生成

1. 确保每个 `_talks/*.md` 文件都有 `location` 字段
2. 运行 `talkmap.ipynb`（Jupyter Notebook）或 `python talkmap.py`
3. 生成的 HTML 地图文件会输出到 `talkmap/map.html`

### 自动生成（GitHub Actions）

本仓库配置了 GitHub Actions 工作流 `.github/workflows/scrape_talks.yml`，当 `_talks/` 目录有变更时会自动运行并更新地图。

在 `_config.yml` 中启用地图链接：

```yaml
talkmap_link: true
```

---

## 🛠️ 批量生成工具（Markdown Generator）

`markdown_generator/` 目录提供了 Jupyter Notebook 和 Python 脚本，用于从表格数据批量生成 Markdown 文件。

### 论文批量生成

1. 编辑 `publications.tsv` 或 `publications.csv`
2. 运行 `publications.ipynb`（推荐）或 `python publications.py`
3. 脚本会自动在 `_publications/` 生成规范命名的 Markdown 文件

### 演讲批量生成

运行 `talks.ipynb`，从 `talks.tsv` 批量生成演讲 Markdown 文件。

---

## 💬 如何开启评论功能

在 `_config.yml` 中设置评论提供者：

```yaml
comments:
  provider: "disqus"    # 可选：disqus, discourse, facebook, google-plus, staticman, 或 false（关闭）
  disqus:
    shortname: "你的disqus短名"
```

需要先去对应平台注册账号。

---

## 💻 本地预览

### 方式一：本地安装 Jekyll（推荐）

```bash
# 安装依赖（首次运行）
bundle install

# 如果遇到权限问题，先配置本地安装路径
bundle config set --local path 'vendor/bundle'
bundle install

# 启动本地服务器
bundle exec jekyll serve -l -H localhost
```

访问 **http://localhost:4000** 即可预览。

> 💡 修改 `_config.yml` 需要**重启** Jekyll 服务器；修改 Markdown 文件会自动刷新。
> 💡 Windows 用户建议通过 **WSL（Windows Subsystem for Linux）** 运行以上命令。

### 方式二：使用 Docker

```bash
chmod -R 777 .
docker compose up
```

访问 **http://localhost:4000** 预览。

### 方式三：VS Code DevContainer

用 VS Code 打开项目，会提示重新在容器中打开（或按 `F1` → `Dev Containers: Reopen in Container`），容器自动运行 Jekyll 服务器，访问 http://localhost:4000 即可预览。

---

## 📝 高级功能

### 数学公式（MathJax）

支持 LaTeX 数学公式：

```latex
$$    # 块级公式
\nabla \cdot E = \frac{\rho}{\epsilon_0}
$$

行内公式：\( a^2 + b^2 = c^2 \)
```

### 图表（Mermaid）

```mermaid
graph LR
A-->B
```

代码写法：

````markdown
```mermaid
graph LR
A-->B
```
````

### 交互式图表（Plotly）

````markdown
```plotly
{
  "data": [{
    "x": [1, 2, 3, 4],
    "y": [10, 15, 13, 17],
    "type": "scatter"
  }]
}
```
````

### 可折叠内容

```html
<details>
  <summary>点击展开</summary>
  这里是折叠的内容...
</details>
```

### 提示框（Notice）

```markdown
**注意：** 这是一条提示信息。
{: .notice}
```

---

## 🚢 发布到 GitHub Pages

1. 将仓库名改为 `你的用户名.github.io`
2. 在 `_config.yml` 中设置正确的 `url` 和 `repository`
3. 推送代码到 GitHub：

```bash
git add .
git commit -m "更新网站内容"
git push
```

4. 在 GitHub 仓库的 **Settings → Pages** 中确认 Source 设置为：
   - **Source**: Deploy from a branch
   - **Branch**: `master`（或 `main`），目录 `/`（root）

5. 等待 1-2 分钟，访问 `https://你的用户名.github.io` 即可看到网站

> ✅ GitHub Actions 会自动构建，可以在仓库的 **Actions** 标签页查看构建状态。
> - 绿色勾 ✅：构建成功
> - 黄色圆圈 ⏳：正在构建
> - 红色叉 ❌：构建失败，点击查看错误日志

---

## ❓ 常见问题

### Q: 修改后网站没有变化？
A: GitHub Pages 构建需要 1-2 分钟，可以在 Actions 标签页查看进度。建议先在本地预览确认无误再推送。

### Q: 本地运行报错？
A: 尝试 `bundle update` 更新依赖，或删除 `Gemfile.lock` 后重新 `bundle install`。

### Q: 如何添加新的页面类型？
A: 在 `_pages/` 目录添加 Markdown 文件，然后在 `_data/navigation.yml` 中添加导航链接。

### Q: 如何删除某个栏目（如 Portfolio）？
A: 从 `_data/navigation.yml` 中移除对应条目即可，对应目录下的文件可以保留（不会被访问到）。

### Q: 如何修改网站图标（favicon）？
A: 替换 `images/favicon.ico`、`images/favicon-32x32.png` 等文件即可。

### Q: 如何开启 Google Analytics？
A: 在 `_config.yml` 中设置：

```yaml
analytics:
  provider: "google-analytics-4"
  google:
    tracking_id: "G-XXXXXXXXXX"
```

---

## 📚 参考资源

- [Academic Pages 官方文档](https://academicpages.github.io/markdown/)
- [Minimal Mistakes 主题文档](https://mmistakes.github.io/minimal-mistakes/docs/configuration/)
- [Jekyll 官方文档](https://jekyllrb.com/docs/)
- [GitHub Pages 文档](https://docs.github.com/en/pages)
- [Markdown 教程（kramdown）](https://kramdown.gettalong.org/syntax.html)
- [Liquid 模板语法](https://shopify.github.io/liquid/tags/control-flow/)

---

*Happy Building! 🚀*
