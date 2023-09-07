---
title: Helpers
---

帮助程序在模板中被用于帮助您快速插入代码片段。  无法在源文件中使用助手。

您可以轻松地 [写入您自己的自定义助手](https://hexo.io/api/helper.html) 或使用我们的现成助手。

{% youtube Uc53pW0GJHU %}

## 网址

### url_for

返回带有根路径前缀的URL。 输出自动编码。

``` js
<%- url_for(路径， [option]) %>
```

| 选项    | 描述     | 默认设置                   |
| ----- | ------ | ---------------------- |
| `相对的` | 输出相对链接 | `config.relative_link` |

**示例：**

``` yml
_config.yml
root: /blog/ # 示例
```

``` js
<%- url_for('/a/path') %>
//blog/a/path
```

Relative link, follows `relative_link` option by default e.g. post/page path is '/foo/bar/index.html'

``` yml
_config.yml
relative_link: true
```

``` js
<%- url_for('/css/style.css') %>
/../../css/style. ss

/* 覆盖选项
 * 您也可以禁用它来输出一个非相对链接，
 * 即使启用 `relative_link` ，反之亦然。
 */
<%- url_for('/css/style.css', {relative: false}) %>
// /css/style.css
```

### 相对url

将 `的相对URL从` 返回 `返回`。

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

从电子邮件返回Gravatar图像URL。

如果您没有指定 [options] 参数，默认选项将适用。 否则，你可以将其设置为一个数字，然后将其作为尺寸参数传递给Gravatar。 最后，如果您将其设置为对象，它将被转换为Gravatar的查询字符串参数。

``` js
<%- gravatar(email, [options]) %>
```

| 选项  | 描述     | 默认设置 |
| --- | ------ | ---- |
| `秒` | 输出图像大小 | 80   |
| `d` | 默认图像   |      |
| `f` | 强制默认   |      |
| `r` | 评分     |      |

More info: [Gravatar](https://en.gravatar.com/site/implement/images/)

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

加载 CSS 文件。 `路径` 可以是一个数组或一个字符串。 `路径` 可以是一个字符串、数组、对象或数组对象。 [`/<root>/`](/docs/configuration#URL) 值已预定，而 `.css` 扩展被自动附加到 `路径` 自定义属性使用对象类型。

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

加载 JavaScript 文件。 `路径` 可以是一个字符串、数组、对象或数组对象。 [`/<root>/`](/docs/configuration#URL) value is prepended while `.js` extension is appended to the `path` automatically. 自定义属性使用对象类型。

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

插入一个链接。

``` js
<%- link_to(路径, [text], [options]) %>
```

| 选项   | 描述        | 默认设置  |
| ---- | --------- | ----- |
| `外部` | 在新标签中打开链接 | false |
| `类`  | 类名        |       |
| `id` | ID        |       |

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

插入邮件链接。

``` js
<%- mail_to(路径, [text], [options]) %>
```

| 选项     | 描述   |
| ------ | ---- |
| `类`    | 类名   |
| `id`   | ID   |
| `主题`   | 邮件主题 |
| `cc`   | CC   |
| `bcc`  | 密送抄送 |
| `正文内容` | 邮件内容 |

**示例：**

``` js
<%- mail_to('a@abc.com') %>
// <a href="mailto:a@abc.com" title="a@abc.com">a@abc.com</a>

<%- mail_to('a@abc.com', '电邮') %>
// <a href="mailto:a@abc.com" title="Email">Email</a>
```

### 图片标签

插入图像。

``` js
<%- image_tag(路径， [options]) %>
```

| 选项      | 描述      |
| ------- | ------- |
| `alt`   | 图像的替代文本 |
| `类`     | 类名      |
| `id`    | ID      |
| `width` | 图像宽度    |
| `高度`    | 图像高度    |

### 收藏夹标签

插入收藏夹。

``` js
<%- favigicon_tag(路径) %>
```

### Feed_标签

插入一个供稿链接。

``` js
<%- feed_tag(路径， [options]) %>
```

| 选项   | 描述    | 默认设置           |
| ---- | ----- | -------------- |
| `标题` | 新闻源标题 | `config.title` |
| `类型` | 新闻源类型 |                |

**示例：**

``` js
<%- feed_tag('atom.xml') %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">

<%- feed_tag('rss.xml', { title: 'RSS Feed', type: 'rss' }) %>
// <link rel="alternate" href="/atom.xml" title="RSS Feed" type="application/atom+xml">

/* Defaults to hexo-generator-feed's config if no argument */
<%- feed_tag() %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">
```

## 条件标签

### 是当前的

检查 `路径` 是否匹配当前页面的 URL。 使用 `严格的` 选项来启用严格匹配。

``` js
<%- is_current(路径， [strict]) %>
```

### 是首页

检查当前页面是否为首页。

``` js
<%- is_home() %>
```

### is_home_first_page (+6.3.0)

检查当前页面是否为首页。

``` js
<%- is_home_first_page() %>
```

### 是帖子

检查当前页面是否是帖子。

``` js
<%- is_post() %>
```

### 是页面

检查当前页面是否是一个页面。

``` js
<%- is_page() %>
```

### 是存档

检查当前页面是否为归档页面。

``` js
<%- is_archive() %>
```

### 是 年

检查当前页面是否为年度归档页面。

``` js
<%- is_year() %>
```

### 是月

检查当前页面是否为每月归档页面。

``` js
<%- is_month() %>
```

### 是类别

检查当前页面是否为类别页面。 如果给定了一个字符串作为参数，请检查当前页面是否与给定的类别相匹配。

``` js
<%- is_category() %>
<%- is_category('hobby') %>
```

### 是标签

检查当前页面是否为标签页。 如果给定字符串作为参数，请检查当前页面是否匹配给定的标签。

``` js
<%- is_tag() %>
<%- is_tag('hobby') %>
```

## 字符串操作

### 修饰

删除字符串的前缀和尾随空格。

``` js
<%- 修剪(字符串) %>
```

### strip_html

将字符串中的所有HTML标签都卫生化。

``` js
<%- strip_html(字符串) %>
```

**示例：**

``` js
<%- strip_html('It\'s not <b>important</b> 再重要！') %>
// 它不再重要！
```

### titlecase

将字符串转换为正确的标题上限.

``` js
<%- titlecase(string) %>
```

**示例：**

``` js
<%- titlecase('这是一个小程序') %>
# 这是一个苹果
```

### markdown

渲染一个带Markdown的字符串。

``` js
<%- markdown(str) %>
```

**示例：**

``` js
<%- Markdown('make me **strong**') %>
// make me <strong>strong</strong>
```

### 渲染

渲染一个字符串。

``` js
<%- 渲染(str, 引擎, [options]) %>
```

**示例：**

``` js
<%- render('p(class="example") Test', 'pug'); %>
// <p class="example">Test</p>
```

See [Rendering](https://hexo.io/api/rendering) for more details.

### 自动换行

将文本包装成不超过 `长度` `长度` 默认是 80。

``` js
<%- word_wrapp(str, [length]) %>
```

**示例：**

``` js
<%- word_wrapp('一次, 8) %>
// 一次在\n 一次时间
```

### 截图

在指定 `长度` 之后截断文本。 默认为30个字符。

``` js
<%- 截断(文本， [options]) %>
```

**示例：**

``` js
<%- 截断('一次在远离世界的世界上很远', {length: 17}) %>
// 偶数...

<%- 截断('一次在远离世界的世界上很远', {length: 17, separator: ' '}) %>
// 一次...

<%- 截断(他们发现很多人睡得更好。', {length: 25, 忽略: '... （续）'}) %>
// 他们...
```

### 转义_html

在字符串中转义HTML实体。

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

| 选项   | 描述                           | 默认设置    |
| ---- | ---------------------------- | ------- |
| `缓存` | 缓存内容 (使用片段缓存)                | `false` |
| `仅限` | 严格的本地变量。 仅使用模板中的 `本地设置的` 变量。 | `false` |

### 片段缓存

将内容放入片段中。 它将内容保存在片段内，并在下一个请求出现时为缓存服务。

``` js
<%- fragment_cache(id, fn);
```

**示例：**

``` js
<%- fragment_cache('header', function()voir
  return '<header></header>';
}) %>
```

## 日期 & 时间

### 日期

插入格式化日期。 `日期` 可以是统一的时间，ISO字符串，日期对象，或者 [Moment.js][] 对象。 `格式` 是 `日期格式` 默认设置。

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

以 XML 格式插入日期。 `日期` 可以是统一的时间，ISO字符串，日期对象，或者 [Moment.js][] 对象。

``` js
<%- date_xml(date) %>
```

**示例：**

``` js
<%- date_xml(Date.now ()) %>
// 2013-01-01T00:00:00.00.000Z
```

### 时间

插入格式化时间。 `日期` 可以是统一的时间，ISO字符串，日期对象，或者 [Moment.js][] 对象。 `格式` 是 `时间格式` 默认设置。

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

插入格式化的日期和时间。 `日期` 可以是统一的时间，ISO字符串，日期对象，或者 [Moment.js][] 对象。 `格式` 是 `date_format + time_format` 默认设置。

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

[Moment.js][] 库。

## 列表

### 列表类别

插入所有类别的列表。

``` js
<%- list_categories([options]) %>
```

| 选项       | 描述                                                         | 默认设置 |
| -------- | ---------------------------------------------------------- | ---- |
| `排序方式`   | 分类顺序                                                       | 名称   |
| `订单`     | 排序。 `1`, `` 按升序排列； `-1`, `按降序排序` 按降序排序                     | 1    |
| `显示计数`   | 显示每个类别的帖子数                                                 | true |
| `样式`     | 显示分类列表的样式。 `列表` 在无序列表中显示类别。 使用 `false` 或任何其他值禁用它。          | 邮件列表 |
| `分隔符`    | 类别之间的分隔符。 (仅当 `样式` 不是 `列表`)                                | ,    |
| `深度：`    | 要显示的分类级别. `0` 显示所有类别和子类别； `-1` 类似于 `0` 但以平面显示； `1` 只显示顶级分类 | 0    |
| `类`      | 类别列表的类名。                                                   | 类别   |
| `转换`     | 更改类别名称显示的函数。                                               |      |
| `suffix` | 添加一个后缀到链接。                                                 | 无    |

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

插入所有标签的列表。

``` js
<%- list_tags([options]) %>
```

| 选项       | 描述                                                         | 默认设置 |
| -------- | ---------------------------------------------------------- | ---- |
| `排序方式`   | 分类顺序                                                       | 名称   |
| `订单`     | 排序。 `1`, `` 按升序排列； `-1`, `按降序排序` 按降序排序                     | 1    |
| `显示计数`   | 显示每个标签的文章数量                                                | true |
| `样式`     | 显示标签列表的样式。 `列表` 在无序列表中显示标签。 使用 `false` 或任何其他值禁用它。          | 邮件列表 |
| `分隔符`    | 类别之间的分隔符。 (仅当 `样式` 不是 `列表`)                                | ,    |
| `类`      | 标签列表类名称 (字符串) 或自定义每个标签类(对象，见下文)。                           | 标签   |
| `转换`     | 更改标签名称显示的函数。 请参阅 [list_categories](#list-categories) 中的示例。 |      |
| `金额`     | 要显示的标签数量 (0= 无限制)                                          | 0    |
| `suffix` | 添加一个后缀到链接。                                                 | 无    |

类高级自定义：

| 选项         | 描述                                                                 | 默认设置                                                     |
| ---------- | ------------------------------------------------------------------ | -------------------------------------------------------- |
| `class.ul` | `<ul>` 类名 (仅适用于 `列表`)                                        | `标签列表` (列表样式)                                            |
| `class.li` | `<li>` 类名 (仅适用于 `列表`)                                        | `标签列表项` (列表样式)                                           |
| `class.a`  | `<a>` 类名称                                                    | `标签列表链接` (列表样式) `标签链接` (普通样式)                            |
| `标签`       | `<span>` 标签存储的类名 (仅用于正常风格，当 `类时。 abel` 设置标签为 `<span>`) | `标签` (正常风格)                                              |
| `计数`       | `<span>` 标签计数器存储的类名 (仅当 `显示计数` 是 `true`)                     | `tag-list-count` (list style) `tag-count` (normal style) |

示例：

```ejs
<%- list_tags(site.tags, {class: 'classtest', style: false, separator: ' | '}) %>
<%- list_tags(site. ags, {class: 'classtest', style: 'list'}>
<%- list_tags(站点)。 ags, {class: {ul: 'ulululul', li: 'lilili', aaa', count : 'ccc'}, style: false, separator: '| '}) %>
<%- list_tags(site ags, {class: {ul: 'ulululul', li: 'lilili', : 'aaa', count: 'ccc'}, 样式: 'list'}) %>
```

### 列表归档文件

插入档案列表。

``` js
<%- list_archives([options]) %>
```

| 选项     | 描述                                                         | 默认设置      |
| ------ | ---------------------------------------------------------- | --------- |
| `类型`   | Type. 此值可以是 `每年的` 或 `每月的`。                                 | 每月的       |
| `订单`   | 排序。 `1`, `` 按升序排列； `-1`, `按降序排序` 按降序排序                     | 1         |
| `显示计数` | 显示每个归档的帖子数                                                 | true      |
| `格式`   | 日期格式                                                       | MMMM YYYY |
| `样式`   | 显示归档列表的样式。 `列表` 在无序列表中显示归档。 使用 `false` 或任何其他值禁用它。          | 邮件列表      |
| `分隔符`  | 归档之间的分隔符。 (仅当 `样式` 不是 `列表`)                                | ,         |
| `类`    | 归档列表的类名称。                                                  | 存档        |
| `转换`   | 更改归档名称显示的函数。 请参阅 [list_categories](#list-categories) 中的示例。 |           |

### 列表帖子

插入帖子列表。

``` js
<%- list_poss([options]) %>
```

| 选项     | 描述                                                         | 默认设置 |
| ------ | ---------------------------------------------------------- | ---- |
| `排序方式` | 帖子顺序                                                       | 日期   |
| `订单`   | 排序。 `1`, `` 按升序排列； `-1`, `按降序排序` 按降序排序                     | 1    |
| `样式`   | 显示帖子列表的样式。 `列表` 显示无序列表中的帖子。 使用 `false` 或任何其他值禁用它。          | 邮件列表 |
| `分隔符`  | 帖子之间的分隔符。 (仅当 `样式` 不是 `列表`)                                | ,    |
| `类`    | 帖子列表的类名称。                                                  | 发帖   |
| `金额`   | 要显示的帖子数量 (0=无限制)                                           | 6    |
| `转换`   | 更改帖子名称显示的函数。 请参阅 [list_categories](#list-categories) 中的示例。 |      |

### tagcloud

插入标签云。

``` js
<%- tagcloud([tags], [options]) %>
```

| 选项                     | 描述                                                                                                                       | 默认设置  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------ | ----- |
| `最小字体`                 | 最小字体大小                                                                                                                   | 10    |
| `max_font`             | 最大字体大小                                                                                                                   | 20    |
| `单位`                   | 字体大小单位                                                                                                                   | px    |
| `金额`                   | 标签总数                                                                                                                     | 无限制   |
| `排序方式`                 | 标签顺序                                                                                                                     | 名称    |
| `订单`                   | 排序。 `1`, `` 等于升序； `-1`, `desc` 降序排列                                                                                      | 1     |
| `颜色`                   | 色彩化标签云                                                                                                                   | false |
| `开始颜色`                 | 开始颜色。 您可以使用十六进制(`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hslam (283, 100%，50%，1)`或 [颜色关键字][]。 此选项仅在 `颜色` 为真时有效。 |       |
| `结束颜色`                 | 结束颜色。 您可以使用十六进制(`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hslam (283, 100%，50%，1)`或 [颜色关键字][]。 此选项仅在 `颜色` 为真时有效。 |       |
| `类`                    | 标签类名称前缀                                                                                                                  |       |
| `关卡`                   | 不同类名称的数量。 此选项仅在设置了 `类` 时有效。                                                                                              | 10    |
| `show_count` (+6.3.0)  | 显示每个标签的文章数量                                                                                                              | false |
| `count_class` (+6.3.0) | 标签数量的类名称                                                                                                                 | 计数    |

**示例：**

``` js
// Default options
<%- tagcloud() %>

// Limit number of tags to 30
<%- tagcloud({amount: 30}) %>
```

## 其他事项

### 分页器

插入分页器。

``` js
<%- 分页符(选项) %>
```

| 选项                            | 描述                                                | 默认设置     |
| ----------------------------- | ------------------------------------------------- | -------- |
| `基数`                          | 基本网址                                              | /        |
| `格式`                          | URL 格式                                            | page/%d/ |
| `总计`                          | 页面数                                               | 1        |
| `当前的`                         | 当前页面编号                                            | 0        |
| `前置文本`                        | 上一页的链接文本。 只有在 `推送` 设置为 true时才能正常工作。               | 上一个      |
| `下一文本`                        | 下一页的链接文本。 只有在 `推送` 设置为 true时才能正常工作。               | 下一个      |
| `空格`                          | 空间文本                                              | &hellp;  |
| `下一个`                         | 显示上一个和下一个链接                                       | true     |
| `结束大小`                        | 开始和结束时显示的页面数                                      | 1        |
| `中大小`                         | 当前页面之间显示的页面数量，但不包括当前页面                            | 2        |
| `显示所有`                        | 显示所有页面。 如果设置为 true， `end_size` 和 `mid_size` 将无法工作 | false    |
| `跳转`                          | 转义HTML标签                                          | true     |
| `page_class` (+6.3.0)         | 页面类名称                                             | `页码`     |
| `current_class` (+6.3.0)      | 当前页面类名称                                           | `当前的`    |
| `space_class` (+6.3.0)        | 空间类名称                                             | `空格`     |
| `prev_class` (+6.3.0)         | 上一个页面类名称                                          | `扩展上一个`  |
| `下一类` (+6.3.0)                | 下一页类名称                                            | `扩展下一个`  |
| `force_prevent_next` (+6.3.0) | 强制显示上一个和下一个链接                                     | false    |


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

插入一个 Google 搜索表。

``` js
<%- search_form(选项) %>
```

| 选项   | 描述                                      | 默认设置  |
| ---- | --------------------------------------- | ----- |
| `类`  | 表单的类名称                                  | 搜索表单  |
| `文本` | 搜索提示词                                   | 搜索    |
| `按钮` | 显示搜索按钮。 该值可以是布尔值或字符串。 如果值是字符串，它将是按钮的文本。 | false |

### 数字格式

格式化数字。

``` js
<%- 数字格式(数、 [options]) %>
```

| 选项    | 描述                            | 默认设置  |
| ----- | ----------------------------- | ----- |
| `精度`  | 数字的精确度。 值可以是 `false` 或一个非负整数。 | false |
| `分隔符` | 千个分隔符                         | ,     |
| `分隔符` | 分数和整数之间的分隔符。                  | .     |

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

插入 [生成器标签](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)

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

| 选项             | 描述                                   | 默认设置                                  |
| -------------- | ------------------------------------ | ------------------------------------- |
| `标题`           | 页面标题 (`og:title`)                    | `page.title`                          |
| `类型`           | 页面类型 (`og:type`)                     | 博客                                    |
| `网址`           | 页面 URL (`og:url`)                    | `网址`                                  |
| `图片`           | 页面图像 (`og:image`)                    | 内容中的所有图像                              |
| `作者`           | 文章作者 (`og:article:author`)           | `作者`                                  |
| `日期`           | 文章发布时间 (`og:article:published_time`) | 页面发布时间                                |
| `已更新`          | 文章修改时间(`og:article:modified_time`)   | 页面修改时间                                |
| `语言`           | 文章语言 (`og:locale`)                   | `页面.lang || 页面.语言 || config.language` |
| `站点名称`         | 站点名称 (`og:site_name`)                | `config.title`                        |
| `描述`           | 页面描述 (`og:description`)              | 页面节录或内容的前200个字符                       |
| `twitter_card` | Twitter 卡类型 (`twitter:card`          | summary                               |
| `twitter_id`   | Twitter ID (`twitter:creator`)       |                                       |
| `Twitter_site` | Twitter 站点 (`twitter:site`)          |                                       |
| `谷歌加成`         | Google+ 个人资料链接                       |                                       |
| `fb_admins`    | Facebook管理员 ID                       |                                       |
| `fb_app_id`    | Facebook 应用程序 ID                     |                                       |

### 托克

解析内容中的所有标题标签 (h1~h6) 并插入一个内容表。

``` js
<%- toc(str, [options]) %>
```

| 选项                      | 描述            | 默认设置              |
| ----------------------- | ------------- | ----------------- |
| `类`                     | 类名            | `托克`              |
| `class_item` (+6.3.0)   | 项目的类名         | `${class}-item`   |
| `class_link` (+6.3.0)   | 链接类名称         | `${class}-link`   |
| `class_text` (+6.3.0)   | 文本类名称         | `${class}-text`   |
| `class_child` (+6.3.0)  | 子类别名称         | `${class}-child`  |
| `class_number` (+6.3.0) | 类编号名称         | `${class}-number` |
| `class_level` (+6.3.0)  | 级别的类名称前缀      | `${class}-level`  |
| `邮件列表编号`                | 显示列表编号        | true              |
| `最大深度`                  | 生成toc 的最大标题深度 | 6                 |
| `最小深度`                  | 生成toc 的最小标题深度 | 1                 |

**示例：**

``` js
<%- toc(page.content) %>
```

#### 无编号数据 (+6.1.0)

属性为 `的标头-unnumbered="true"` 将被标记为未编号(列表号将不会显示)。

{% note warn "警告!" %}
若要使用 `data-toc-unnumbered="true"`，渲染器必须有添加CSS 类的选项。

请参阅以下PRs。

- https://github.com/hexojs/hexo/pull/4871
- https://github.com/hexojs/hexo-util/pull/269
- https://github.com/hexojs/hexo-render-markdown-it/pull/174
{% endnote %}

[颜色关键字]: http://www.w3.org/TR/css3-color/#svg-color
[Moment.js]: http://momentjs.com/
[打开图]: http://ogp.me/
