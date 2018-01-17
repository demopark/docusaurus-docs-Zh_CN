# 添加博客

## 初始设置

要设置您的网站的博客，先在您的仓库的网站目录中创建一个 `blog` 文件夹。

然后，在 `siteConfig.js` 中添加一个 header link 到你的博客：

```
headerLinks: [
    ...
    {blog: true, label: 'Blog'},
    ...
]
```


## 添加博文

要在博客中发布，请在博客文件夹中创建一个格式为 `YYYY-MM-DD-My-Blog-Post-Title.md` 的文件。 发布日期是从文件名中提取的。

例如，在 `website/blog/2017-08-18-Introducing-Docusaurus.md`:

```
---
author: Frank Li
authorURL: https://twitter.com/foobarbaz
authorFBID: 503283835
title: Introducing Docusaurus
---

博文内容..
```


## Header 参数

唯一必需的字段是`title`; 不过，我们也提供了将作者信息添加到博客文章的参数。

- `author` - 作者署名的文本标签。
- `authorURL` - 与作者相关的网址。 这可能是一个Twitter，GitHub，Facebook帐户等。
- `authorFBID` - 用于提取个人资料图片的 Facebook ID。
- `title` - 博客文章标题。


## 摘要截断

使用博客文章中的  `<!--truncate-->` 标记来表示在查看博客发布的所有博客文章时将显示的摘要。 在 `<!--truncate-->` 之上的任何内容都将成为摘要的一部分。 例如：

```
---
title: 截断示例
---

所有这些将成为博客文章摘要的一部分。

就到这里。

<!--truncate-->

但是从此以后的任何内容都不会是。

不是这里。

也不是这里。
```

## RSS 订阅

Docusaurus 为您的博客文章提供了一个简单的 RSS 源。 支持 RSS 和 Atom 订阅格式。 这些数据会自动添加到您的网站页面的 HTML <HEAD> 标签中。

RSS 订阅中提供了文章的摘要，直到 `<!--truncate-->` 结束。 如果没有找到`<!--truncate-->` 标签，那么所有文本最多可以使用250个字符。

## 社交按钮

如果您希望在博客文章的底部添加 Facebook 和/或 Twitter 社交按钮，请在 `siteConfig.js` 中设置 `facebookAppId` 和/或 `twitter` [网站配置](api-site-config.md) 参数。
