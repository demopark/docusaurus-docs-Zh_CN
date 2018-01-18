# 页面和样式

Docusaurus 支持在 `website/pages` 文件夹中将页面编写为 React 组件，该文件夹将与网站的其他部分共享相同的页眉，页脚和样式。

## 页面的 URL

 `website/pages` 中的任何 `.js` 文件将使用 "pages" 之后的文件路径呈现为静态 html。 `website/pages/en` 中的文件也将被复制到 `pages` 中，并将覆盖 `pages` 中的任何同名文件。 例如，`website/pages/en/help.js`  文件的页面可以在 URL `${baseUrl}en/help.js` 以及 URL `${baseUrl}help.js` 中找到。其中 `${baseUrl}` 是在 [siteConfig.js 文件](api-site-config.md)中设置的 `baseUrl` 字段。

## 页面请求路径

Docusaurus 提供了一些有用的 React 组件供用户编写他们自己的页面，可以在 `CompLibrary` 模块中找到。这个模块是在 `node_modules/docusaurus` 中作为 Docusaurus 的一部分提供的，所以为了访问它，在渲染为静态 html 时，`pages` 文件夹中的页面被临时复制到 `node_modules/docusaurus` 中。如示例文件所示，这意味着位于 `pages/en/index.js` 的用户页面使用 `"../../core/CompLibrary.js"` 的 require 路径导入提供的组件。

这对用户意味着如果你想使用 `CompLibrary` 模块，请确保 require 路径设置正确。例如，在 `page/mypage.js` 中的一个页面将使用一个路径 `"../core/CompLibrary.js"`。

如果你想在你的网站文件夹中使用你自己的组件，可以使用 `process.cwd()` 来引用 `website` 文件夹来构建 require 路径。例如，如果你添加一个组件到 `website/core/mycomponent.js`，你可以使用 require 路径，`"process.cwd() + /core/mycomponent.js"`。

## 提供的组件

Docusaurus 在 `CompLibrary` 中提供了以下组件：

### `CompLibrary.MarkdownBlock`

一个 React 组件，用于解析 markdown 并呈现给 HTML。

示例:

```jsx
const MarkdownBlock = CompLibrary.MarkdownBlock;

<MarkdownBlock>[Markdown syntax for a link](http://www.example.com)</MarkdownBlock>
```

### `CompLibrary.Container`

使用 Docusaurus 样式的 React 容器组件。 有可选的填充和背景颜色属性，您可以配置。

填充选择: `all`, `bottom`, `left`, `right`, `top`.  
背景选择: `dark`, `highlight`, `light`.

示例:

```jsx
<Container padding={["bottom", "top"]} background="light">
  ...         
</Container>
```

### `CompLibrary.GridBlock`

一个 React 组件来组织文本和图像。

 `align` 属性确定文本对齐。 文本对齐方式默认为 `left`，可以设置为 `center` 或 `right`。

`layout` 属性确定每个 GridBlock 的列部分的数量。 `layout ` 默认为 `twoColumn`，也可以设置为 `threeColumn` 或 `fourColumn`。

`contents` 属性是一个包含 GridBlock 每个部分内容的数组。 每个内容对象可以有以下字段：

- `content` 是从 markdown 解析的章节文本
- `image` 显示图片的路径
- `imageAlign` 字段用于图像对齐，相对于文本，默认为 `top` ，可以设置为 `bottom`, `left`, 或 `right`
- `title` 是从 markdown 解析的要显示的标题
- `imageLink` 是点击图像链接目的地的

示例:

```
<GridBlock
  align="center"
  contents={[
    {
      content: "Learn how to use this project",
      image: siteConfig.baseUrl + "img/learn.png",
      title: `[Learn](${siteConfig.baseUrl}docs/tutorial.html)`,
      imageLink: siteConfig.baseUrl + "docs/tutorial.html"
    },
    {
      content: "Questions gathered from the community",
      image: siteConfig.baseUrl + "img/faq.png",
      imageAlign: "top",
      title: "Frequently Asked Questions"
    },
    {
      content: "Lots of documentation is on this site",
      title: "More"
    }
  ]}
  layout="threeColumn"
/>
```

在[生成的示例文件](getting-started-preparation.md) 以及 Docusaurus 自己的网站设置 repo 中，可以找到更多关于如何使用这些组件的例子。

## 翻译字符串

启用翻译后，`website/pages/en` 内的任何页面都将被翻译为所有已启用的语言。 非英文网页的网址将使用 `languages.js` 文件中指定的语言标记。 例如。 法语页面 `website/pages/en/help.js` 的网址可以在 `${baseUrl}fr/help.html` 处找到。

在编写要翻译的页面时，可以将任何要翻译的字符串包装在 `<translate>` 标签中。 例如

```jsx
<p><translate>I like translations</translate></p>
```

您还可以提供一个可选的说明属性，为翻译人员提供上下文。 例如

```jsx
<a href="/community">
  <translate desc="footer link to page referring to community github and slack">Community</translate>
</a>
```

添加以下require语句：

```js
const translate = require("../../server/translate.js").translate;
```

请注意，这个路径对 `pages/en` 里面的文件是有效的，如果文件位于不同的位置，就应该相应地进行调整，正如[上面](#页面请求路径)讨论的那样。

## 使用静态资源

静态资源应该放在 `website/static` 文件夹中。 他们可以通过他们的路径访问，不包括 "static"。 例如，如果该网站的 `baseUrl` 为 "/docusaurus/"，`website/static/img/logo.png` 中的图片可用 `/docusaurus/img/logo.png`。

## 样式

您应该使用 `siteConfig` 中的 `colors` 字段来配置您的网站的主要，辅助和代码块颜色，如[这里](api-site-config.md)所示。 你也可以像 `siteConfig` 文档中描述的那样配置其他颜色。

您可以通过在 `website/static` 文件夹中的任何位置添加自定义样式。 您在 `static` 文件夹中提供的任何 `.css` 文件将连接到 Docusaurus 提供的样式的末尾，允许您根据需要添加或覆盖 Docusaurus 默认样式。

一个简单的方法来找出你想要覆盖或添加到什么类是[本地启动您的服务器](api-commands.md)，并使用您的浏览器的检查元素工具。
