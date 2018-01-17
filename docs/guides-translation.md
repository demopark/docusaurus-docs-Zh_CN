# 翻译 & 本地化

Docusaurus允许使用 [Crowdin](https://crowdin.com/) 轻松实现翻译功能。 以英文撰写的文档文件将上传到 Crowdin，由社区内的用户进行翻译。 使用英文字符串编写的顶层页面可以通过在 `<translate>` 标签中包装要翻译的任何字符串来翻译。 其他标题和标签也将被找到并正确翻译。

## Docusaurus 翻译配置

要用 Docusaurus 生成用于翻译的示例文件，请使用命令行参数 `translations` 运行 `examples` 脚本：

```
npm run examples translations
```

或

```
yarn examples translations
```

这将创建以下文件：

```
pages/en/help-with-translations.js
languages.js
../crowdin.yaml
```

`pages/en/help-with-translations.js` 文件包含由 `examples` 脚本生成的相同的起始帮助页面，但现在包含了翻译标签。

`languages.js` 文件告诉 Docusaurus 你想为你的网站启用什么语言。 默认情况下，我们希望启用英文。

`crowdin.yaml` 文件用于配置 crowdin 集成，并将其复制到您的 docusaurus 项目库。 如果您的docusaurus 项目驻留在 `/project/website` 中，则 `crowdin.yaml `将被复制到 `/project/crowdin.yaml` 中。

## 翻译现有文档

您的文档文件不需要更改或移动来支持翻译。 他们将被上传到 Crowdin 直接翻译。

## 在页面上启用翻译

页面允许您自定义页面或帮助页面等页面的布局和特定内容。

包含要翻译的文字的页面应放置在 `website/pages/en` 文件夹中。

将需要翻译的字符串封装在一个 `<translate>` 标签中，并在文件的顶部添加下面的 `require` 语句：

```jsx
...
const translate = require("../../server/translate.js").translate;
...
<h2>
  <translate>This header will be translated</translate>
</h2>
...
```

您还可以包含一个可选的 description 属性，为翻译者提供更多关于如何翻译字符串的上下文：

```jsx
<p>
  <translate desc="flower, not verb">Rose</translate>
<p>
```

## 提取字符串到翻译

必须提取本地化页面内的字符串并提供给 Crowdin。

将以下脚本添加到您的package.json文件中：

```json
...
"scripts": {
  "write-translations": "docusaurus-write-translations"
},
...
```

运行脚本将生成一个 `website/i18n/en.json` 文件，其中包含所有将从英文翻译成其他语言的字符串。

该脚本将包括来自以下地方的文本：

- 文档 markdown header 中的 `title` 和 `sidebar_label` 字符串
- `sidebars.json` 中的类别名称
- 在 `siteConfig.js` 中的 tagline
- `siteConfig.js` 中的 header link 的 `label ` 字符串
- 在 `pages` 内的任何 `.js` 文件中的 `<translate>` 标签中包装的字符串

## 如何获得翻译的字符串

Docusaurus 本身不会从一种语言翻译到另一种语言。 相反，它集成了 [Crowdin](https://crowdin.com/) 来上传翻译，然后从 Crowdin 下载适当翻译的文件。

## Docusaurus 如何使用字符串翻译

本节介绍 Docusaurus 中的翻译如何工作。

### 字符串

Docusaurus 网站有很多字符串需要本地化。 但是，维持在网站中使用的字符串列表可能是很费力的。 Docusaurus 通过集中字符串来简化这一点。

例如，标题导航可以链接到“主页”或“博客”。 在页面的标题和侧边栏中找到的这个和其他字符串被提取并放置到 `i18n/en.json` 中。 当你的文件被翻译成西班牙语时，一个 `i18n/es-ES.json` 文件将从 Crowdin 下载。 然后，当生成西班牙语页面时，Docusaurus 将从相应的本地化字符串文件中替换相应字符串的英文版本（例如，在启用西班牙语的网站“Help”中将变成“Ayuda”）。

### Markdown 文件

对于文档文件本身，下载这些文件的翻译版本，然后通过适当的版面模板进行渲染。

### 其它页面

对于其他页面，Docusaurus 会自动将所发现的所有 `<translate>` 标签转换为函数调用，从相应的本地化文件 _`locale.json`_ 返回翻译后的字符串。

## Crowdin

Crowdin是一家提供翻译服务的公司。 对于开源项目，Crowdin 提供免费的字符串翻译。

在 [Crowdin](https://crowdin.com/) 上创建您的翻译项目。 您可以使用[Crowdin的指南]](https://support.crowdin.com/translation-process-overview/)来了解有关翻译工作流程的更多信息。 _我们建议您不要选择“英语”作为可翻译的语言，以防止创建 `en-US` 本地化文件，因为这会导致混淆。_

您的项目需要生成一个 `crowdin.yaml` 文件。

> 你将需要安装 `crowdin-cli`。 请参照[安装说明](https://support.crowdin.com/cli-tool/)。

下面的例子可以由 docusaurus cli 用 `examples` 脚本自动生成。 它应该放置在项目目录的顶层，以配置如何上传/下载文件。

以下是德语，西班牙语，法语，日语，韩语，印度尼西亚语，巴西葡萄牙语，简体中文和繁体中文的各种语言的配置示例。

```yaml
project_identifier_env: CROWDIN_DOCUSAURUS_PROJECT_ID
api_key_env: CROWDIN_DOCUSAURUS_API_KEY
base_path: "./"
preserve_hierarchy: true

files:
  -
    source: '/docs/*.md'
    translation: '/website/translated_docs/%locale%/%original_file_name%'
    languages_mapping: &anchor
      locale:
        'de': 'de'
        'es-ES': 'es-ES'
        'fr': 'fr'
        'ja': 'ja'
        'ko': 'ko'
        'mr': 'mr-IN'
        'pt-BR': 'pt-BR'
        'zh-CN': 'zh-CN'
        'zh-TW': 'zh-TW'
```

你可以在[这里](https://support.crowdin.com/configuration-file/)了解更多关于定制你的 `crowdin.yaml` 文件的信息。

### 手动同步文件

您将需要手动同步您的文件下拉和上传到 crowdin。 同步过程将上传 `/ docs` 中的任何 markdown 文件以及 `website/i18n/en.json` 中的可翻译字符串。 （这些字符串可以通过运行 `yarn write-translations` 来生成。）

您可以将以下内容添加到您的 `package.json` 中以手动触发 crowdin。

```json
"scripts": {
  "crowdin-upload": "export CROWDIN_DOCUSAURUS_PROJECT_ID=$YOUR_CROWDIN_ID;
  export CROWDIN_DOCUSAURUS_API_KEY=$YOUR_CROWDIN_API_KEY; crowdin-cli --config ../crowdin.yaml upload sources --auto-update -b master",
  "crowdin-download": "export CROWDIN_DOCUSAURUS_PROJECT_ID=$YOUR_CROWDIN_ID;
  export CROWDIN_DOCUSAURUS_API_KEY=$YOUR_CROWDIN_API_KEY; crowdin-cli --config ../crowdin.yaml download -b master"
},
```

这些命令需要拥有一个环境变量，用您的 crowdin 项目 id 和 api key（`CROWDIN_PROJECT_ID`，`CROWDIN_API_KEY`）设置。 你可以像上面一样内联添加它们，或者将它们永久添加到你的 `.bashrc` 或 `.bash_profile` 中。

如果在计算机上运行多个本地化的 Docusaurus 项目，则应该将环境变量的名称更改为唯一(`CROWDIN_PROJECTNAME_PROJECT_ID`, `CROWDIN_PROJECTNAME_API_KEY`)。

### 使用 CircleCI 自动同步文件

您可以使用 [CircleCI](https://circleci.com) 网络持续集成服务自动为您的文件下拉和上传翻译。

首先，更新项目目录中的 `circle.yml` 文件，包括上传要翻译的英文文件的步骤，以及使用 Crowdin CLI 下载已翻译的文件。 这是一个 `circle.yml` 文件的例子：

```yaml
machine:
  node:
    version: 6.10.3
  npm:
    version: 3.10.10

test:
  override:
    - "true"

deployment:
  website:
    branch: master
    commands:
      # 配置 git 用户
      - git config --global user.email "test-site-bot@users.noreply.github.com"
      - git config --global user.name "Website Deployment Script"
      - echo "machine github.com login test-site-bot password $GITHUB_TOKEN" > ~/.netrc
      # 安装 Docusaurus 并生成英文字符串文件
      - cd website && npm install && npm run write-translations && cd ..
      # 安装 crowdin
      - sudo apt-get install default-jre
      - wget https://artifacts.crowdin.com/repo/deb/crowdin.deb -O crowdin.deb
      - sudo dpkg -i crowdin.deb
      # 翻译 上传/下载
      - crowdin --config crowdin.yaml upload sources --auto-update -b master
      - crowdin --config crowdin.yaml download -b master
      # 构建和发布网站
      - cd website && GIT_USER=test-site-bot npm run publish-gh-pages
```

`crowdin` 命令使用 `examples` 脚本生成的 `crowdin.yaml` 文件。 它应该放在您的项目目录中，以配置如何上传/下载文件。

请注意，在 `crowdin.yaml` 文件中，`CROWDIN_PROJECT_ID` 和 `CROWDIN_API_KEY` 是Circle 中为你的 Crowdin 项目设置的环境变量。 他们可以在您的 Crowdin 项目设置中找到。

现在，Circle 将帮助您在构建您的网站之前自动获取翻译。 提供的 `crowdin.yaml` 文件会将翻译后的文件复制到 `website/translated_docs/` 中，`i18n/en.json` 字符串文件的翻译版本将转换为 `i18n/${language}.json`。

如果你想在本地使用你的机器上的 Crowdin，你可以安装 [Crowdin CLI 工具](https://support.crowdin.com/cli-tool/) 并运行 `circle.yaml` 文件中的命令。 唯一的区别是你必须在 `crowdin.yaml` 文件中设置 `project_identifier` 和 `api_key` 值，因为你不会设置 Circle 环境变量。

## 版本化翻译

如果您希望为文档进行翻译和版本控制，请将以下部分添加到 `crowdin.yaml` 文件的末尾：

```yaml
  -
    source: '/website/versioned_docs/**/*.md'
    translation: '/website/translated_docs/%locale%/**/%original_file_name%'
    languages_mapping: *anchor
```

翻译版本的文档将被复制到 `website/translated_docs/${language}/${version}/`。

> 确保在您的 Crowdin 设置的翻译部分中将 “重复字符串” 设置为[“隐藏 - 所有重复将共享相同的翻译”](https://support.crowdin.com/api/create-project/)。 此设置将确保不同版本之间的相同字符串共享一个翻译。
