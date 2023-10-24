---
title: 辅助函数（Helpers）
---

辅助函数帮助您在模版中快速插入内容。  辅助函数不能在源文件中使用。

您可以轻松地 [写入您自己的自定义助手](https://hexo.io/api/helper.html) 或使用我们的现成助手。

{% youtube Uc53pW0GJHU %}

## 网址

### url_for

在路径前加上根路径和域名。 输出会被自动转码。

``` js
<%- url_for(路径， [option]) %>
```

| 选项    | 描述       | 默认值                       |
| ----- | -------- | ------------------------- |
| `相对的` | 是否输出相对链接 | `config.relative_link` 的值 |

**示例：**

``` yml
_config.yml
root: /blog/
```

``` js
<%- url_for('/a/path') %>
//blog/a/path
```

是否输出相对链接，默认遵循配置文件中 `relative_link` 的值 例如， post/page 的相对路径值可能是 `/foo/bar/index.html`

``` yml
_config.yml
relative_link: true
```

``` js
<%- url_for('/css/style.css') %>
// ../../css/style.css
/* 覆盖配置
 * 即使配置文件中启用了 relative_link，你也可以使用 relative 参数禁用相对链接输出，反之亦然
 */
<%- url_for('/css/style.css', {relative: false}) %>
// /css/style.css
 */
<%- url_for('/css/style.css', {relative: false}) %>
// /css/style.css
```

### 相对url

取得与 `from` 相对的 `to` 路径。

``` js
<%- 相对url(from, to) %>
```

**示例：**

``` js
<%- relative_url('foo/bar/', 'css/style.css') %>
/../css/style.css
```

### 已满的 url_for

以 `config.url` 前缀返回一个URL。 输出自动编码。

``` js
<%- full_url_for(路径) %>
```

**示例：**

``` yml
_config.yml
url: https://example.com/blog# 示例
```

``` js
<%- full_url_for('/a/path') %>
// https://example.com/blog/a/path
```

### 格拉塔尔

根据邮箱地址返回 Gravatar 头像 URL。

如果你不指定 `options` 参数，将会应用默认参数。 否则，你可以将其设置为一个数字，这个数字将会作为 Gravatar 的大小参数。 最后，如果你设置它一个对象，它将会被转换为 Gravatar 的一个查询字符串参数。

``` js
<%- gravatar(email, [options]) %>
```

| 选项  | 描述       | 默认值 |
| --- | -------- | --- |
| `秒` | 图片大小     | 80  |
| `d` | 默认头像     |     |
| `f` | 强制使用默认图象 |     |
| `r` | 评分       |     |

访问 [Gravatar](https://en.gravatar.com/site/implement/images/) 了解更多。

**示例：**

``` js
<%- gravatar('a@abc.com') %>
/https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787

<%- gravatar('a@abc)。 om, 40) %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787?s=40

<%- gravatar('a@abc)。 om' {s：40, d：'https://via.placeholder.com/150 '}] %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73c73cb6bdb06787?s=40&d=https%3A%2F%2Fvia.placeholder.com%2F150
```

## HTML 标签

### css

载入 CSS 文件。 `路径` 可以是一个数组或一个字符串。 `路径` 可以是一个字符串、数组、对象或数组对象。 `path` 可以是数组或字符串，如果 `path` 开头不是 `/` 或任何协议，则会自动加上根路径；如果后面没有加上 `.css` 扩展名的话，也会自动加上。 对于自定义属性请使用对象类型。

``` js
<%- css(path, ...) %>
```

**示例：**

``` js
<%- css('style.css') %>
// <link rel="stylesheet" href="/style.css">

<%- css(['style.css', 'screen.css']) %>
// <link rel="stylesheet" href="/style.css">
// <link rel="stylesheet" href="/screen.css">

<%- css({ href: 'style.css', integrity: 'foo' }) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">

<%- css([{ href: 'style.css', integrity: 'foo' }, { href: 'screen.css', integrity: 'bar' }]) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">
// <link rel="stylesheet" href="/screen.css" integrity="bar">
```

### js

载入 JavaScript 文件。 `路径` 可以是一个字符串、数组、对象或数组对象。 `path` 可以是数组或字符串，如果 `path` 开头不是 `/` 或任何协议，则会自动加上根路径；如果后面没有加上 `.js` 扩展名的话，也会自动加上。 对于自定义属性请使用对象类型。

``` js
<%- js(path, ...) %>
```

**示例：**

``` js
<%- js('script.js') %>
// <script src="/script.js"></script>

<%- js(['script.js', 'gallery.js']) %>
// <script src="/script.js"></script>
// <script src="/gallery.js"></script>

<%- js({ src: 'script.js', integrity: 'foo', async: true }) %>
// <script src="/script.js" integrity="foo" async></script>

<%- js([{ src: 'script.js', integrity: 'foo' }, { src: 'gallery.js', integrity: 'bar' }]) %>
// <script src="/script.js" integrity="foo"></script>
// <script src="/gallery.js" integrity="bar"></script>
```

### 链接到

插入链接。

``` js
<%- link_to(路径, [text], [options]) %>
```

| 选项   | 描述       | 默认值   |
| ---- | -------- | ----- |
| `外部` | 在新视窗打开链接 | false |
| `类`  | Class 名称 |       |
| `id` | ID       |       |

**示例：**

``` js
<%- link_to('http://www.google.com') %>
// <a href="http://www.google.com" title="http://www.google.com">http://www.google.com</a>

<%- link_to('http://www.google.com', 'Google') %>
// <a href="http://www.google.com" title="Google">Google</a>

<%- link_to('http://www.google.com', 'Google', {external: true}) %>
// <a href="http://www.google.com" title="Google" target="_blank" rel="noopener">Google</a>
```

### 发送至

插入电子邮箱链接。

``` js
<%- mail_to(路径, [text], [options]) %>
```

| 选项     | 描述       |
| ------ | -------- |
| `类`    | Class 名称 |
| `id`   | ID       |
| `主题`   | 邮件主题     |
| `cc`   | CC       |
| `bcc`  | 密送（BCC）  |
| `正文内容` | 邮件内容     |

**示例：**

``` js
<%- mail_to('a@abc.com') %>
// <a href="mailto:a@abc.com" title="a@abc.com">a@abc.com</a>

<%- mail_to('a@abc.com', '电邮') %>
// <a href="mailto:a@abc.com" title="Email">Email</a>
```

### 图片标签

插入图片。

``` js
<%- image_tag(路径， [options]) %>
```

| 选项      | 描述       |
| ------- | -------- |
| `alt`   | 图片的替代文字  |
| `类`     | Class 名称 |
| `id`    | ID       |
| `width` | 图片宽度     |
| `高度`    | 图片高度     |

### 收藏夹标签

插入 favicon。

``` js
<%- favigicon_tag(路径) %>
```

### Feed_标签

插入 feed 链接。

``` js
<%- feed_tag(路径， [options]) %>
```

| 选项   | 描述      | 默认值            |
| ---- | ------- | -------------- |
| `标题` | Feed 标题 | `config.title` |
| `类型` | Feed 类型 |                |

**示例：**

``` js
<%- feed_tag('atom.xml') %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">

<%- feed_tag('rss.xml', { title: 'RSS Feed', type: 'rss' }) %>
// <link rel="alternate" href="/atom.xml" title="RSS Feed" type="application/rss+xml">

/* Defaults to hexo-generator-feed's config if no argument */
<%- feed_tag() %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">
```

## 条件标签

### 是当前的

检查 `path` 是否符合目前页面的网址。 开启 `strict` 选项启用严格比对。

``` js
<%- is_current(路径， [strict]) %>
```

### 是首页

检查当前页面是否为文章。

``` js
<%- is_home() %>
```

### is_home_first_page (+6.3.0)

检查当前页面是否为独立页面。

``` js
<%- is_home_first_page() %>
```

### 是帖子

检查当前页面是否为存档页面。

``` js
<%- is_post() %>
```

### 是页面

检查当前页面是否为年度归档页面。

``` js
<%- is_page() %>
```

### 是存档

检查当前页面是否为月度归档页面。

``` js
<%- is_archive() %>
```

### 是 年

检查当前页面是否为年度归档页面。

``` js
<%- is_year() %>
```

### 是月

检查当前页面是否为首页。

``` js
<%- is_month() %>
```

### 是类别

检查当前页面是否为分类归档页面。 如果给定一个字符串作为参数，将会检查目前是否为指定分类。

``` js
<%- is_category() %>
<%- is_category('hobby') %>
```

### 是标签

检查当前页面是否为标签归档页面。 如果给定一个字符串作为参数，将会检查目前是否为指定标签。

``` js
<%- is_tag() %>
<%- is_tag('hobby') %>
```

## 字符串处理

### 修饰

清除字符串开头和结尾的空格。

``` js
<%- 修剪(字符串) %>
```

### strip_html

清除字符串中的 HTML 标签。

``` js
<%- strip_html(字符串) %>
```

**示例：**

``` js
<%- strip_html('It\'s not <b>important</b> anymore!') %>
// It's not important anymore! %>
// 它不再重要！
```

### titlecase

把字符串转换为正确的 Title case。

``` js
<%- titlecase(string) %>
```

**示例：**

``` js
<%- titlecase('这是一个小程序') %>
# 这是一个苹果
```

### markdown

使用 Markdown 解析字符串。

``` js
<%- markdown(str) %>
```

**示例：**

``` js
<%- Markdown('make me **strong**') %>
// make me <strong>strong</strong>
```

### 渲染

解析字符串。

``` js
<%- 渲染(str, 引擎, [options]) %>
```

**示例：**

``` js
<%- render('p(class="example") Test', 'pug'); %>
// <p class="example">Test</p>
```

详见 [渲染](https://hexo.io/zh-cn/api/rendering)。

### 自动换行

使每行的字符串长度不超过 `length`。 `length` 预设为 80。

``` js
<%- word_wrapp(str, [length]) %>
```

**示例：**

``` js
<%- word_wrapp('一次, 8) %>
// 一次在\n 一次时间
```

### 截图

移除超过 `length` 长度的字符串。 `length` 的默认值是 30。

``` js
<%- truncate(text, length) %>
```

**示例：**

``` js
<%- truncate('Once upon a time in a world far far away', {length: 17}) %>
// Once upon a ti...

<%- truncate('Once upon a time in a world far far away', {length: 17, separator: ' '}) %>
// Once upon a...

<%- truncate('And they found that many people were sleeping better.', {length: 25, omission: '... (continued)'}) %>
// And they f... (continued)

<%- 截断('一次在远离世界的世界上很远', {length: 17, separator: ' '}) %>
// 一次...

<%- 截断(他们发现很多人睡得更好。', {length: 25, 忽略: '... （续）'}) %>
// 他们...
```

### 转义_html

在字符串中转义 HTML 实体。

``` js
<%- escape_html(str) %>
```

**示例：**

``` js
<%- escape_html('<p>Hello "world".</p>') %>
// &lt;p&gt;Hello &quot;world&quot;.&lt;&#x2F;p&gt;
```

## 模板

### 部分的

加载其他模板文件。 您可以在 `局部变量` 中定义本地变量。

``` js
<%- partial(布局, [locals], [options]) %>
```

| 选项   | 描述                                | 默认值     |
| ---- | --------------------------------- | ------- |
| `缓存` | 缓存（使用 Fragment cache）             | `false` |
| `仅限` | 限制局部变量。 在模板中只能使用 `locals` 中设定的变量。 | `false` |

### 片段缓存

局部缓存。 它储存局部内容，下次使用时就能直接使用缓存。

``` js
<%- fragment_cache(id, fn);
```

**示例：**

``` js
<%- fragment_cache('header', function()voir
  return '<header></header>';
}) %>
```

## 日期与时间

### 日期

插入格式化的日期。 `date` 可以是 UNIX 时间、ISO 字符串、Date 对象或 [Moment.js][] 对象。 `format` 默认为 `date_format` 配置信息。

``` js
<%- 日期(日期, [format]) %>
```

**示例：**

``` js
<%- 日期(Date.now ()) %>
// 2013-01-01

<%- 日期(Date.now (), 'YYYY/M/D') %>
// 1 2013
```

### date_xml

插入 XML 格式的日期。 `date` 可以是 UNIX 时间、ISO 字符串、Date 对象或 [Moment.js][] 对象。

``` js
<%- date_xml(date) %>
```

**示例：**

``` js
<%- date_xml(Date.now ()) %>
// 2013-01-01T00:00:00.00.000Z
```

### 时间

插入格式化的时间。 `date` 可以是 UNIX 时间、ISO 字符串、Date 对象或 [Moment.js][] 对象。 `format` 默认为 `time_format` 配置信息。

``` js
<%- 时间(日期, [format]) %>
```

**示例：**

``` js
<%- time(Date.now ()) %>
// 13:05:12

<%- time(Date.now (), 'h:mm:ss a') %>
// 1:05:12 pm
```

### 完整日期

插入格式化的日期和时间。 `date` 可以是 UNIX 时间、ISO 字符串、Date 对象或 [Moment.js][] 对象。 `format` 默认为 `date_format + time_format`。

``` js
<%- 完整日期(日期, [format]) %>
```

**示例：**

``` js
<%- full_date(new Date()) %>
// Jan 1, 2013 0:00:00

<%- full_date(新日期), 'dddd, MMM Do YYYY, h:mm:ss a') %>
// 2013年1月1日星期二，12:00:00
```

### 时间

[Moment.js][] 函数库。

## 列表

### 列表类别

插入分类列表。

``` js
<%- list_categories([options]) %>
```

| 选项       | 描述                                                                               | 默认值  |
| -------- | -------------------------------------------------------------------------------- | ---- |
| `排序方式`   | 分类排列方式                                                                           | 名称   |
| `订单`     | 排列顺序。 `1`, `asc` 升序；`-1`, `desc` 降序。                                             | 1    |
| `显示计数`   | 显示每个分类的文章总数                                                                      | true |
| `样式`     | 显示分类列表的样式。 分类列表的显示方式。 使用 `list` 以无序列表（unordered list）方式显示。 使用 `false` 或任何其他值禁用它。 | 邮件列表 |
| `分隔符`    | 分类间的分隔符号。 只有在 `style` 不是 `list` 时有用。                                             | ,    |
| `深度：`    | 要显示的分类层级。 `0` 显示所有层级的分类；`-1` 和 `0` 很类似，但是显示不分层级；`1` 只显示第一层的分类。                   | 0    |
| `类`      | 分类列表的 class 名称。                                                                  | 类别   |
| `转换`     | 改变分类名称显示方法的函数                                                                    |      |
| `suffix` | 为链接添加前缀                                                                          | 无    |

**示例：**

``` js
<%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return titlecase(str);
  }
}) %>
 <%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return str.toUpperCase();
  }
}) %>
```

### 列表标签

插入标签列表。

``` js
<%- list_tags([options]) %>
```

| 选项       | 描述                                                                               | 默认设置 |
| -------- | -------------------------------------------------------------------------------- | ---- |
| `排序方式`   | 分类顺序                                                                             | 名称   |
| `订单`     | 分类排列顺序。 `1`, `asc` 升序；`-1`, `desc` 降序。                                           | 1    |
| `显示计数`   | 显示每个标签的文章总数                                                                      | true |
| `样式`     | 显示标签列表的样式。 标签列表的显示方式。 使用 `list` 以无序列表（unordered list）方式显示。 使用 `false` 或任何其他值禁用它。 | 邮件列表 |
| `分隔符`    | 标签间的分隔符号。 只有在 `style` 不是 `list` 时有用。                                             | ,    |
| `类`      | 标签列表的类名（字符串）或自定义每个标签的类（对象，见下文）。                                                  | 标签   |
| `转换`     | 改变标签名称显示方法的函数。 请查看 [list_categories](#list-categories) 中给出的例子                    |      |
| `金额`     | 要显示的标签数量（0 = 无限制）                                                                | 0    |
| `suffix` | 为链接添加前缀                                                                          | 无    |

类的高级定制：

| 选项         | 描述                                                                                      | 默认设置                                       |
| ---------- | --------------------------------------------------------------------------------------- | ------------------------------------------ |
| `class.ul` | `<ul>` 类名 （只适用于样式 `list`）                                                         | `tag-list` （列表样式）                          |
| `class.li` | `<li>` 类名 （只适用于样式 `list`）                                                         | `tag-list-item` （列表样式）                     |
| `class.a`  | `<a>` 类名                                                                          | `tag-list-link` （列表样式） `tag-link` （普通样式）   |
| `标签`       | `<span>` 类名，标签 label 存储在这里（仅适用于普通样式，当 `class.label` 被设置时，标签被放置在 `<span>` 中） | `tag-label` （普通样式）                         |
| `计数`       | `<span>` 类名，标签 counter 存储在这里 （仅当 `show_count` 为 `true`）                           | `tag-list-count` （列表样式） `tag-count` （普通样式） |

示例：

```ejs
<%- list_tags(site.tags, {class: 'classtest', style: false, separator: ' | '}) %>
<%- list_tags(site. ags, {class: 'classtest', style: 'list'}>
<%- list_tags(站点)。 ags, {class: {ul: 'ulululul', li: 'lilili', aaa', count : 'ccc'}, style: false, separator: '| '}) %>
<%- list_tags(site ags, {class: {ul: 'ulululul', li: 'lilili', : 'aaa', count: 'ccc'}, 样式: 'list'}) %>
```

### 列表归档文件

插入归档列表。

``` js
<%- list_archives([options]) %>
```

| 选项     | 描述                                                                               | 默认值       |
| ------ | -------------------------------------------------------------------------------- | --------- |
| `类型`   | 类型。 此设定可为 `yearly` 或 `monthly`。                                                  | 每月的       |
| `订单`   | 标签排列顺序。 `1`, `asc` 升序；`-1`, `desc` 降序。                                           | 1         |
| `显示计数` | 显示每个归档的文章总数                                                                      | true      |
| `格式`   | 日期格式                                                                             | MMMM YYYY |
| `样式`   | 显示归档列表的样式。 归档列表的显示方式。 使用 `list` 以无序列表（unordered list）方式显示。 使用 `false` 或任何其他值禁用它。 | 邮件列表      |
| `分隔符`  | 归档间的分隔符号。 只有在 `style` 不是 `list` 时有用。                                             | ,         |
| `类`    | 归档列表的 class 名称。                                                                  | 存档        |
| `转换`   | 改变归档名称显示方法的函数。 请查看 [list_categories](#list-categories) 中给出的例子                    |           |

### 列表帖子

插入文章列表。

``` js
<%- list_poss([options]) %>
```

| 选项     | 描述                                                                    | 默认值  |
| ------ | --------------------------------------------------------------------- | ---- |
| `排序方式` | 帖子顺序                                                                  | 日期   |
| `订单`   | 文章排列顺序。 `1`, `asc` 升序；`-1`, `desc` 降序。                                | 1    |
| `样式`   | 文章列表的显示方式。 使用 `list` 以无序列表（unordered list）方式显示。 使用 `false` 或任何其他值禁用它。 | 邮件列表 |
| `分隔符`  | 文章间的分隔符号。 只有在 `style` 不是 `list` 时有用。                                  | ,    |
| `类`    | 文章列表的 class 名称。                                                       | 发帖   |
| `金额`   | 要显示的文章数量（0 = 无限制）                                                     | 6    |
| `转换`   | 改变文章名称显示方法的函数。 请查看 [list_categories](#list-categories) 中给出的例子         |      |

### tagcloud

插入标签云。

``` js
<%- tagcloud([tags], [options]) %>
```

| 选项                     | 描述                                                                                                                           | 默认值   |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ----- |
| `最小字体`                 | 最小字体尺寸                                                                                                                       | 10    |
| `max_font`             | 最大字体尺寸                                                                                                                       | 20    |
| `单位`                   | 字体尺寸的单位                                                                                                                      | px    |
| `金额`                   | 标签总量                                                                                                                         | 无限制   |
| `排序方式`                 | 标签排列方式                                                                                                                       | 名称    |
| `订单`                   | 标签排列顺序。 `1`, `sac` 升序；`-1`, `desc` 降序                                                                                        | 1     |
| `颜色`                   | 使用颜色                                                                                                                         | false |
| `开始颜色`                 | 开始的颜色。 您可使用十六进位值（`#b700ff`），rgba（`rgba(183, 0, 255, 1)`），hsla（`hsla(283, 100%, 50%, 1)`）或 [颜色关键字][]。 此变量仅在 `color` 参数开启时才有用。 |       |
| `结束颜色`                 | 结束的颜色。 您可使用十六进位值（`#b700ff`），rgba（`rgba(183, 0, 255, 1)`），hsla（`hsla(283, 100%, 50%, 1)`）或 [颜色关键字][]。 此变量仅在 `color` 参数开启时才有用。 |       |
| `类`                    | 标签的 class name 前缀                                                                                                            |       |
| `关卡`                   | 不同 class name 的总数。 此变量仅在 `class` 参数设定时才有用。                                                                                   | 10    |
| `show_count` (+6.3.0)  | 显示每个标签的文章总数                                                                                                                  | false |
| `count_class` (+6.3.0) | 标签文章总数的 class                                                                                                                | 计数    |

**示例：**

``` js
// Default options
<%- tagcloud() %>

// Limit number of tags to 30
<%- tagcloud({amount: 30}) %>
```

## 其他

### 分页器

插入分页器。

``` js
<%- 分页符(选项) %>
```

| 选项                            | 描述                                              | 默认值      |
| ----------------------------- | ----------------------------------------------- | -------- |
| `基数`                          | 基础网址                                            | /        |
| `格式`                          | 网址格式                                            | page/%d/ |
| `总计`                          | 分页总数                                            | 1        |
| `当前的`                         | 目前页数                                            | 0        |
| `前置文本`                        | 上一页链接的文字。 仅在 `prev_next` 设定开启时才有用。              | 上一个      |
| `下一文本`                        | 下一页链接的文字。 仅在 `prev_next` 设定开启时才有用。              | 下一个      |
| `空格`                          | 空白文字                                            | &hellip; |
| `下一个`                         | 显示上一页和下一页的链接                                    | true     |
| `结束大小`                        | 显示于两侧的页数                                        | 1        |
| `中大小`                         | 显示于中间的页数                                        | 2        |
| `显示所有`                        | 显示所有页数。 如果开启此参数的话，`end_size` 和 `mid_size` 就没用了。 | false    |
| `跳转`                          | 转义 HTML 标签                                      | true     |
| page_class                    | 分页链接的 class 名称                                  | `页码`     |
| `current_class` (+6.3.0)      | 当前页链接的 class 名称                                 | `当前的`    |
| `space_class` (+6.3.0)        | 空白文字的 class 名称                                  | `空格`     |
| `prev_class` (+6.3.0)         | 上一页链接的 class 名称                                 | `扩展上一个`  |
| `下一类` (+6.3.0)                | 下一页链接的 class 名称                                 | `扩展下一个`  |
| `force_prevent_next` (+6.3.0) | 强制显示上一页和下一页的链接                                  | false    |


**示例：**

``` js
<%- paginator(ford
  prevent_text: '<',
  next tt_text: '>'
}) %>
```

``` html
<！ - 渲染为 -->
<a href="/1/">&lt;</a>
<a href="/1/"></a>
2
<a href="/3/">3</a>
<a href="/3/">&gt；</a>
```

``` js
<%- paginator(ford
  prevent_text: '<i class="fa fa-angle-left"></i>',
  next tt_text: '<i class="fa fa-angle-right"></i>',
  escape: false
}) %>
```

``` html
<！ - 渲染为 -->
<a href="/1/"><i class="fa fa-angle-left"></i></a>
<a href="/1/">1</a>
2
<a href="/3/">3</a>
<a href="/3/"><i class="fa fa-angle-right"></i></a>
```

### 搜索表单

插入 Google 搜索框。

``` js
<%- search_form(选项) %>
```

| 选项   | 描述                                      | 默认值   |
| ---- | --------------------------------------- | ----- |
| `类`  | 表单的 class name                          | 搜索表单  |
| `文本` | 搜索提示文字                                  | 搜索    |
| `按钮` | 显示搜索按钮。 该值可以是布尔值或字符串。 如果值是字符串，它将是按钮的文本。 | false |

### 数字格式

格式化数字。

``` js
<%- 数字格式(数、 [options]) %>
```

| 选项    | 描述                         | 默认值   |
| ----- | -------------------------- | ----- |
| `精度`  | 数字精度。 此选项可为 `false` 或非负整数。 | false |
| `分隔符` | 千位数分隔符号                    | ,     |
| `分隔符` | 整数和小数之间的分隔符号               | .     |

**示例：**

``` js
<%- 数字格式(12345.67, {precision: 1}) %>
// 12,345.68

<%- 数字格式(12345) 7, {precision: 4}%>
// 12,345.6700

<%- 数字格式(12345) 7, {precision: 0}(%) %>
// 12,345

<%- number_格式(12345.67, {delimiter: ''}) %>
// 12345。 7

<%- 数字格式(12345.67, {separator: '/'}) %>
/ 12,345/67
```

### meta_generator

插入 [generator tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)。

``` js
<%- meta_generator() %>
```

**示例：**

``` js
<%- meta_generator() %>
// <meta name="generator" content="Hexo 4.0.0">
```

### 打开图

插入 [打开图][] 数据。

``` js
<%- open_graph([options]) %>
```

| 选项              | 描述                                   | 默认值                                   |
| --------------- | ------------------------------------ | ------------------------------------- |
| `标题`            | 页面标题 (`og:title`)                    | `page.title`                          |
| `类型`            | 页面类型 (`og:type`)                     | 博客                                    |
| `网址`            | 页面网址 (`og:url`)                      | `网址`                                  |
| `图片`            | 页面图片 (`og:image`)                    | 内容中的图片                                |
| `作者`            | 文章作者 (`og:article:author`)           | `作者`                                  |
| `日期`            | 文章发表时间 (`og:article:published_time`) | 页面发表时间                                |
| `已更新`           | 文章修改时间 (`og:article:modified_time`)  | 页面修改时间                                |
| `语言`            | 文章语言 (`og:locale`)                   | `页面.lang || 页面.语言 || config.language` |
| `站点名称`          | 网站名称 (`og:site_name`)                | `config.title`                        |
| `描述`            | 页面描述 (`og:description`)              | 内容摘要或前 200 字                          |
| `twitter_card`  | Twitter 卡片类型 (`twitter:card`)        | summary                               |
| `twitter_id`    | Twitter ID (`twitter:creator`)       |                                       |
| `Twitter_site`  | Twitter 网站 (`twitter:site`)          |                                       |
| `twitter_image` | Twitter Image (`twitter:image`)      |                                       |
| `谷歌加成`          | Google+ 个人资料链接                       |                                       |
| `fb_admins`     | Facebook 管理者 ID                      |                                       |
| `fb_app_id`     | Facebook 应用程序 ID                     |                                       |

### 托克

解析内容中的标题标签 (h1~h6) 并插入目录。

``` js
<%- toc(str, [options]) %>
```

| 选项                      | 描述                | 默认值               |
| ----------------------- | ----------------- | ----------------- |
| `类`                     | Class 名称          | `托克`              |
| `class_item` (+6.3.0)   | 目录元素的 Class 名称    | `${class}-item`   |
| `class_link` (+6.3.0)   | 目录内链接的 Class 名称   | `${class}-link`   |
| `class_text` (+6.3.0)   | 目录链接内文本的 Class 名称 | `${class}-text`   |
| `class_child` (+6.3.0)  | 子类别名称             | `${class}-child`  |
| `class_number` (+6.3.0) | 目录序号的 Class 名称    | `${class}-number` |
| `class_level` (+6.3.0)  | 目录层级的 Class 名称前缀  | `${class}-level`  |
| `邮件列表编号`                | 显示编号              | true              |
| `最大深度`                  | 生成 TOC 的最大深度      | 6                 |
| `最小深度`                  | 生成 TOC 的最小深度      | 1                 |

**class_level**

``` js
<%- toc(page.content) %>
```

#### 无编号数据 (+6.1.0)

带有 `data-toc-unnumbered="true"` 属性的标题将被标记为未编号（不显示列表编号）。

{% note warn "警告！" %} %}
对于使用 `data-toc-unnumbered="true"`，渲染引擎必须要有添加 CSS 类的选项。

请看下面的 PR。

- https://github.com/hexojs/hexo/pull/4871
- https://github.com/hexojs/hexo-util/pull/269
- https://github.com/hexojs/hexo-render-markdown-it/pull/174
{% endnote %}

[颜色关键字]: http://www.w3.org/TR/css3-color/#svg-color
[Moment.js]: http://momentjs.com/
[打开图]: http://ogp.me/
