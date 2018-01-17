# 安装指南

Docusaurus 是从全新设计的，易于安装和使用，让您的网站能够快速运行。 要安装 Docusaurus，我们已经创建了一个简单的脚本，可以为您提供所有的基础架构设置：

1. 进入你将要创建文档的 GitHub repo 目录的根目录。
2. `yarn global add docusaurus-init` 或 `npm install --global docusaurus-init`
3. `docusaurus-init`

除了以前存在的文件和目录，您的根目录现在将包含类似于以下的结构：

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

> 如果您不想全局安装 init 脚本，则可以在本地安装，然后通过 `npx docusaurus-init` 或通过 `./node_modules/.bin/docusaurus-init` 创建的 `node_modules` 目录运行。 运行脚本后，您可能需要删除已创建的 `package.json` 文件和 `node_modules` 目录。
