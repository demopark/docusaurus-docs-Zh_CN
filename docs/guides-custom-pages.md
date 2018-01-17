# 自定义页面

您可以将网页添加到您的网站，而不是作为标准文档或博客 markdown 文件的一部分。 你可以通过在 `website/pages` 目录中添加 `.js` 文件来实现。 这些文件是 [React](https://reactjs.org/) 组件，并调用 `render()` 来创建它们，由CSS类等支持。

## 自定义主页

开始自定义主页的最简单方法是使用运行 [Docusaurus 初始化脚本](getting-started-installation.md) 时 [创建](getting-started-site-creation.md) 的示例网站。

你可以 [启动](getting-started-preparation.md#验证安装) 你的本地服务器并跳转到 `http://localhost:3000`  来查看示例主页的样子。 从那里，编辑 `website/pages/en/index.js` 文件及其各个组件以使用您想要的项目的图像和文本。

## 添加其它自定义页面

Docusaurus 在 `website/pages/en` 目录中提供了一些简单的示例页面，包括 `index.js`，`users.js` 和 `help.js`。 这些是展示如何为 Docusaurus 创建自定义页面的很好的例子。

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
│       └── index.js
│       └── users.js
│       └── help.js
│   └── sidebars.json
│   └── siteConfig.js
│   └── static
```

当然，你也可以自由地写你自己的网页。 强烈建议您至少有一个索引页面，而没有提供的页面是强制性的以包含在您的网站中。 有关如何使用提供的组件或包括您自己的更多信息可以在[这里](api-pages.md)找到。 有关如何链接到页眉导航栏中的不同页面的信息可以在[这里](guides-navigation.md)找到。

> 如果你想让你的页面显示在你的导航头文件中，你需要更新 `siteConfig.js` 来添加到 `headerLinks` 元素。 例如 `{ page: "about-slash", label: "About/"}`

## 添加静态页面

也可以使用静态 `.html` 文件，但默认情况下，它们不包括 Docusaurus 的页眉，页脚或样式。 这些可以像其他 [静态资源](api-pages.md#使用静态资源) 一样添加到 `static` 文件夹中。 或者，它们可以放在 `pages` 文件夹中，而不是从 React 中渲染。

如果你想使用 Docusaurus 的样式表，你可以在 `${baseUrl}css/main.css` 中访问它。 如果你想为这些静态页面使用单独的 css，你可以通过将它们添加到 `siteConfig.js` 中的 `siteConfig.separateCss` 字段来排除它们与 Docusaurus 的样式的关联。

## 自定义网站页脚

从运行 [Docusaurus 初始化脚本](getting-started-installation.md) 时 [创建](getting-started-site-creation.md) 的示例 `core/Footer.js` 文件开始，编辑页脚以包含您网站上的任何链接或其他您希望拥有的网站。

所提供的示例有三列，左侧有一个页脚图像，Facebook 的开放源代码标识和版权在底部。 如果您的项目不是 Facebook 开源项目，请删除徽标和版权。 当然，您也可以随意创造页脚，让它看起来成为您想要的样子！

可能提供的链接的一些建议：Docs，API，Twitter，Discord，Facebook groups，Stack Overflow，GitHub等

您的页脚将自动应用到您网站上的所有页面，包括文档和博客文章。 唯一的例外是你所包含的任何静态 html 页面。

如果你不想为你的站点添加页脚，把 `core/Footer.js` 的 `render` 函数改为返回 `null`。 例如:

```jsx
const React = require("react");

class Footer extends React.Component {
  render() {
    return null;
  }
}

module.exports = Footer;
```
