---
title: 前端
---

{% youtube Rl48Yk4A_V8 %}

前事物是用于配置您写入设置的 YAML 或 JSON 的一个块。 当在 YAML 中写入或在 JSON 中写入三个分号时，前事项前缀会被三个分号终止。

**YAML**

``` yaml
---
title: Hello World
date: 2013/7/13 20:46:25
-
```

**JSON Front-matter**

``` json
"title": "Hello World",
"date": "2013/7/13 20:46:25"
 ;; ;
```

### 设置 & 其默认值

| 设置               | 描述                                                                        | 默认值                                                    |
| ---------------- | ------------------------------------------------------------------------- | ------------------------------------------------------ |
| `布局`             | 布局                                                                        | [`config.default_layout`](/docs/configuration#Writing) |
| `标题`             | 标题                                                                        | 文章的文件名                                                 |
| `日期`             | 建立日期                                                                      | 文件建立日期                                                 |
| `已更新`            | 更新日期                                                                      | 文件更新日期                                                 |
| `评论`             | 开启文章的评论功能                                                                 | `true`                                                 |
| `标签`             | 标签（不适用于分页）                                                                |                                                        |
| `类别`             | 分类（不适用于分页）                                                                |                                                        |
| `永久链接`           | 覆盖帖子的默认永久链接。 覆盖文章的永久链接，永久链接应该以 `/` 或 `.html` 结尾                           | `空的`                                                   |
| `摘录`             | 纯文本的页面摘要。 使用 [该插件](/zh-cn/docs/tag-plugins#文章摘要和截断) 来格式化文本                |                                                        |
| `DisablNunjucks` | 启用时禁用 Nunjucks 标签 `{{ }}`/`{% %}` 和 [标签插件](/zh-cn/docs/tag-plugins) 的渲染功能 | false                                                  |
| `lang`           | 设置语言以覆盖 [自动检测](/zh-cn/docs/internationalization#路径)                       | 继承自 `_config.yml`                                      |
| `已发布`            | 文章是否发布                                                                    | 对于 `_posts` 下的文章为 `true`，对于 `_draft` 下的文章为 `false`     |

#### 布局

根据 `_config.yml` 中 [`default_layout`](/zh-cn/docs/configuration#文章) 的设置，默认布局是 `post` 。 当文章中的布局被禁用(`layout: false`)，它将不会使用主题处理。 然而，它仍然会被任何可用的渲染引擎渲染：如果一篇文章是用 Markdown 写的，并且安装了 Markdown 渲染引擎（比如默认的 [hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked))，它将被渲染成HTML。

除非通过 `disableNunjucks` 设置或 [渲染引擎](/zh-cn/api/renderer#禁用-Nunjucks-标签) 禁用，否则无论布局如何，[标签插件](/zh-cn/docs/tag-plugins) 总是被处理。

#### 分类和标签

只有帖子支持使用分类和标签。 类别按顺序适用于员额，导致分类和次级分类等级。 标签都是在相同的等级级别上定义的，所以它们的表面顺序不重要。

**示例**

``` yaml
categories:
- Diary
tags:
- PS3
- Games
```

如果你想应用多个分类层次结构，请使用一个名称列表而不是一个单个名称。 如果Hexo看到某个帖子上这种定义的任何类别，它将把该帖子的每个类别视为它自己的独立等级。

**示例**

``` yaml
categories:
- [Diary, PlayStation]
- [Diary, Games]
- [Life]
```
