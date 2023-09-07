---
title: 写作
---

{% youtube HLJ9jJy7CMg %}

你可以执行下列命令来创建一篇新文章或者新的页面。

``` bash
美元新增 [layout] <title>
```

`post` is the default `layout`, but you can supply your own. 您可以在命令中指定文章的布局（layout），默认为 `post`，可以通过修改 `_config.yml` 中的 `default_layout` 参数来指定默认布局。 您可以在命令中指定文章的布局（layout），默认为 `post`，可以通过修改 `_config.yml` 中的 `default_layout` 参数来指定默认布局。

## 布局（Layout）

Hexo 有三种默认布局：`post`、`page` 和 `draft`。 每个文件创建的文件被保存到不同的路径。 Files created by each of them is saved to a different path. Newly created posts are saved to the `source/_posts` folder.

| 布局   | 路径       |
| ---- | -------- |
| `发帖` | `来源/帖子`  |
| `页面` | `来源`     |
| `草稿` | `来源/_草稿` |

{% note tip 禁用布局 %}
如果你不希望一篇文章（post/page）使用主题处理，请在它的 front-matter 中设置 `layout: false`。 详情请参考[本节](/zh-cn/docs/front-matter#布局)。
{% endnote %}

## 文件名称

默认情况下，Hexo使用帖子标题作为其文件名。 您可以编辑 `_config.yml` 中的 `新的 post_name` 设置更改默认文件名。 例如， `:year :month-:day:title.md` 将在帖子创建日期前修复文件名。 你可以使用以下占位符：

| 占位符      | 描述                   |
| -------- | -------------------- |
| `:title` | 标题（小写，空格将会被替换为短杠）    |
| `:年`     | 建立的年份，比如， `2015`     |
| `:月`     | 建立的月份（有前导零），比如， `04` |
| `:i_月`   | 建立的月份（无前导零），比如， `4`  |
| `:day`   | 建立的日期（有前导零），比如， `07` |
| `:i_day` | 建立的日期（无前导零），比如， `7`  |

## 草稿

以前，我们在 Hexo: `草案` 中提到了一个特殊的布局。 以此布局初始化的帖子被保存到 `源/_草稿` 文件夹。 Previously, we mentioned a special layout in Hexo: `draft`. Posts initialized with this layout are saved to the `source/_drafts` folder. You can use the `publish` command to move drafts to the `source/_posts` folder. `publish` works in a similar way to the `new` command. `发布` 工作方式类似于 `新的` 命令。

``` bash
$十六进制发布 [layout] <title>
```

草稿不默认显示。 Drafts are not displayed by default. You can add the `--draft` option when running Hexo or enable the `render_drafts` setting in `_config.yml` to render drafts.

## 手柄武器库

在新建文章时，Hexo 会根据 `scaffolds` 文件夹内相对应的文件来建立文件，例如： For example: 例如：

``` bash
$ 十六进制新照片"My Gallery
```

在执行这行指令时，Hexo 会尝试在 `scaffolds` 文件夹中寻找 `photo.md`，并根据其内容建立文章，以下是您可以在模版中使用的变量： The following placeholders are available in scaffolds: 以下占位符可用于scaffolds：

| 占位符  | 描述     |
| ---- | ------ |
| `布局` | 布局     |
| `标题` | 标题     |
| `日期` | 文件建立日期 |

## 支持的格式

Hexo 支持以任何格式书写文章，只要安装了相应的渲染插件。

例如，Hexo 默认安装了 `hexo-renderer-marked` 和 `hexo-renderer-ejs`，因此你不仅可以用 Markdown 写作，你还可以用 EJS 写作。 如果你安装了 `hexo-renderer-pug`，你甚至可以用 Pug 模板语言书写文章。

只需要将文章的扩展名从 `md` 改成 `ejs`，Hexo 就会使用 `hexo-renderer-ejs` 渲染这个文件，其他格式同理。
