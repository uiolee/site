---
title: 数据文件
---

有时您可能需要在模板中使用一些在您的帖子中无法直接获取的数据。 或者你想要在别处重新使用数据。 对于这种情况，Hexo 3 引入了新的 **数据文件**。 此功能会载入 `source/_data` 内的 YAML 或 JSON 文件，如此一来您便能在网站中复用这些文件了。

{% youtube CN31plHbI-w %}

举例来说，在 `source/_data` 文件夹中新建 `menu.yml` 文件：

``` yaml
主页: /
图库: /gallery/
档案: /archives/
```

您就能在模板中使用这些资料：

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
