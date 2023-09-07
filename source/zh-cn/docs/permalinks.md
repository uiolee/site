---
title: 永久链接
---

您可以在 `_config.yml` 或在每个帖子的前缀中为您的网站指定永久链接。

### 变量

除以下变量外，您还可以使用永久链接中的任何属性。

| 变量            | 描述                                                                    |
| ------------- | --------------------------------------------------------------------- |
| `:年`          | 发布时间 (4位数)                                                            |
| `:月`          | 发布月(2位数)                                                              |
| `:i_月`        | 发布月的帖子 (不带前零)                                                         |
| `:day`        | 发布日期 (2位数)                                                            |
| `:i_day`      | 发布日期 (不带前零)                                                           |
| `:小时`         | 发布时间(2位数)                                                             |
| `:分钟`         | 发布时间(2位数)                                                             |
| `:秒`          | 发布第二个帖子(2位数)                                                          |
| `:title`      | 文件名(相对于"source/_posts/"文件夹)                                           |
| `:name`       | 文件名                                                                   |
| `:pos_title`  | 帖子标题                                                                  |
| `:id`         | Post ID (_not persistent across [cache reset](/docs/commands#clean)_) |
| `:categories` | 分类 如果帖子未分类，它将使用 `默认类别` 值。                                             |
| `:hash`       | SHA1 文件名哈希值(与 `:title`)和日期 (12-十六进制)                                  |

您可以通过 `permalink_default` 设置来定义永久链接中每个变量的默认值：

``` yaml
permalink_defauls:
  lang: en
```

### 示例：

``` yaml source/_posts/hello-world.md
title: Hello World
date: 2013-07-14 17:01:34
类别:
- foo
- bar
```

| 设置                            | 结果                          |
| ----------------------------- | --------------------------- |
| `:year/:month/:day/:title/`   | 2013/07/14/hello-world/     |
| `:year:month-:day:title.html` | 2013-07-14-hello-world.html |
| `:category/:title/`           | foo/bar/hello-world/        |
| `:title-:hash/`               | hello-world-a2c8ac003b43/   |

``` yaml source/_posts/lorem/hello-world.md
title: Hello World
date: 2013-07-14 17:01:34
类别:
- foo
- bar
```

| 设置                          | 结果                            |
| --------------------------- | ----------------------------- |
| `:year/:month/:day/:title/` | 2013/07/14/lorem/hello-world/ |
| `:year/:month/:day/:name/`  | 2013/07/14/hello-world/       |

### 多语言支持

To create a multi-language site, you can modify the `new_post_name` and `permalink` settings like this:

``` yaml
new_post_name: :lang/:title.md
permalink: :lang/:title/
```

当您创建一个新帖子时，帖子将被保存到：

``` bash
$ hexo new "Hello World" --lang tw
# => source/_posts/tw/Hello-World.md
```

和 URL 将是：

``` plain
http://localhost:4000/tw/hello-world/
```
