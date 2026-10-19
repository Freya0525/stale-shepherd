# online resume

一个基于 Astro 构建的专业个人简历网站，面向 Java 后端与 AI Agent 开发岗位，支持响应式浏览、头像展示、完整技能清单、项目经历与 GitHub Pages 自动部署。

<p align="center">
  <a href="https://freya0525.github.io/stale-shepherd/">在线预览</a>
  ·
  <a href="https://github.com/Freya0525/stale-shepherd/actions">部署状态</a>
</p>

![Astro](https://img.shields.io/badge/Astro-7.x-BC52EE?logo=astro&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-22%2B-339933?logo=node.js&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/Hosted%20on-GitHub%20Pages-222222?logo=github&logoColor=white)
![License](https://img.shields.io/badge/license-personal-use-blue)

## 在线预览

访问：<https://freya0525.github.io/stale-shepherd/>

网站采用深蓝到青绿色渐变头图、信息卡片、技能标签和清晰的简历分节，适合桌面端浏览，也适合手机端查看。

## 功能特性

- 响应式简历布局，适配桌面端和移动端
- 支持本地头像文件展示
- 完整展示 Java、Spring Cloud、MySQL、Redis、消息队列和 AI 相关技能
- 项目职责、技能描述和项目亮点采用数据驱动方式渲染
- 支持 GitHub Pages 静态部署
- 推送到 `main` 分支后自动执行构建和发布
- 支持浏览器打印为 PDF
- 使用 Astro 静态生成，无需后端服务或数据库

## 技术栈

| 技术 | 用途 |
| --- | --- |
| Astro | 页面构建与静态生成 |
| TypeScript | Astro 类型检查 |
| CSS | 响应式布局与视觉样式 |
| GitHub Actions | 自动构建和部署 |
| GitHub Pages | 静态网站托管 |

## 项目目录

```text
stale-shepherd/
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Pages 自动部署
├── public/
│   ├── avatar.jpg           # 个人头像
│   ├── favicon.svg          # 站点图标
│   └── favicon.ico
├── src/
│   ├── layouts/
│   │   └── Layout.astro     # 页面 HTML 外壳和全局样式
│   └── pages/
│       └── index.astro      # 简历内容、数据和页面样式
├── astro.config.mjs         # Astro 与 GitHub Pages 配置
├── package.json
└── tsconfig.json
```

## 本地运行

要求 Node.js `22.22.0` 或更高版本。

```bash
npm install
npm run dev
```

开发服务器启动后访问：

```text
http://localhost:4321
```

生产构建：

```bash
npm run build
```

预览生产构建：

```bash
npm run preview
```

## 修改简历内容

主要内容集中在 [`src/pages/index.astro`](./src/pages/index.astro) 的顶部数据区，可以直接修改：

- 姓名、电话、邮箱、民族、年龄、微信
- 教育背景和求职意向
- 核心技能标签和完整技能说明
- 项目名称、技术栈、项目职责、技能描述和项目亮点
- 工作经历和自我评价

替换头像时，将新图片放到：

```text
public/avatar.jpg
```

文件名保持为 `avatar.jpg` 即可。

## 部署到 GitHub Pages

### 三、添加自动部署文件

创建目录和文件：

```bash
mkdir -p .github/workflows
touch .github/workflows/deploy.yml
```

将以下内容写入 `.github/workflows/deploy.yml`：

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Build and upload
        uses: withastro/action@v3
        with:
          node-version: 22

  deploy:
    needs: build
    runs-on: ubuntu-latest

    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}

    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 四、在 GitHub 开启 Pages

进入 GitHub 仓库：

```text
Settings
→ Pages
→ Build and deployment
→ Source
→ GitHub Actions
```

然后提交部署文件：

```bash
git add astro.config.mjs .github/workflows/deploy.yml
git commit -m "配置 GitHub Pages 部署"
git push
```

进入仓库的：

```text
Actions
```

等待工作流完成。

如果你的用户名是 `yourname`，仓库名是 `stale-shepherd`，网站地址一般是：

```text
https://yourname.github.io/stale-shepherd/
```

## 许可证

本项目主要用于个人简历展示和学习参考。未经许可，请勿直接复制个人信息、头像或简历内容用于其他用途。
