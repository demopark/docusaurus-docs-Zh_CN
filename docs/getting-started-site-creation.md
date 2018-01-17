# 创建网站

Docusaurus 的创造，是希望能够让你为开源项目创建一个网站和文档变得非常简单。

在 [安装](getting-started-installation.md) 和 [准备](getting-started-preparation.md) 之后，为文档创建基本网站的许多工作已经完成。

## 网站结构

你的网站结构看起来像下面这样：

```bash
root-of-repo
├── docs
└── website
│   └── blog
│   └── core
│       └── Footer.js
│   └── node_modules
│   └── package.json
│   └── pages
│   └── sidebars.json
│   └── siteConfig.js
│   └── static
```

> 这里假设您已经删除了与 [初始化](getting-started-installation.md) 脚本一起安装的 `.md` 示例文件。

所有的文档文件都应该作为 `.md` 文件放在 `docs` 文件夹中。 任何博客文章都应该在 `blog` 文件夹中。

> 博客帖子的格式必须为 yyyy-mm-dd-your-file-name.md

## 创建您的基本网站

要创建一个功能齐全的网站，您只需要执行几个步骤：

1. 将您的文档以 `.md` 文件的形式添加到 `/docs` 文件夹中，并确保每个文件都有正确的[header](api-doc-markdown.md#文档)。 最简单的标题如下，其中 `id` 是链接名称（例如 `docs/intro.html`），`title` 当然是浏览器页面的标题。

    ```
    ---
    id: intro
    title: 入门
    ---

    这是我的 *新文件内容* ...
    ```

1. 将零个或多个文档添加到 [`sidebars.json`](guides-navigation.md#添加文档到侧边栏) 文件，以便您的文档在侧边栏中呈现，如果您想要显示它们。

  > 如果您不将文档添加到 `sidebars.json` 文件中，那么文档依然被渲染，但只能从其他文档链接到该文档，并使用已知的URL进行访问。

1. 修改 `website/siteConfig.js` 文件来[配置网站](api-site-config.md)，按照 `website/siteConfig.js` 的 [文档](api-site-config.md) 指引。
1. 创建任何的 [自定义页面](guides-custom-pages.md#自定义网站页脚) 和/或 [自定义](guides-custom-pages.md#自定义网站页脚) `website/core/Footer.js` 文件来为你的网站提供页脚。
1. 将网站资源（如图像）放在 `website/static/` 文件夹中。
1. 运行该网站以查看更改的结果。 

  ```
  cd website
  yarn run start # 或 `npm run start`
  # 浏览 http://localhost:3000
  ```
