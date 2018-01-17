# CLI 命令

Docusaurus提供了一组脚本来帮助您生成，运行和部署您的网站。 当使用 Yarn 或 npm 时，可以用 `run` 命令调用这些脚本。 一些常见的命令是：

* [`yarn run start`](api-commands.md#docusaurus-start---port-number): 从本地服务器构建和运行网站
* [`yarn run examples`](api-commands.md#docusaurus-examples-feature): 创建示例配置文件


## 从命令行运行

脚本可以使用 Yarn 或 npm 运行。 如果您已经阅读了入门指南，您可能已经熟悉 `start` 命令。 这个命令告诉 Docusaurus 运行生成站点并启动服务器的 `docusaurus-start` 脚本，通常这样调用它：

```
yarn run start
```

可以使用 npm 来调用相同的脚本：

```
npm run start
```

要运行一个特定的脚本，只需将上面例子中的 `start` 命令替换为与脚本相关的命令即可。

## 使用参数

有些命令支持可选参数。 例如，要在端口 8080 上启动服务器，可以在运行 `start` 时指定 `--port` 参数：

```
yarn run start --port 8080
```

如果你使用 npm 运行 Docusaurus，你仍然可以通过在 `npm run <command>` 和命令参数之间插入 `--` 来使用命令行参数：

```
npm run start -- --port 8080
```

## 配置

这些脚本是作为安装过程的一部分在 `website/package.json` 文件的 `"scripts"` 键下建立的。 如果您需要重新设置，请参考[安装指南](getting-started-installation.md)。

Docusaurus 提供了一些默认映射，允许您按照 node 惯例运行命令。 每次输入 `docusaurus-start`，你都可以输入 `yarn run start` 或 `npm start` 来达到同样的目的。

## 命令

* [docusaurus-build](#docusaurus-build)
* [docusaurus-examples [feature]](#docusaurus-examples-feature)
* [docusaurus-publish](#docusaurus-publish)
* [docusaurus-rename-version <currentVersion> <newVersion>](#docusaurus-rename-version-currentversion-newversion)
* [docusaurus-start [--port <number>]](#docusaurus-start---port-number)
* [docusaurus-version <version>](#docusaurus-version-version)
* [docusaurus-write-translations](#docusaurus-write-translations)

-----

## 参考

### `docusaurus-build`
别名: `build`.

生成静态网站，必要时应用翻译。 在部署之前用于构建网站。

也可以参考 [`docusaurus-start`](api-commands.md#docusaurus-start---port-number).

---

### `docusaurus-examples [feature]`
别名: `examples`

如果没有指定功能，则在您的项目中设置一个最低限度配置的示例网站。这个命令更深入的内容在 [网站准备指南](getting-started-preparation.md)中。指定一个功能 `translations` 或 `versions` 来为该功能生成额外的示例文件。

---

### `docusaurus-publish`
别名: `publish-gh-pages`

[构建](api-commands.md#docusaurus-build)，然后将静态网站部署到 GitHub 页面。 此命令在 Circle CI 的部署步骤中运行，因此需要定义一些环境变量：

以下通常由用户在 CircleCI 的 `config.yml` 文件中手动设置。

 - `GIT_USER`: 与部署提交相关联的 git 用户。
 - `USE_SSH`: 是否使用 SSH 而不是 HTTPS 连接到 GitHub 仓库。

示例

 ```bash
 GIT_USER=docusaurus-bot USE_SSH=true yarn run publish-gh-pages
 ```

以下是在构建过程中由 [CircleCI 环境](https://circleci.com/docs/1.0/environment-variables/) 设置的。

 - `CIRCLE_BRANCH`: 与触发 CI 运行的提交相关联的 git 分支。
 - `CI_PULL_REQUEST`: 如果当前的 CI 运行是由提交请求中的提交触发的，那么预计会实现。

你应该在 `siteConfig.js` 中分别设置为 `organizationName` 和 `projectName`。 如果它们未在您的站点配置中设置，则会回退到[CircleCI环境](https://circleci.com/docs/1.0/environment-variables/)。

 - `CIRCLE_PROJECT_USERNAME`: 承载git仓库的 GitHub 用户名或组织名称，例如 "facebook"。
 - `CIRCLE_PROJECT_REPONAME`: git repo的名字，例如 "Docusaurus"。

您可以在[发布指南](getting-started-publishing.md)中了解更多关于使用 CircleCI 配置自动部署的信息。

---

### `docusaurus-rename-version <currentVersion> <newVersion>`
别名: `rename-version`

将文档的现有版本重命名为新的版本名称。

参考 [版本化指南](guides-versioning.md#重命名现有版本) 来学习更多.

---

### `docusaurus-start [--port <number>]`
别名: `start`.

该脚本将构建静态网站，必要时应用翻译，然后启动本地服务器。 该网站将默认从端口 3000 提供。

---

### `docusaurus-version <version>`
别名: `version`

生成文档的新版本。 这将导致您的网站的新副本生成并存储在其自己的版本文件夹中。 用于捕获映射到特定版本的软件的 API 文档的快照。 接受任何字符串作为版本号。

参考 [版本化指南](guides-versioning.md) 来学习更多.

---

### `docusaurus-write-translations`
别名: `write-translations`

将需要翻译成 `website/i18n/en.json` 文件的字符串写入英文。 脚本将遍历 `website/pages/en` 中的每个文件，并通过 `siteConfig.js` 文件和其他配置文件读取英文字符串，然后在 Crowdin 上进行翻译。 请参阅[翻译指南](guides-translation.md)了解更多信息。
