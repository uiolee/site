---
title: 数据文件
---

有时您可能需要在模板中使用一些在您的帖子中无法直接获取的数据。 或者你想要在别处重新使用数据。 对于这种情况，Hexo 3 引入了新的 **数据文件**。 此功能在 `source/_data` 文件夹中加载了YAML 或 JSON 文件，以便您可以在您的网站中使用它们。

{% youtube CN31plHbI-w %}

例如，在 `source/_data` 文件夹中添加 `menu.yml`

``` yaml
主页: /
图库: /gallery/
档案: /archives/
```

你可以在模板中使用它们：

```
<% 用于 (站点数据中的 var 链接)。 enu: %>
  <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% }>
```

渲染就像这样：

```
<a href="/"> Home </a>
<a href="/gallery/"> Gallery </a>
<a href="/archives/"> Archives </a>
```
