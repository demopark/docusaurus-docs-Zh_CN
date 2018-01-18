# siteConfig.js

网站配置的很大一部分是通过编辑 `siteConfig.js` 文件完成的。

## 用户展示

`users` 数组用于存储要在您的站点上显示的每个项目/用户的对象。 目前这个字段被提供给 `pages/en/index.js` 和 `pages/en/users.js` 文件使用。 每个用户对象应该有 `caption`，`image`，`infoLink` 和 `pinned` 字段。`caption` 是当某人悬停在该用户的 `image` 上时显示的文本，而 `infoLink` 则是点击该图片将会某人谁去哪。 `pinned` 字段决定它是否显示在 `index`页面上。

目前这个 `users` 数组只用于 `index.js` 和 `users.js` 示例文件。 如果您不希望在 `index` 页面上显示用户页面或显示用户，则可以删除此部分。

## siteConfig 字段

`siteConfig` 对象包含你的网站的大部分配置设置。

### 必选字段

`title` - 网站的标题

`tagline` - 网站的标语

`url` - 网站的 URL

`baseUrl` - 网站的 baseUrl

`projectName` - 项目名称. 这必须匹配你的 GitHub 仓库项目名称（区分大小写）。

`noIndex` - 布尔。 如果为真，Docusaurus 会礼貌地要求爬虫和搜索引擎避免索引您的网站。 这是用 header 标签完成的，所以只适用于文档和页面。 不会试图隐藏静态资源。 这是一个尽最大努力的要求。 恶意抓取工具仍然可以继续为您的网站编制索引。

`headerLinks` - 将在标题导航栏中使用的链接。 每个对象的 `label` 字段将成为链接文本，也将被翻译为每种语言。

使用示例:

```js
headerLinks: [
  // 链接到当前 语言/版本 并且 ID 为 doc1 的文档
  { doc: "doc1", label: "Getting Started" },
  // 使用当前语言链接到 pages/en/help.js 中找到的页面，如果不存在，则使用 pages/help.js。
  { page: "help", label: "Help" },
  // 链接到 href 目的地
  { href: "https://github.com/", label: "GitHub" },
  // 由 Docusaurus (${baseUrl}blog) 生成的博客链接
  { blog: true, label: "Blog" },
  // 判断链接中的搜索栏的位置
  { search: true },
  // 判断链接中的语言下拉菜单的位置
  { languages: true }
],
```
`headerIcon` - 标题导航栏中使用的图标的 URL。

`favicon` -  网站 favicon 的 URL。

`colors` - 网站的颜色配置。

  - `primaryColor` 是用于标题导航栏和侧边栏的颜色。
  - `secondaryColor` 是用于当站点窗口很窄时（包括在移动设备上）在页眉导航栏的第二行中看到的颜色。
  - 也可以添加自定义颜色配置。 例如，如果用指定为 `$myColor` 的颜色添加用户样式，则将 `myColor` 字段添加到 `colors` 将可以让您轻松配置此颜色。

`copyright` - 网站页脚和订阅内的版权字符串

### 可选字段

默认情况下，Docusaurus 希望您的文档位于名为 `docs` 的目录中。 该目录与 `website` 目录处于同一级别（即不在 `website` 目录内）。 您可以使用此字段指定文档的自定义路径。**请注意，所有文档的*.md文件都必须位于平面层次结构中。 不可以使用文件嵌套目录**。

```js
customDocsPath: "docs/site"
```

```js
customDocsPath: "website-docs"
```

`useEnglishUrl` - 如果你没有启用 [翻译](guides-translation.md)（例如，通过一个 `languages.js` 文件），那么仍然需要一个 `/docs/en/doc.html` 形式的链接 `en`），将其设置为 `true`。

`organizationName` - 托管此项目的组织或用户的 GitHub 用户名。 发布脚本使用它来确定您的 GitHub 页面网站的托管位置。

`editUrl` - 用于编辑文档的 URL，用法示例：`editUrl + 'en/doc1.md'`。 如果此字段被省略，则每个文档将不会有 "Edit this Doc" 按钮。

`users` - 前面提到的 `users` 数组。

`disableHeaderTitle` - 可以选择禁止在标题图标旁边显示标题。 排除此字段以保持标题正常，否则设置为 `true`。

`disableTitleTagline` - 禁止在主页标题中显示标语的选项。 排除此字段可将页面标题保留为 `Title • Tagline`。 设置为 `true`，使页面标题只是 `Title`。

`separateCss` - 其中任何 `css` 文件不会被处理并连接到 Docusaurus 的样式文件夹。 这是为了支持静态的 `html` 页面，它可以与 Docusaurus 样式完全独立的分开。

`footerIcon` - 页脚图标的 URL。 目前在 `core/Footer.js` 文件中使用，但是可以从该文件中删除。

`translationRecruitingLink` - 当启用除英文以外的语言时，语言选择的 `Help Translate` 选项卡的 URL。 这可以包括你正在使用的翻译，但不一定都是这样。

`algolia` - Algolia 搜索集成信息。 如果该字段被排除，搜索栏将不会出现在标题中。

`gaTrackingId` - Google Analytics 跟踪 ID 来跟踪页面浏览量。

`facebookAppId` - 如果你想在你博客文章底部的 Facebook Like/Share 按钮，提供一个[Facebook应用程序ID](https://www.facebook.com/help/audiencenetwork/804209223039296)，并且按钮将显示在所有的博客文章。

`twitter` - 如果你想让一个 Twitter 的社交按钮出现在你的博客文章的底部，请将其设置为 `true`。

`highlight` - [语法突出显示](api-doc-markdown.md) 参数:

 - `theme` 是语法突出显示时 Highlight.js 使用的主题的名称。 你可以在这里找到[支持的主题列表](https://github.com/isagalaev/highlight.js/tree/master/src/styles)。
 - `version` 指定要使用的特定版本的 Highlight.js。
 - `hljs` 通过将 Highlight.js 的实例传递给此处指定的函数来提供一个接口，从而允许注册语法突出显示的其他语言。
 - `defaultLang` 定义一个默认的语言。 如果没有在代码块的顶部指定它，将会使用它。 你可以在这里找到[支持的语言列表](https://github.com/isagalaev/highlight.js/tree/master/src/languages)。

`markdownPlugins` - 一个由 Remarkable 加载的插件数组，Docusaurus 使用的 markdown 解析器和渲染器。 该插件将接收对 Remarkable 实例的引用，允许定义自定义分析和呈现规则。

`wrapPagesHTML` - 布尔标志来指示 `/pages` 中的 `html` 文件是否应该用网站页眉和页脚的Docusaurus 样式进行封装。 这个功能是实验性的，依赖于文件是 `html` 片段而不是完整的页面。 它插入的 `html` 文件的内容没有额外的处理。 默认为 `false`。

`scripts` - 要加载的 JavaScript 源数组。 脚本标签将被插入到 HTML 头中。

`stylesheets` - 要加载的 CSS 源数组。 链接标签将被插入到 HTML 头中。

`cname` - 您的网站的 CNAME。 当您的网站建立时，它会进入一个 `CNAME` 文件。

如果用户希望跨不同文件提供一些数据，用户也可以添加自己的自定义字段。

## siteConfig.js 全字段示例

```
const users = [
  {
    caption: "User1",
    image: "/test-site/img/docusaurus.svg",
    infoLink: "https://www.example.com",
    pinned: true
  }
];

const siteConfig = {
  title: "Docusaurus",
  tagline: "Generate websites!",
  url: "https://docusaurus.io",
  baseUrl: "/",
// 对于 github.io 类型的 URLS，你可以将 url 和 baseUrl 结合起来：
// url: "https://reasonml.github.io",
// url: "/reason-react/",
  organizationName: "facebook",
  projectName: "docusaurus",
  noIndex: false,
  headerLinks: [
    { doc: "doc1", label: "Docs" },
    { page: "help", label: "Help" },
    { search: true },
    { blog: true }
  ],
// 对于顶部导航栏中没有标题链接 -> headerLinks: [],
  headerIcon: "img/docusaurus.svg",
  favicon: "img/favicon.png",
  colors: {
    primaryColor: "#2E8555",
    secondaryColor: "#205C3B"
  },
  editUrl: "https://github.com/facebook/docusaurus/edit/master/docs/",
  users,
  disableHeaderTitle: true,
  disableTitleTagline: true,
  separateCss: ["static/css/non-docusaurus", "static/assets/separate-css"],
  footerIcon: "img/docusaurus.svg",
  translationRecruitingLink:
    "https://crowdin.com/project/docusaurus",
  algolia: {
    apiKey:
      "0f9f28b9ab9efae89810921a351753b5",
    indexName: "github"
  },
  gaTrackingId: "U-A2352",
  highlight: {
    theme: 'default'
  },
  markdownPlugins: [
    function foo(md) {
      md.renderer.rules.fence_custom.foo = function(tokens, idx, options, env, instance) {
        return '<div class="foo">bar</div>';
      }
    }
  ],
  scripts: [ "https://docusaurus.io/slash.js" ],
  stylesheets: [ "https://docusaurus.io/style.css" ],
  facebookAppId: "1615782811974223",
  twitter: "true"
};

module.exports = siteConfig;
```
