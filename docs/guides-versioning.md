# 版本化

您可以使用 `version` 脚本根据 `docs` 文件夹中的最新内容来剪切新的文档版本。 即使 `docs` 文件夹中的文档发生变化，该特定的文档集也将保留并可访问。

## 如何创建新版本

运行以下脚本以生成并列出所有网站版本的初始版本页面：

```
yarn examples versions
```

这将创建以下文件：

```
pages/en/versions.js
```

您稍后可以编辑此文件以自定义如何显示版本。

如果脚本不存在，请将以下脚本添加到 `package.json` 文件中：

```json
...
"scripts": {
  "version": "docusaurus-version"
},
...
```

用您希望创建的版本的命令行参数运行脚本。 例如：

```bash
yarn run version 1.0.0
```

这将保留当前在 `docs` 文件夹中的所有文档，并使它们作为版本 `1.0.0` 的文档提供。

例如，如果您使用1.0.0作为版本号运行版本脚本，则版本1.0.0将被视为您项目的最新版本。 该站点将显示标题旁标题的版本号。 此版本号链接到您之前创建的版本页面。

`docs` 文件夹中的文档将被认为是 `next` 版本的一部分，并使它们可用。例如在 URL `docs/next/doc1.html` 处，最新版本的文档使用 url `docs/doc1.html`。

用 `yarn run version 2.0.0` 再次运行脚本将会创建一个 `2.0.0` 版本，使得2.0.0版本成为最新版本的文档。 来自`1.0.0`版本的文档将使用 URL `docs/1.0.0/doc1.html`，而 `2.0.0` 将使用 `docs/doc1.html`。

## 版本化模式

您可以以任何您想要的格式创建版本号，只要与现有版本不匹配，就可以使用任何版本号创建新版本。 版本排序由创建版本的顺序决定，与编号的方式无关。

## 存储每个版本的文件

版本化的文档被放置在 `website/versioned_docs/version-${version}` 中，其中 `${version}` 是你提供 `version` 脚本的版本号。

每个版本化文档的 markdown 标题都会通过将 id frontmatter 字段重命名为 `original_id`，然后使用 `"version-${version}-${original_id}"` 作为实际的 `id` 字段的值来更改。

版本化的边栏被复制到 `website/versioned_sidebars` 中，并被命名为 `version-${version}-sidebars.json`。

一个 `website/versions.json` 文件是在您第一次剪切版本时创建的，并被 Docusaurus 用来检测存在的版本。 每次添加新版本时，都会将其添加到 `versions.json` 文件中。

如果您希望更改以前版本的文档，则可以访问相应版本的文件。

## 回退功能

每次指定新版本时，只有 `docs` 文件夹和侧边栏文件中与最新版本文件不同的文件才会被复制。 如果版本之间没有变化，Docusaurus 将使用该文件的最新版本的文件。

例如，具有原始 id `doc1` 的文档存在于最新版本 `1.0.0` 中，并且具有与 `docs` 文件夹中具有id `doc1` 的文档相同的内容。 当创建一个新版本 `2.0.0` 时，`doc1` 文件不会被复制到 `versioned_docs/version-2.0.0/` 中。 仍然会有一个 `docs/2.0.0/doc1.html` 的页面，但它将使用版本为 `1.0.0` 的文件。

## 重命名现有版本

要将现有版本号重命名为其他内容，请首先确保以下脚本位于 `package.json` 文件中：

```json
...
"scripts": {
  "rename-version": "docusaurus-rename-version"
},
...
```

使用命令行参数运行脚本，当前版本名称，然后是新版本名称。 例如：

```bash
yarn run rename-version 1.0.0 1.0.1
```

## 版本化和翻译

如果你想使用版本化和翻译功能，应该设置 `crowdin.yaml` 文件来上传和下载来自 Crowdin 的版本化文档以进行翻译。 翻译后的版本化文件将进入文件夹`translated_docs/${language}/version-${version}/`。 有关更多信息，请查看[翻译指南](guides-translation.md)。
