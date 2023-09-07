---
title: 标签插件
---

标签插件与帖子标签不同。 他们被移除，为您快速添加特定内容给您的帖子提供了一个有用的方式。

虽然您可以以任何格式写您的帖子，但标签插件总是可用的，语法保持不变。

{% youtube I07XMi7MHd4 %}

_Tag plugins should not be wrapped inside Markdown syntax, e.g. `[]({% post_path lorem-ipsum %})` is not supported._

## 阻止引用

可选的作者、源和标题信息用于添加引文到您的帖子。

**别名：** 引用

```
{% blockquate [author[, source]] [link] [source_link_title] %}
内容
{% endblockquote %}
```

### 示例：

**没有参数。 普通方块引用。**

```
{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}
```

{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

**从一本书中引用**

```
{% blockquate quotes David Levithan, Wide Awake %}
不要仅仅为自己寻求幸福。 为所有人寻求幸福。 善良。 通过仁慈。
{% endblockquote %}
```

{% blocklease quoting David Levithan, Wide Awake %}
不要仅仅为自己寻求幸福。 为所有人寻求幸福。 善良。 通过仁慈。
{% endblockquote %}

**来自 Twitter 的引用**

```
{% blockquate @DevDocs https://twitter.com/devdocs/status/356095192085962752%}
NEW: DevDocs 现在带有语法高亮。 http://devdocs.io
{% endblockquote %}
```

{% blockquate @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs 现在带有语法高亮。 http://devdocs.io
{% endblockquote %}

**引用网页上的文章**

```
{% blockquate Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
每次互动都是宝贵的，也是欣赏的机会。
{% endblockquote %}
```

{% blockquate Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcoming to-island-marketing.html Welcome to Island Marketing %}
每次互动都是宝贵的，也是欣喜的机会。
{% endblockquote %}

## 代码块

添加代码片段到您的帖子的有用功能。

**Alias:** code

```
{% codeblock [title] [lang:lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}
```

以 `选项:value` 格式指定额外的选项，例如 `line_number:false first_line:5`

| 额外选项   | 描述                                                                                        | 默认设置   |
| ------ | ----------------------------------------------------------------------------------------- | ------ |
| `行数`   | 显示行号                                                                                      | `true` |
| `线性阈值` | 只在代码块的行数超过此阈值时显示行数。                                                                       | `0`    |
| `高亮显示` | 启用代码高亮显示                                                                                  | `true` |
| `第一行`  | 指定第一行号                                                                                    | `1`    |
| `标记`   | 行高亮显示特定线(s)，每个值用逗号隔开。 指定数字范围使用破折号<br>示例： `mark:1,4-7,10` 将标记第 1, 4 到 7 和 10 行。      |        |
| `换行`   | 将代码块换成 [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) | `true` |

### 示例：

**纯代码块**

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

**添加一个标题到代码块**

```
{% codeblock Array.map %}
数组地图(回调[, thisArg])
{% endcodeblock %}
```

{% codeblock Array.map %}
array.map(调用[, thisArg])
{% endcodeblock %}

**添加一个标题和一个 URL**

```
{% codeblock _.cord http://underrejs.org/#compted Underscore.js %}
_.compact([0, 1, false, 2, ', 3]);
=> [1, 2, 3]
{% endcodeblock %}
```

{% codeblock _.dold http://underrejs.org/#compound Underscore.js %}
_.compact([0, 1, false, 2, ', 3]); => [1, 2, 3]
{% endcodeblock %}

## Backtick 代码块

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

## jsFiddle

嵌入jsFiddle 代码片段：

```
{% jsfiddle shorttag [tabs] [skin] [width] [height]%}
```

## 基斯文

要嵌入 Gist 代码片段：

```
{% gist gist_id [filename]%}
```

## iframe

要嵌入 iframe ：

```
{% iframe url [width] [height] %}
```

## 图片

插入具有指定大小的图像。

```
{% img [class names] /path/to/image [width] [height] '"title text" "alt text"" %}
```

## 链接

以 `target="_blank"` 属性插入一个链接。

```
{% link text url [external] [title]%}
```

## 包含代码

在 `source/downloads/code` 文件夹中插入代码片段。 可以通过配置中的 `code_dir` 选项指定文件夹位置。

```
{% include_code [title] [lang:lang:language] [从:line] [to:line] path/to/file %}
```

### 示例：

**嵌入测试.js的全部内容**

```
{% include_code lang:javascript test.js %}
```

**仅嵌入行 3**

```
{% include_code lang:javascript from:3 to:3 test.js %}
```

**嵌入行5-8**

```
{% include_code lang:javascript from:5 to:8 test.js %}
```

**嵌入到文件末尾的第5行**

```
{% include_code lang:javascript from:5 test.js %}
```

**嵌入第1至第8行**

```
{% include_code lang:javascript to:8 test.js %}
```

## YouTube

插入YouTube视频。

```
{% youtube video_id [type] [cookie]%}
```

### 示例：

**嵌入视频**

```
{% youtube lJIrF4YjHfQ %}
```

**嵌入播放列表**

```
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' %}
```

**启用隐私增强模式**

YouTube的 cookie 没有在此模式下使用。

```
{% youtube lJIrF4YjHfQ false %}
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' false %}
```

## Vimeo

插入响应或指定大小 Vimeo 视频。

```
{% vimeo video_id [width] [height]%}
```

## 包含帖子

包含到其他帖子的链接。

```
{% post_path filename %}
{% post_link filename [title] [escape] %}
```

当使用此标签时，您可以忽略永久链接和文件夹信息，例如语言和日期。

例如： `{% raw %}{% post_link how-to-bake-a-cake %}{% endraw %}`

只要帖子的文件名是 `如何拿起蛋糕，这个操作就会奏效。 d`, 即使该员额位于 `来源/帖子/帖子//2015-02-my-family-sper` 并拥有永久链接 `2018/en/howto bake-a-cake`

您可以自定义显示文本，而不是显示帖子的标题。

默认情况下，帖子的标题和自定义文本会被撤销。 您可以使用 `转义` 选项来禁用转义。

例如：

**显示帖子的标题**

`{% raw %}{% post_link hexo-3-8-released %}{% endraw %}`

{% post_link hexo-3-8-released %}

**显示自定义文本。**

`{% raw %}{% post_link hexo-3-8-released 'Link to a post' %}{% endraw %}`

{% post_link hexo-3-8-released 'Link to a post' %}

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

Include post assets, to be used in conjunction with [`post_asset_folder`](/docs/asset-folders).

```
{% asset_path filename %}
{% asset_img [class names] slug [width] [height] [titure [alt text]] %}
{% asset_link filename [title] [escape]%}
```

### 嵌入图像

_hexo-renderer-marked 3.1.0+ can (optionally) resolves the post's path of an image automatically, refer to [this section](/docs/asset-folders#Embedding-an-image-using-markdown) on how to enable it._

"foo.jpg" is located at `http://example.com/2020/01/02/hello/foo.jpg`.

**默认 (没有选项)**

`{% asset_img foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg">
```

**自定义类**

`{% asset_img post-image foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" class="post-image">
```

**显示大小**

`{% asset_img foo.jpg 500 400 %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" width="500" height="400">
```

**标题 & Alt**

`{% asset_img foo.jpg "lorem ipsum'dolor'" %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" title="lorem ipsum" alt="dolor">
```

## 原始文件

如果某些内容在您的帖子中造成处理问题，用 `原始` 标签打包，以避免渲染错误。

```
{% raw %}
内容
{% endraw %}
```

## 文章摘要

Use text placed before the `<!-- more -->` tag as an excerpt for the post. `摘录： <a href="/docs/front-matter#Settings-amp-Their-Default-Values">前事项</a>中的` 值，如果指定，将成为先例。

**示例：**

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
<!-- more -->
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
