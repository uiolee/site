---
title: 配置
---

您可以修改 `_config.yml` 或 [备用配置文件](#Using-an-Alternate-Config) 中的站点设置。

### 站点

| 设置         | 描述                                                                                                                                                                                       |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `标题`       | 您网站的标题                                                                                                                                                                                   |
| `字幕`       | 您网站的字幕                                                                                                                                                                                   |
| `描述`       | 您的网站描述                                                                                                                                                                                   |
| `关键字`      | 您网站的关键字。 支持多个值。                                                                                                                                                                          |
| `作者`       | 您的姓名                                                                                                                                                                                     |
| `语言`       | 您网站的语言。 使用 [2-字母 ISO-639-1 代码](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 或可选的 [其变体](/docs/internationalization)。 默认是 `的`                                                    |
| `timezone` | 您网站的时区。 Hexo 默认使用您计算机上的设置。 You can find the list of available timezones [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). 一些例子是： `America/New_York`、 `Japan`和 `UTC`。 |

### 网址

| 设置                          | 描述                                                                  | 默认设置                        |
| --------------------------- | ------------------------------------------------------------------- | --------------------------- |
| `网址`                        | 您网站的 URL，必须以 `http://` 或 `https:////` 开头。                           |                             |
| `根目录`                       | 您的网站的根目录                                                            | `url's pathname`            |
| `永久链接`                      | The [permalink](permalinks.html) format of articles                 | `:year/:month/:day/:title/` |
| `permalink默认值`              | 每个段在永久链接中的默认值                                                       |                             |
| `偏好url`                     | Rewrite the [`permalink`](permalinks.html) variables to pretty URLs |                             |
| `petty_urls.trailing_index` | Trailing `index.html`, set to `false` to remove it                  | `true`                      |
| `petty_urls.trailing_html`  | Trailing `.html`, 设置为 `false` 以删除它(_不适用于尾迹 `index.html`_)           | `true`                      |

{% note info Website in subdirectory %}
如果您的网站位于子目录(如 `http://example.org/blog`)设置 `` 到 `http://example。 rg/blog` 并设置 `root` 到 `/blog/`.
{% endnote %}

示例：

``` yaml
# 例如：page.permalink 是 http://example.com/foo/bar/index.html
petty_urls:
  Trailing_index: false
# reason http://example.com/food/bar/
```

### 目录

| 设置           | 描述                                                                                                        | 默认设置    |
| ------------ | --------------------------------------------------------------------------------------------------------- | ------- |
| `源码目录`       | 源文件夹。 存储您的内容的位置                                                                                           | `来源`    |
| `public_dir` | 公共文件夹。 将生成静态站点的位置                                                                                         | `公开的`   |
| `tag_dir`    | 标签目录                                                                                                      | `标签`    |
| `存档目录`       | 存档目录                                                                                                      | `档案`    |
| `类别目录`       | 类别目录                                                                                                      | `类别`    |
| `code_dir`   | 包含代码目录( `source_dir` 的子目录)                                                                                | `下载/代码` |
| `i18n_dir`   | i18n 目录                                                                                                   | `:lang` |
| `跳过渲染`       | 将复制到 `公开的` 无需渲染的路径。 您可以使用 [glob 表达式](https://github.com/micromatch/micromatch#extended-globbing) 来进行路径匹配。 |         |

示例：

``` yaml
skip_render: "mypage/**/*"
# 将输出`source/mypage/index.html` 和 `source/mypage/code.js` 而不改变它们。

## 这也可以用来排除帖子，
skip_render: "_posts/test-post.md"
# 将忽略 `source/_posts/test-post.md`。
```

### 写入中

| 设置               | 描述                                                                   | 默认设置        |
| ---------------- | -------------------------------------------------------------------- | ----------- |
| `新帖子名称`          | 新帖子的文件名格式                                                            | `:title.md` |
| `默认布局`           | 默认布局                                                                 | `发帖`        |
| `titlecase`      | 将标题转换为标题案例？                                                          | `false`     |
| `外部链接`           | 在新标签中打开外部链接？                                                         |             |
| `外部链接已启用`        | 在新标签中打开外部链接？                                                         | `true`      |
| `外部链接字段`         | 仅应用于整个 `网站` 或 `帖子`                                                   | `站点`        |
| `外部 link.ext`    | 排除主机名。 在适用时指定子域名，包括 `www`                                            | `[]`        |
| `filename_case`  | 将文件名转换为 `1` 小案； `2` 大案                                               | `0`         |
| `渲染草稿`           | 显示草稿？                                                                | `false`     |
| `post_asset_文件夹` | 启用 [Asset 文件夹](asset-folders.html)?                                  | `false`     |
| `相对链接`           | 创建相对于根文件夹的链接？                                                        | `false`     |
| `未来`             | 显示未来的帖子？                                                             | `true`      |
| `高亮显示`           | 代码块语法高亮设置，请参阅关于使用指南的 [高亮。js](/docs/syntax-highlight#Highlight-js) 部分 |             |
| `prismjs`        | 代码块语法高亮设置，请参阅 [PrismJS](/docs/syntax-highlight#PrismJS) 部分使用指南       |             |

### 主页设置

| 设置                               | 描述                                                                                                              | 默认设置  |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------- | ----- |
| `index_生成器`                      | Generate an archive of posts, powered by [hexo-generator-index](https://github.com/hexojs/hexo-generator-index) |       |
| `index_generator.path`           | 博客索引页面的根路径                                                                                                      | `''`  |
| `index_generator.per_page`       | 每页显示帖子。                                                                                                         | `10`  |
| `index_生成器.order_by`             | 发布订单。 默认情况下按日期降序(从新到旧)。                                                                                         | `-日期` |
| `index_generator.pagination_dir` | URL 格式，请参阅下面的 [分页](#Pagination) 设置                                                                              | `页面`  |

### 分类 & 标签

| 设置     | 描述       | 默认设置  |
| ------ | -------- | ----- |
| `默认类别` | 默认类别     | `未分类` |
| `类别地图` | 重写类别sugs |       |
| `标签地图` | 覆盖标签斜体   |       |

示例：

``` yaml
category_map:
  "昨天的想法": 昨天的想法
  "C++": c-plus-plus
```

### 日期/时间格式

Hexo 使用 [Moment.js](http://momentjs.com/) 来处理日期。

| 设置     | 描述                                                    | 默认设置         |
| ------ | ----------------------------------------------------- | ------------ |
| `日期格式` | 日期格式                                                  | `YYYY-MM-DD` |
| `时间格式` | 时间格式                                                  | `HH:mm:ss`   |
| `更新选项` | [`更新了`](/docs/variables#Page-Variables) 当前事项未提供时要使用的值 | `时长`         |

{% note info updated_option %}
`updated_option` 控制了 `已更新的` 值当未在前面事项中提供时：

- `mtime`: Use file modification date as `updated`. 这是从 3.0.0 开始的 Hexo 的默认行为
- `日期`: 使用 `日期` 为 `更新`. 当文件修改日期可能不同时，通常使用 Git 工作流。
- `空的`: 在未提供时只需丢弃 `已更新` 可能与大多数主题和插件不兼容。

`use_date_for_updated` 已废弃，并将在下一个主要版本中删除。 请使用 `updated_option: 'date'` 代替。
{% endnote %}

### 分页

| 设置         | 描述                   | 默认设置 |
| ---------- | -------------------- | ---- |
| `per_page` | 每个页面显示的帖子数。 `0` 禁用分页 | `10` |
| `分页`       | URL 格式               | `页面` |

示例：

``` yaml
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/esome-page/2
```

### 扩展

| 设置               | 描述                                                                                                               |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- |
| `主题`             | 主题名称。 `false` 禁用主题                                                                                               |
| `主题配置`           | 主题配置。 在此密钥下包含任何自定义主题设置以覆盖默认主题。                                                                                   |
| `部署`             | 部署设置                                                                                                             |
| `meta_generator` | [Meta generator](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes) tag. `false` 禁用注入标签。 |

### 包含/排除文件或文件夹

使用以下选项来明确处理或忽略某些文件/文件夹。 支持 [手套表达式](https://github.com/micromatch/micromatch#extended-globbing) 路径匹配。

`包含` 和 `排除` 选项仅适用于 `源/` 文件夹，而 `忽略` 选项适用于所有文件夹。

| 设置    | 描述                             |
| ----- | ------------------------------ |
| `包含`  | 包括隐藏的文件(包括以下划线开头的文件/文件夹，例外情况*) |
| `不包含` | 排除文件/文件夹                       |
| `忽略`  | 忽略文件/文件夹                       |

示例：

```yaml
# 包含/排除文件/文件夹
包括：
  - ".nojekyll"
  # 包含 'source/css/_typing.css'。
  - "css/_typing.css"
  # 包含 'source/_css/' 中的任何文件。
  - "_css/*"
  # 包含 'source/_css/' 中的任何文件和子文件夹。
  - "_css/**/*"

排除：
  # 排除“source/js/test.js”。
  - "js/test.js"
  # 排除“source/js/”中的任何文件。
  - "js/*"
  # 排除“source/js/”中的任何文件和子文件夹。
  - "js/**/*"
  # 排除以'source/js/'开头的“test”文件名的任何文件。
  - "js/test*"
  # 排除以'test' 开头的“source/js/”及其子文件夹的任何文件名。
  - "js/**/test*"
  # 不要用它来排除'source/_posts/'中的帖子。
  # 为此使用 skip_render。 或者在文件名前添加下划线。
  # - "_posts/hello-world.md" # 不起作用。

ignore:
  # Ignore any folder named 'foo'.
  - "**/foo"
  # 只忽略'themes/' 中的“foo” 文件夹。
  - "**/themes/*/foo"
  # 与上面相同，但适用于“主题”的每个子文件夹。
  - "**/themes/**/foo"
```

列表中的每个值必须包含单个/双引号。

`包括：` 和 `排除：` 不适用于 `主题/` 文件夹。 要么使用 `忽略：` ，要么在文件/文件夹名称前添加下划线以便排除。

\* 值得注意的异常是 `源/_posts` 文件夹。 但以下划线开头的任何文件或文件夹仍将被忽略。 使用 `包括：不推荐该文件夹中的` 规则。

### 使用替代配置

A custom config file path can be specified by adding the `--config` flag to your `hexo` commands with a path to an alternate YAML or JSON config file, or a comma-separated list (no spaces) of multiple YAML or JSON files.

``` bash
# 使用 'custom.yml' 代替'_config.yml'
$ hexo server --config custom.yml

# 使用 'custom.yml' ml' & 'custom2.json' 优先级为“custom2.json”
$ hexo server --config custom.yml,custom2.json
```

使用多个文件将所有配置文件合并，并将合并的设置保存到 `_multiconfig.yml`。 后一种数值居优先。 它与任意深空物体的 JSON 和 YAML 文件的任何数量协同工作。 Note that **no spaces are allowed in the list**.

例如，在上面的例子中，如果 `foo：bar` 在 `习惯中。 ml`, but `"foo": "dinosaur"` is in `custom2. son`, `_multiconfig.yml` 将包含 `foo: dinosaur`

### 备用主题配置

Hexo 主题是独立的项目，具有独立的 `_config.yml` 文件。

您可以在其他地方配置一个主题，而不是使用您的设置创建一个自定义版本：

**从站点主配置文件中的 `theme_config`**

> 自十六进制以来支持 2.8.2

```yml
# _config.yml
主题 "my-theme"
theme_config:
  bio: "我很棒的生物"
  foo:
    bar: 'a'
```

```yml
# themes/my-theme/_config.yml
bio: "Some general bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

主题配置结果：

```json
{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

**from a dedicated `_config.[theme].yml` file**

> 自Hexo 5.0.0 以来支持

该文件应该放在您的网站文件夹中，支持 `yml` 和 `json`。 `主题` 在 `_config.yml` 中必须配置Hexo 才能读取 `_config。[theme].yml`

```yml
# _config.yml
主题：“我的主题”
```

```yml
# _config.my-theme.yml
生物: "我很棒的生物"
foo:
  bar: 'a'
```

```yml
# themes/my-theme/_config.yml
bio: "Some general bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

主题配置结果：

```json
{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

{% note %}
我们强烈建议您将主题配置存储在一个地方。 但如果您需要分开存储主题配置。 您需要知道这些配置的优先级：网站主配置文件内的 `theme_config` 在合并过程中具有最高优先级， 然后专用主题配置文件。 主题目录下的 `_config.yml` 文件具有最低优先级。
{% endnote %}
