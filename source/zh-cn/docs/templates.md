---
title: 模板
---

模板通过描述每个页面的样式来定义您网站的演示。 下表显示每个可用页面的相应模板。 At the very least, a theme should contain an `index` template.

{% youtube mb65bQ4iUc4 %}

| 模板   | 页    | Fallback |
| ---- | ---- | -------- |
| `索引` | 主页   |          |
| `发帖` | 员额   | `索引`     |
| `页面` | 页 次  | `索引`     |
| `存档` | 档案   | `索引`     |
| `类别` | 分类档案 | `存档`     |
| `标签` | 标签档案 | `存档`     |

## 布局

When pages share a similar structure - for instance, when two templates have both a header and a footer - you can consider using a `layout` to declare these structural similarities. 每个布局文件都应该包含一个 `正文` 变量来显示有关模板的内容。 例如：

``` html index.ejs
索引
```

``` html layout.ejs
<!DOCTYPE html>
<html>
  <body><%- body %></body>
</html>
```

产量：

``` html
<!DOCTYPE html>
<html>
  <body>索引</body>
</html>
```

默认情况下，所有其他模板都使用了 `布局` 模板。 You can specify additional layouts in the front-matter or set it to `false` to disable it. 甚至可以通过在您的顶部布局中添加更多的布局来构建复杂的嵌套结构。

## 部分

零件对于共享模板之间的组件非常有用。 典型的例子包括标题、页脚或侧边栏。 您可能想要将您的部分放在单独的文件中，以使维护您的网站更加方便。 例如：

``` html partial/header.ejs
<h1 id="logo"><%= config.title %></h1>
```

``` html index.ejs
<%- partial('partial/header') %>
<div id="content">主页</div>
```

产量：

``` html
<h1 id="logo">我的网站</h1>
<div id="content">首页</div>
```

## 本地变量

您可以在模板中定义本地变量并在其他模板中使用它们。

``` html partial/header.ejs
<h1 id="logo"><%= title %></h1>
```

``` html index.ejs
<%- partial('partial/header', {title: 'Hello World'}) %>
<div id="content">首页</div>
```

产量：

``` html
<h1 id="logo">Hello World</h1>
<div id="content">主页</div>
```

## 优化

如果您的主题过于复杂，或者如果要生成的文件数量过大， 十六进制文件生成性能可能开始大幅下降。 除了简化您的主题外，您还可以尝试片段缓存，这是在 Hexo 2.7中引入的。

This feature was borrowed from [Ruby on Rails](http://guides.rubyonrails.org/caching_with_rails.html#fragment-caching). 它导致内容被保存为片段并在提出额外请求时缓存。 这可以减少数据库查询次数，也可以加快文件生成。

片段缓存最好用于头、页脚、侧边栏或其他静态内容，这些内容不可能从模板变为模板。 例如：

``` js
<%- fragment_cache('header', function()Pop
  return '<header></header>';
});
```

尽管使用部分可能比较容易：

``` js
<%- partial('header', {}, {cache: true});
```

{% note warn %}
`fragment_cache()` 将缓存结果并将缓存结果输出到其他页面。 这只能用于预期为 **而不是** 更改不同页面的partials。 否则，它应该启用 **而不是**。 例如，在配置启用 `relative_link` 时，它应该被禁用。 这是因为各页之间的相对链接可能出现差异。
{% endnote %}
