---
title: 标签插件（Tag Plugins）
---

标签插件和 Front-matter 中的标签不同，它们是用于在文章中快速插入特定内容的插件。 他们被移除，为您快速添加特定内容给您的帖子提供了一个有用的方式。

虽然你可以使用任何格式书写你的文章，但是标签插件永远可用，且语法也都是一致的。

{% youtube I07XMi7MHd4 %}

_标签插件不应该被包裹在 Markdown 语法中，例如： `[]({% post_path lorem-ipsum %})` 是不被支持的。_

## 引用块

可选的作者、源和标题信息用于添加引文到您的帖子。

**别号：** quote

```
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

### 示例

**没有参数。 普通方块引用。**

```
{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}
```

{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

**引用书上的句子**

```
{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy.
{% endblockquote %} 为所有人寻求幸福。 善良。 通过仁慈。
{% endblockquote %}
```

{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy. 为所有人寻求幸福。 善良。 通过仁慈。
{% endblockquote %}

**引用 Twitter**

```
{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io
{% endblockquote %} http://devdocs.io
{% endblockquote %}
```

{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs now comes with syntax highlighting. http://devdocs.io http://devdocs.io
{% endblockquote %}

**引用网络上的文章**

```
{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}
{% endblockquote %}
```

{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
每次互动都是宝贵的，也是欣喜的机会。
{% endblockquote %}

## 代码块

添加代码片段到您的帖子的有用功能。

**别名：** code

```
{% codeblock [title] [lang:lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}
```

以 `option:value` 的格式指定额外选项，例如：`line_number:false first_line:5`。

| 额外选项   | 描述                                                                                         | 默认值    |
| ------ | ------------------------------------------------------------------------------------------ | ------ |
| `行数`   | 显示行号                                                                                       | `true` |
| `线性阈值` | 只有代码块的行数超过该阈值，才显示行数                                                                        | `0`    |
| `高亮显示` | 启用代码高亮                                                                                     | `true` |
| `第一行`  | 指定第一个行号                                                                                    | `1`    |
| `标记`   | 突出显示特定的行，每个值用逗号分隔。 使用破折号指定数字范围<br>例如： `mark:1,4-7,10` 将标记第1、4至7和10行                  |        |
| `换行`   | 用 [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) 包裹代码块 | `true` |

### 示例

**普通的代码块**

```
{% codeblock %}
警报('Hello World!');
{% endcodeblock %}
```

{% codeblock %}
警报('Hello World!');
{% endcodeblock %}

**指定语言**

```
{% codeblock lang:objc %}
[矩形设置X: 10 y: 10 宽度: 20 height: 20];
{% endcodeblock %}
```

{% codeblock lang:objc %}
[矩形设置：10：10：10：10：10：10：20：20]；
{% endcodeblock %}

**在文章中插入代码。**

```
{% codeblock Array.map %}
数组地图(回调[, thisArg])
{% endcodeblock %}
```

{% codeblock Array.map %}
array.map(调用[, thisArg])
{% endcodeblock %}

**附加说明和网址**

```
{% codeblock _.cord http://underrejs.org/#compted Underscore.js %}
_.compact([0, 1, false, 2, ', 3]);
=> [1, 2, 3]
{% endcodeblock %}
```

{% codeblock _.dold http://underrejs.org/#compound Underscore.js %}
_.compact([0, 1, false, 2, ', 3]); => [1, 2, 3]
{% endcodeblock %}

## 反引号代码块

这与使用代码块相同，但是使用三个背景来划分方块。

{% raw %}
&#96`[language] [title] [url] [链接文本]
代码片段
&#96;`
{% endraw %}

## 拉取报价

要将拉取引号添加到您的帖子：

```
{% pullquote [class] %}
content
{% endpullquote %}
```

## jsFiddle (`v7.0.0` 中被移除)

{% note warn %}
如果你正在使用 `v7.0.0+`，请使用 [hexo-tag-embed](https://github.com/hexojs/hexo-tag-embed) 替代。
{% endnote %}

在文章中嵌入 jsFiddle。

```
{% jsfiddle shorttag [tabs] [skin] [width] [height]%}
```

## Gist (`v7.0.0` 中被移除)

{% note warn %}
如果你正在使用 `v7.0.0+`，请使用 [hexo-tag-embed](https://github.com/hexojs/hexo-tag-embed) 替代。
{% endnote %}

要嵌入 Gist 代码片段：

```
{% gist gist_id [filename]%}
```

## iframe

在文章中插入 iframe。

```
{% iframe url [width] [height] %}
```

## 图片

在文章中插入指定大小的图片。

```
{% img [class names] /path/to/image [width] [height] '"title text" "alt text"" %}
```

## 链接

在文章中插入链接，并自动给外部链接添加 `target="_blank"` 属性。

```
{% link text url [external] [title]%}
```

## 包含代码

插入 `source/downloads/code` 文件夹内的代码文件。 `source/downloads/code` 不是固定的，取决于你在配置文件中 `code_dir` 的配置。

```
{% include_code [title] [lang:language] [from:line] [to:line] path/to/file %}
```

### 示例

**嵌入 test.js 文件全文**

```
{% include_code lang:javascript test.js %}
```

**只嵌入第 3 行**

```
{% include_code lang:javascript from:3 to:3 test.js %}
```

**嵌入第 5 行至第 8 行**

```
{% include_code lang:javascript from:5 to:8 test.js %}
```

**嵌入第 5 行至文件结束**

```
{% include_code lang:javascript from:5 test.js %}
```

**嵌入第 1 行至第 8 行**

```
{% include_code lang:javascript to:8 test.js %}
```

## Youtube (`v7.0.0` 中被移除)

{% note warn %}
如果你正在使用 `v7.0.0+`，请使用 [hexo-tag-embed](https://github.com/hexojs/hexo-tag-embed) 替代。
{% endnote %}

在文章中插入 Youtube 视频。

```
{% youtube video_id [type] [cookie]%}
```

### 示例

**视频**

```
{% youtube lJIrF4YjHfQ %}
```

**播放列表**

```
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' %}
```

**隐私模式**

在这种模式下，禁用 YouTube cookie

```
{% youtube lJIrF4YjHfQ false %}
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' false %}
```

## Vimeo (`v7.0.0` 中被移除)

{% note warn %}
如果你正在使用 `v7.0.0+`，请使用 [hexo-tag-embed](https://github.com/hexojs/hexo-tag-embed) 替代。
{% endnote %}

插入响应或指定大小 Vimeo 视频。

```
{% vimeo video_id [width] [height] %}
```

## 包含帖子

包含到其他帖子的链接。

```
{% post_path filename %}
{% post_link filename [title] [escape] %}
```

在使用此标签时可以忽略文章文件所在的路径或者文章的永久链接信息、如语言、日期。

例如，在文章中使用 `{% raw %}{% post_link how-to-bake-a-cake %}{% endraw %}` 时，只需有一个名为 `how-to-bake-a-cake.md` 的文章文件即可。

只要帖子的文件名是 `如何拿起蛋糕，这个操作就会奏效。 d`, 即使该员额位于 `来源/帖子/帖子//2015-02-my-family-sper` 并拥有永久链接 `2018/en/howto bake-a-cake`

默认链接文字是文章的标题，你也可以自定义要显示的文本。

默认对文章的标题和自定义标题里的特殊字符进行转义。 可以使用 `escape` 选项，禁止对特殊字符进行转义。

例如：

**显示帖子的标题**

`{% raw %}{% post_link hexo-3-8-released %}{% endraw %}`

{% post_link hexo-3-8-released %}

**显示自定义文本。**

`{% raw %}{% post_link hexo-3-8-released '通往文章的链接' %}{% endraw %}`

{% post_link hexo-3-8-released '通往文章的链接' %}

**转义标题。**

```
{% post_link hexo-4-released '如何在标题中使用 <b> 标签' %}
```
{% post_link hexo-4-released 'How to use <b> tag in title' %}

**不要跳过标题。**

```
{% post_link hexo-4-released '<b>bold</b> customary title' false %}
```

{% post_link hexo-4-released '<b>bold</b> customary title' false %}

## 包括资产

引用文章的资源，与 [资源文件夹](/zh-cn/docs/asset-folders) 一起使用。

```
{% asset_path filename %}
{% asset_img [class names] slug [width] [height] [titure [alt text]] %}
{% asset_link filename [title] [escape]%}
```

### 嵌入图片

_hexo-renderer-marked 3.1.0+ 可以（可选）自动解析图片的文章路径，参考 [本节](/zh-cn/docs/asset-folders#使用-Markdown-嵌入图片) 如何启用它。_

"foo.jpg" 位于 `http://example.com/2020/01/02/hello/foo.jpg`。

**默认（无选项）**

`{% asset_img foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg">
```

**自定义 class 属性**

`{% asset_img post-image foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" class="post-image">
```

**展示尺寸**

`{% asset_img foo.jpg 500 400 %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" width="500" height="400">
```

**title 和 alt 属性**

`{% asset_img logo.svg "lorem ipsum'dolor'" %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" title="lorem ipsum" alt="dolor">
```

## URL

### url_for (7.0.0+)

返回一个带有根路径前缀的URL。输出将会自动编码。

```
{% url_for text path [relative] %}
```

**示例：**

``` yml
_config.yml
root: /blog/ # example
```

``` 
{% url_for blog index.html %}
```

``` html
<a href="/blog/index.html">blog</a>
```

是否输出相对链接，默认遵循配置文件中 `relative_link` 的值
例如， post/page 的路径值可能是 `/foo/bar/index.html`

``` yml
_config.yml
relative_link: true
```

```
{% url_for blog index.html %}
```

``` html
<a href="../../index.html">blog</a>
```

即使配置文件中启用了 `relative_link`，你也可以使用 `relative` 参数禁用相对链接输出，反之亦然

```
{% url_for blog index.html false %}
```

``` html
<a href="/index.html">blog</a>
```

### full_url_for (7.0.0+)

返回一个以 `config.url` 为前缀的URL。输出将会自动编码。

```
{% full_url_for text path %}
```

**示例：**

``` yml
_config.yml
url: https://example.com/blog # example
```

```
{% full_url_for index /a/path %}
```

``` html
<a href="https://example.com/blog/a/path">index</a>
```

## Raw

如果某些内容在您的帖子中造成处理问题，用 `原始` 标签打包，以避免渲染错误。

```
{% raw %}
内容
{% endraw %}
```

## 文章摘要

在文章中使用 `<!-- more -->`，那么 `<!-- more -->` 之前的文字将会被视为摘要。 `摘录： <a href="/docs/front-matter#Settings-amp-Their-Default-Values">前事项</a>中的` 值，如果指定，将成为先例。

**例如：**

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
<!-- more -->
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
