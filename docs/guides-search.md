# 启用搜索

Docusaurus 支持使用 [Algolia DocSearch](https://community.algolia.com/docsearch/) 进行搜索。 一旦你建立了你的网站，[输入你的网站信息](https://community.algolia.com/docsearch/) 来让 Algolia 抓取你网站的文档页面。 Algolia 会向您发送您的网站的 API 密钥和索引名称。

### 启用搜索栏

在 `algolia` 部分的 `siteConfig.js` 中输入您的搜索 API 密钥和索引名称，以启用您的网站搜索。

```js
const siteConfig = {
  ...
  algolia: {
    apiKey: "my-search-only-api-key-1234",
    indexName: "my-index-name"
  },
  ...
}
```

### 额外搜索参数

您还可以在 `algolia` 中使用`algoliaOptions`字段指定额外的 [Algolia 使用的搜索参数](https://community.algolia.com/docsearch/documentation/)。 如果您想为文档的不同版本或语言提供不同的搜索结果，这可能会很有用。 任何 "VERSION" 或 "LANGUAGE" 都将被当前页面的版本或语言所取代。 关于搜索选项的更多细节可以在[这里找到](https://www.algolia.com/doc/api-reference/api-parameters/#overview)。

```js
const siteConfig = {
  ...
  algolia: {
    ...
    algoliaOptions: { 
      facetFilters: [ "tags:VERSION" ], 
      hitsPerPage: 5 
    }
  },
}
```

### 控制搜索栏位置

默认情况下，搜索栏将是顶部导航栏中最右边的元素。

如果您想更改默认位置，请在 `siteConfig.js` 的 `headerLinks` 字段中将 `searchBar` 标志添加到您想要的位置。 例如，您可能需要在内部和外部链接之间的搜索栏。

```js
const siteConfig = {
  ...
  headerLinks: [
    {...}
    {...}
    { search: true }
    {...}
    {...}
  ],
  ...
}
```

### 禁用搜索栏

要禁用搜索栏，请注释掉（推荐）或删除 `siteConfig.js` 文件中的 `algolia` 部分。

另外，如果您在 `headerLinks` 中自定义了搜索栏的位置，请设置 `search: false`。
