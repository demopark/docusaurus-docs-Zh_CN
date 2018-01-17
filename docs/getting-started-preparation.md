# 准备网站

[安装 Docusaurus](getting-started-installation.md) 之后，您现在有一个框架可以为您特定的网站工作。 通过一些更改，您可以通过在本地运行网站来验证 Docusaurus 是否已正确安装。

## 目录结构

如[安装 Docusaurus](getting-started-installation.md) 之后所示，初始化脚本创建了一个类似于以下内容的目录结构：

```bash
root-of-repo
├── docs-examples-from-docusaurus
│   └── doc1.md
│   └── doc2.md
│   └── doc3.md
│   └── exampledoc4.md
│   └── exampledoc5.md
└── website
│   └── blog-examples-from-docusaurus
│       └── 2016-03-11-blog-post.md
│       └── 2017-04-10-blog-post-two.md
│   └── core
│       └── Footer.js
│   └── node_modules
│   └── package.json
│   └── pages
│   └── sidebars.json
│   └── siteConfig.js
│   └── static
```

- `website/core/Footer.js` 文件是一个 React 组件，充当 Docusaurus 生成的网站的页脚，应该由用户自定义。
- `website/blog-examples-from-docusaurus` 文件夹包含用 markdown 编写的博客文章的例子。
- `docs-examples-from-docusaurus` 文件夹包含用 markdown 编写的示例文档文件。
- `website/pages` 文件夹包含该网站的示例顶级页面。
- `website/static` 文件夹包含示例网站使用的静态资源。
- `website/siteConfig.js` 文件是 Docusaurus 使用的主要配置文件。

你需要保留 `website/siteConfig.js` 和 `website/core/Footer.js` 文件，但是可以随意编辑它们。

你应该保留 `website/pages` 和 `website/static` 文件夹，但可以如你所愿的改变其内容。 最低限度，你应该有一个在 `website/pages` 内的 `en/index.js` 或 `en/index.html` 文件和一个图像用作 `website/static` 内的标题图标。

`website/blog-examples-from-docusaurus` 和 `docs-examples-from-docusaurus` 文件夹包含示例博客和文档的 markdown 文件。 如下文所示，当您确认示例网站正确运行时，如果您希望使用这些文件运行 Docusaurus，则需要分别将文件夹重命名为`website/blog` 和 `docs`。

## 验证安装

运行 Docusaurus 初始化脚本 `docusaurus-init` 后，会生成一个可运行的示例网站，以此为基础开发您的网站。

1. 在根目录, 重命名 `docs-examples-from-docusaurus` 为 `docs`.
1. `cd website`
1. 重命名 `blog-examples-from-docusaurus` 为 `blog`.
1. 通过 `yarn start` 或 `npm start` 运行本地 web 服务器.
1. 通过 http://localhost:3000 访问示例网站。 你应该看到浏览器加载的示例网站。

![](/img/getting-started-preparation-verify.png)
