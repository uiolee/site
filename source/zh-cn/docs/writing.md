---
title: 写入中
---

{% youtube AIqBubK6ZLc %}

要创建一个新的帖子或一个新的页面，您可以运行以下命令：

``` bash
美元新增 [layout] <title>
```

`post` is the default `layout`, but you can supply your own. You can change the default layout by editing the `default_layout` setting in `_config.yml`.

## 布局

十六进制有三个默认布局： `发布`、 `页面` 和 `草稿`。 每个文件创建的文件被保存到不同的路径。 新创建的帖子被保存到 `源/_post` 文件夹。

| 布局   | 路径       |
| ---- | -------- |
| `发帖` | `来源/帖子`  |
| `页面` | `来源`     |
| `草稿` | `来源/_草稿` |

{% note tip Disabling layout %}
如果您不想用主题处理文章 (post/page)，请设置 `布局：false` 在其前端。 Refer to [this section](/docs/front-matter#Layout) for more details.
{% endnote %}

## 文件名

默认情况下，Hexo使用帖子标题作为其文件名。 您可以编辑 `_config.yml` 中的 `新的 post_name` 设置更改默认文件名。 例如， `:year :month-:day:title.md` 将在帖子创建日期前修复文件名。 您可以使用以下占位符：

| 占位符      | 描述                 |
| -------- | ------------------ |
| `:title` | 帖子标题 (小写，空格替换为连字符) |
| `:年`     | 创建年份，例如： `2015`    |
| `:月`     | 创建月 (前导零)，例如： `04` |
| `:i_月`   | 创建月 (无前端零)，例如： `4` |
| `:day`   | 创建日 (前零)，例如： `07`  |
| `:i_day` | 创建日 (无前导零)，例如： `7` |

## 草稿

以前，我们在 Hexo: `草案` 中提到了一个特殊的布局。 以此布局初始化的帖子被保存到 `源/_草稿` 文件夹。 您可以使用 `发布` 命令将草稿移动到 `source/_posts` 文件夹。 `发布` 工作方式类似于 `新的` 命令。

``` bash
$十六进制发布 [layout] <title>
```

草稿不默认显示。 您可以在运行 Hexo 时添加 `--draft` 选项或启用 `render_draft` 设置 `_config.yml` 来渲染草稿。

## 手柄武器库

创建帖子时，Hexo 将会根据 `scaffolds` 文件夹中的相应文件构建文件。 例如：

``` bash
$ 十六进制新照片"My Gallery
```

当你运行此命令时，Hexo会尝试找到 `张照片。 d` `scaffolds` 文件夹并基于它构建帖子。 以下占位符可用于scaffolds：

| 占位符  | 描述     |
| ---- | ------ |
| `布局` | 布局     |
| `标题` | 标题     |
| `日期` | 文件创建日期 |

## 支持的格式

十六进制支持帖子以任何格式写出，只要相应的渲染器插件已经安装。

例如，Hexo 有 `十六进制渲染器标记为` 和 `十六进制渲染器-ejs` 默认情况下安装， 这样您就可以在 `Markdown` 或 `ejs` 中写您的帖子。 If you have `hexo-renderer-pug` installed, then you can even write your post in pug template language.

您可以将您的帖子重命名并更改为文件扩展名从 `.md` 更改为 `js`, 然后Hexo 将使用 `十六进制渲染器-ejs` 来渲染该文件，其他格式就是这样的。
