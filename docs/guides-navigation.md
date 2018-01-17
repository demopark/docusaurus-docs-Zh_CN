# 导航和侧边栏

## 引用网站文档

如果你想在 `docs` 文件夹中引用另一个文档（或者你通过[可选 `customDocsPath`](api-site-config.md#可选字段)路径站点配置选项设置的位置），那么你只需要使用你想引用的文档名称。

例如，如果你在 `doc2.md` 中，而你想引用 `doc1.md`：

```
这里引用了一个 [文档](doc1.md).
```

> Docusaurus 目前不支持嵌套文件夹中的文件; 只能是在一个平面文件结构中。 我们正在考虑添加对嵌套文件夹的支持。

## 文档如何链接

`docs` 中的新 markdown 文件将在网站上显示为页面。 这些文档的链接首先通过在每个文档的头部使用 `id` 来创建。 如果没有 `id` 字段，那么文件的名称将作为链接名称。

例如，创建诸如 "docs/getting-started.md" 之类的空文件将使新页面 URL 成为 `/docs/getting-started.html`。

假设您将其添加到您的文档中：

```
---
id: intro
title: 入门
---

这是文档的 *新内容*...
```

如果您在文件的标记标题中设置了 `id` 字段，那么文档将从 `/docs/intro.html` 形式的 URL 访问。

> 您需要一个 `id` 字段才能将文档添加到侧边栏。

## 添加文档到侧边栏

很多时候，您将需要添加一个文档到侧边栏，这个侧边栏将与网站顶部导航栏中的一个标题相关联。 最常见的补充工具栏，以及在 Docusaurus 初始化时安装的工具栏是 `docs` 工具栏。

> "docs" 只是一个名字。 它没有继承的意义。 你可以随意更改。

您可以在 `website/sidebars.json` 文件中配置侧边栏的内容以及文档的顺序。

> 在将文档添加到 `website/sidebars.json` 之前，只能通过直接的URL访问它们。 该文档不会显示在任何侧边栏。

在 `sidebars.json` 中，将在文档头中使用的 `id` 添加到现有的侧边栏/类别中。 在下面的情况下，`docs` 是侧边栏的名称，`Getting Started` 是侧边栏中的一个类别。

```
{
  "docs": {
    "Getting Started": [
      "getting-started"
```

或者你可以在侧边栏中创建一个新的类别：

```
{
  "docs": {
    ...
    "My New Sidebar Category": [
      "getting-started"
    ],
    ...
```

### 添加新侧边栏

您也可以将文档放在新的侧边栏中。 在下面的例子中，我们在 `sidebars.json` 里面创建一个名为 `My Example Category` 的类别为 `examples-sidebar` 的工具栏，里面包含一个 `id` 为 `my-examples` 的文档。

```
{
  "examples-sidebar": {
    "My Example Category": [
      "my-examples"
    ],
  },
  ...
```

重要的是要注意，直到你[从 `"example-sidebar"` 侧边栏添加一个文档到导航栏](#添加到网站导航栏)，它将会被隐藏。

## 添加到网站导航栏

要展开侧边栏，您需要将可点击的标签添加到网站顶部的网站导航栏中。 您可以添加文档，页面和外部链接。

### 添加文档

通过将其[添加](#添加新侧边栏)到 `sidebars.json`，为该网站创建一个新的侧边栏后，您可以通过编辑 `siteConfig.js` 的 `headerLinks` 字段来从顶部导航栏中展开新的侧边栏。

```
headerLinks: [
  ...
  { doc: 'my-examples', label: 'Examples' },
  ...
],
```

一个名为 `Examples` 的标签将被添加到网站导航栏中，当您在网站顶部点击它时，将会显示 `examples-sidebar`，默认文档将是 `my-examples`。

### 添加自定义页面

要将自定义页面添加到网站导航栏，可将条目添加到 `siteConfig.js` 的 `headerLinks` 中。 例如，如果我们在 `website/pages/help.js` 中有一个页面，我们可以通过添加以下内容来链接到它：

```
headerLinks: [
  ...
  { page: 'help', label: 'Help' },
  ...
],
```

一个名为 `Help` 的标签将被添加到站点导航栏中，当您在站点顶部点击它时，将显示 `help.js` 页面的内容。

### 添加外部链接

自定义链接可以通过 `siteConfig.js` 中的以下条目添加到网站导航栏中：

```
headerLinks: [
  ...
  { href: 'https://github.com/facebook/Docusaurus', label: 'GitHub' },
  ...
],
```

一个名为 `GitHub` 的标签将被添加到站点导航栏中，当您在站点顶部点击它时，外部链接的内容将被显示。

> 要在新选项卡中打开外部链接，请在标题链接配置中提供一个 `external: true` 标志。

## 网站导航栏定位

在网站顶部的网站导航栏中显示搜索和语言下拉列表元素时，您的控制权限有限。

### 搜索

如果在您的网站上启用搜索，您的搜索栏将显示在您的链接的右侧。 如果您想要在搜索栏中的链接之间添加一个搜索条目，在 `headerLinks` 配置数组中：

```
headerLinks: [
  { doc: 'foo', label: 'Foo' },
  { search: true },
  { doc: 'bar', label: 'Bar' },
],
```

### 语言下拉菜单

如果在您的网站上启用了翻译，则语言下拉菜单将显示在您的链接的右侧（如果启用搜索，则会显示在搜索栏的左侧）。 如果要将语言选择放在标题中的链接之间，请在 `headerLinks` 配置数组中添加一个语言条目：

```
headerLinks: [
  { doc: 'foo', label: 'Foo' },
  { languages: true },
  { doc: 'bar', label: 'Bar' },
],
```
