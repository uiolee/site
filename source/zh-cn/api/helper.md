---
title: 帮助者
---

帮手可以轻松地将代码片段添加到您的模板。 当你处理更复杂的代码时，我们建议使用助手而不是模板。

无法从 `源` 文件访问助手.

## 简述

``` js
hexo.extend.helper.register(name, function()@un.org.
  // ...
});
```

## 示例

``` js
hexo.extend.helper.register('js', function(path)申請
  return '<script src="' + path + '"></script>';
});
```

``` js
<%- js('script.js') %>
// <script src="script.js"></script>
```

## 常见问题

### 放置自定义助手在哪里？

Place it under `scripts/` or `themes/<yourtheme>/scripts/` folder.

### 如何在我的自定义助手中使用另一个注册的助手？

所有助手都是在相同的环境下执行的。 例如，要在自定义助手中使用 [`url_for()`](/docs/helpers#url-for)

``` js
hexo.extend.helper.register('lorem', function(path) {
  return '<script src="' + this.url_for(path) + '"></script>';
});
```

### 我如何在另一个扩展中使用注册的助手(例如过滤器、喷射器等)？

`hexo.extend.helper.get` 将返回助手函数，但是它的上下文需要十六进制，这样：

``` js
const url_for = hexo.extend.helper.get('url_for').bindhexo;
```
