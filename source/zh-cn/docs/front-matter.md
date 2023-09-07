---
title: 前端
---

{% youtube pfD6FCZdW4Q %}

前事物是用于配置您写入设置的 YAML 或 JSON 的一个块。 当在 YAML 中写入或在 JSON 中写入三个分号时，前事项前缀会被三个分号终止。

**YAML**

``` yaml
---
title: Hello World
date: 2013/7/13 20:46:25
-
```

**JSON**

``` json
"title": "Hello World",
"date": "2013/7/13 20:46:25"
 ;; ;
```

### 设置 & 其默认值

| 设置               | 描述                                                                                                  | 默认设置                                                   |
| ---------------- | --------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `布局`             | 布局                                                                                                  | [`config.default_layout`](/docs/configuration#Writing) |
| `标题`             | 标题                                                                                                  | 文件名(仅帖子)                                               |
| `日期`             | 发布日期                                                                                                | 文件创建日期                                                 |
| `已更新`            | 更新日期                                                                                                | 文件更新日期                                                 |
| `评论`             | 启用帖子的评论功能                                                                                           | true                                                   |
| `标签`             | 标签(不适用于页面)                                                                                          |                                                        |
| `类别`             | 类别(不适用于页面)                                                                                          |                                                        |
| `永久链接`           | 覆盖帖子的默认永久链接。 Permalink should end with `/` or `.html`                                               | `空的`                                                   |
| `摘录`             | 纯文本中的页面节录。 使用 [此插件](/docs/tag-plugins#Post-Excerpt) 格式化文本                                           |                                                        |
| `DisablNunjucks` | Disable rendering of Nunjucks tag `{{ }}`/`{% %}` and [tag plugins](/docs/tag-plugins) when enabled | false                                                  |
| `lang`           | 设置重写 [自动检测](/docs/internationalization#Path)                                                        | 继承自 `_config.yml`                                      |

#### 布局

The default layout is `post`, in accordance to the value of [`default_layout`](/docs/configuration#Writing) setting in `_config.yml`. 当文章中禁用布局时(`布局：false`)，将不会用主题处理。 然而，仍然存在着这种情况。 它仍将由任何可用的渲染器呈现：如果一个文章是在 Markdown 中写的，并且一个Markdown 渲染器(例如默认 [十六进制渲染器标记的](https://github.com/hexojs/hexo-renderer-marked))已安装， 它将被渲染到 HTML。

[标签插件](/docs/tag-plugins) 总是被处理，不管布局如何，除非被 `DisablNunjucks` 设置或 [渲染器](/api/renderer#Disable-Nunjucks-tags) 禁用。

#### Categories & Tags

只有帖子支持使用分类和标签。 类别按顺序适用于员额，导致分类和次级分类等级。 标签都是在相同的等级级别上定义的，所以它们的表面顺序不重要。

**示例**

``` yaml
categories:
- Sports
- Baseball
tags:
- Injury
- Fight
- Shocking
```

如果你想应用多个分类层次结构，请使用一个名称列表而不是一个单个名称。 如果Hexo看到某个帖子上这种定义的任何类别，它将把该帖子的每个类别视为它自己的独立等级。

**示例**

``` yaml
类别：
- [体育，Baseball]
- [MLB, American League, Boston Red Sox]
- [MLB, American League, New York Yanke]
- Rivalries
```
