# 发布网站

你现在应该有一个[在本地运行的网站](getting-started-site-creation.md)。 一旦你将它[定制为](api-site-config.md)你喜欢样子，就是时候发布它了。 Docusaurus 生成一个静态 HTML 网站，准备好由您最喜爱的网络服务器或在线托管解决方案来提供服务。

## 构建静态 HTML 页面

要创建您的网站的静态版本，请在 `website` 的目录中运行以下脚本：

```
yarn run build # 或 `npm run build`
```

这将在 `website` 目录下生成 `build` 文件夹，其中包含 `pages` 中的所有文档和其他页面的 `.html` 文件。

## 托管静态 HTML 页面

此时，您可以抓取 `website/build` 文件夹中的所有文件，并将它们复制到您喜欢的 Web 服务器的“html”目录中。

> 例如，Apache 和 nginx 默认提供 `/var/www/html` 中的内容。 也就是说，选择一个 Web 服务器或提供商是不属于 Docusaurus 的范围。

### 使用 GitHub 页面

虽然选择 Web 服务器或主机不在 Docusaurus 的范围内，但 Docusaurus 的设计与开放源代码项目中最受欢迎的托管解决方案之一非常吻合：
[GitHub Pages](https://pages.github.com/).

如果您已经在使用 GitHub 来托管您的项目，那么将您的 Docusaurus 站点部署到 GitHub Pages 是非常简单的。 你的代码库甚至不需要公开。

> 即使您的 repo 是私有的，发布到 `gh-pages` 分支的任何内容都将是 [公开的](https://help.github.com/articles/user-organization-and-project-pages/)。

大部分发布到 GitHub pages 的工作都是通过 [`publish-gh-pages`](./api-commands.md#发布-docusaurus) 脚本自动完成的。 您只需确定脚本所需的一些参数的值即可。

在 [`siteConfig.js`](api-site-config.md) 中设置两个必需的参数：

- `organizationName`: 拥有存储库的 GitHub 用户或组织。 在 Docusaurus 的情景下，这 GitHub 组织将是 "facebook"。
- `projectName`: 您的项目的 GitHub 存储库的名称。 例如，Docusaurus 托管在 https://github.com/facebook/docusaurus，所以在这种情景下我们的项目名称将是 "docusaurus"。

> 虽然我们建议在 `siteConfig.js` 中设置上面的内容，您也可以使用环境变量`ORGANIZATION_NAME` 和 `PROJECT_NAME` 。

其中一个必需的参数设置为环境变量：

- `GIT_USER`: 具有提交访问权限的 GitHub 帐户的用户名。 对于你自己的仓库，这通常是你自己的 GitHub 用户名。

还有两个可选参数设置为环境变量：

- `USE_SSH`: 如果设置为 `true`，则使用 SSH 代替 HTTPS 连接到 GitHub 仓库。 如果未设置此变量，则默认值是 HTTPS 。

- `CURRENT_BRANCH`: 包含将部署的最新文档更改的分支。 通常情况下，分支是 `master`，但是除了 `gh-pages` 外，它可以是任何分支（默认或其他）。 如果没有设置这个变量，那么将使用当前的分支。

> Docusaurus 还支持部署用户或组织站点。 只需将您的项目名称设置为 "_username_.github.io"（其中 _username_ 是您在 GitHub 上的用户名或组织名称），发布脚本将自动将您的站点部署到 "master" 分支的根目录。

一旦获得了参数值信息，就可以继续运行发布脚本，确保您在各种参数占位符中插入了自己的值：

要直接从命令行运行脚本，可以使用以下方法，根据需要填写参数值。

```bash
GIT_USER=<GIT_USER> \
  CURRENT_BRANCH=master \
  USE_SSH=true \
  yarn run publish-gh-pages # 或 `npm run publish-gh-pages`
```

> 指定的 `GIT_USER `必须具有对 `organizationName` 和 `projectName` 组合中指定的存储库的访问权限。

您现在应该可以通过访问其 GitHub Pages 的 URL 来加载您的网站，这可能是 https://_username_.github.io/_projectName_ ，或者如果您已经设置了自定义域名。 例如，Docusaurus 的自己的 GitHub 页面 URL 是 https://docusaurus.io（它也可以通过 https://docusaurus.io/ 访问），因为它是由 https://github.com/facebook/docusaurus GitHub repo 的 `gh-pages` 分支提供的。我们强烈建议您阅读 [GitHub Pages 文档](https://pages.github.com) 以了解更多关于这个托管解决方案的信息。

您可以在任何希望更新文档时运行该命令，并将更改部署到您的网站。 对于文档很少更改的站点，手动运行脚本可能没问题，记住手动部署更改也不是太麻烦。

当然，您可以通过持续集成（CI）自动执行发布过程。

## 使用持续集成实现自动化部署

持续集成（CI）服务通常用于在新提交签入源代码控制时执行例行任务。 这些任务可以是运行单元测试和集成测试的任意组合，自动构建，将包发布到 NPM，是的，将更改部署到您的网站。 你所需要做的就是自动部署你的网站，只要你的文档被更新，就调用 `publish-gh-pages` 脚本。 在下一节中，我们将介绍如何使用 [Circle CI](https://circleci.com/) 这个流行的持续集成服务提供商。

### 使用 Circle CI

如果您已经为您的项目使用了 Circle CI，则只需将 Circle 配置为在发布步骤中运行 `publish-gh-pages` 脚本，就可以启用自动部署。

1. 确保设置为 `GIT_USER` 的 GitHub 账户拥有对包含文档的 repo 的 `write` 访问权限，方法是在 repo 中勾选 `Settings | Collaborators & teams`。
1. 以 `GIT_USER` 的身份登录到 GitHub。
1. 转到 https://github.com/settings/tokens 获取 `GIT_USER` 并生成一个新的 [个人访问令牌](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)，通过 `repo` 访问范围授予它完全控制私有存储库的权限。 将此令牌存放在安全的地方，确保不与任何人分享。 这个令牌可以用来代替你的 GitHub 密码来代表你的 GitHub 动作。
1. 打开您的 Circle CI 仪表板，并导航到您的存储库的设置页面，然后选择 "Environment variables"。 该 URL 看起来像 https://circleci.com/gh/ORG/REPO/edit#env-vars，其中 "ORG/REPO" 应该替换为您自己的 GitHub org/repo。
1. 创建一个名为 "GITHUB_TOKEN" 的新环境变量，使用新生成的访问令牌作为值。
1. 打开你的 `circle.yml` 文件，在 `machine:` 部分下添加以下内容，告诉 Circle 使用相对较新版本的 node 和 npm，如果可以，用 yarn 替换 npm：

```
machine:
  node:
    version: 6.11.2
  npm:
    version: 3.10.10
```

1. 然后，将以下行添加到 `deployment:` 部分。 如果您没有 `deployment:` 部分，则可以将其添加到文件末尾。

```
deployment:
  website:
    branch: master
    commands:
      - git config --global user.email "<GITHUB_USERNAME>@users.noreply.github.com"
      - git config --global user.name "<YOUR_NAME>"
      - echo "machine github.com login <GITHUB_USERNAME> password $GITHUB_TOKEN" > ~/.netrc
      - cd website && npm install && GIT_USER=<GIT_USER> npm run publish-gh-pages
```

确保 `<GIT_USER>` 替换为将用于发布文档的 GitHub 帐户的实际用户名。

**不要** 将 `$ GITHUB_TOKEN` 的实际值放在 `circle.yml` 中。 我们已经在步骤 3 中将其作为环境变量进行配置。

> 如果你想为你的 GitHub repo 连接使用 SSH，你可以设置 `USE_SSH=true`。 所以上面的命令看起来像这样：`cd website && npm install && GIT_USER=<GIT_USER> USE_SSH=true npm run publish-gh-pages`.

> 与手动运行 `publish-gh-pages` 脚本不同的是，当脚本在 Circle 环境中运行时，`CURRENT_BRANCH` 的值已经被定义为 [CircleCI 中的一个环境变量](https://circleci.com/docs/1.0/environment-variables/)，并且会被脚本自动获取。

现在，无论何时一个新的提交出现在 `master` 中，Circle CI 都会运行您的测试套件，如果一切通过，您的网站将通过 `publish-gh-pages` 脚本进行部署。

> 如果您更愿意使用部署密钥而不是个人访问令牌，则可以从 Circle CI [instructions](https://circleci.com/docs/1.0/adding-read-write-deployment-key/) 添加 read/write 部署密钥。

#### 提示 & 技巧

当使用 Circle CI 初始部署到 `gh-pages` 分支时，您可能会注意到，由于缺少测试，提交给 `gh-pages` 分支触发的一些作业无法成功运行。 您可以通过创建具有以下内容的基本 Circle CI 配置轻松解决此问题：

```yml
# Circle CI 2.0 Config File
# 这个配置文件将阻止测试在 gh-pages 分支上运行。
version: 2
jobs:
  build:
    machine: true
    branches:
      ignore: gh-pages
    steps:
      -run: echo "Skipping tests on gh-pages branch"
```

将这个文件保存为 `config.yml`，并将其放在 `website/assets` 文件夹内的 `.circleci` 文件夹中。
