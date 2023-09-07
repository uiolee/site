---
title: 国际化(i18n)
---

您可以使用国际化来以不同的语言展示您的网站。 设置默认语言的方式是修改 `_config.yml` 中的 `语言` 设置。 您也可以设置多种语言并修改默认语言的顺序。

``` yaml
语言： zh-tw

语言：
- zh-tw
- en
```

### 语言文件

语言文件可以是 YAML 或 JSON 文件。 您应该将它们放入主题中的 `语言` 文件夹。 语言文件中支持 [打印f 格式](https://github.com/alexei/sprintf.js)。

### 模板

Use `__` or `_p` helpers in templates to get the translated strings. 前者用于正常用途，后者用于复数字符串。 例如：

``` yaml en.yml
index:
  title: Home
  add: Add
  video:
    zero: No videos
    one: One video
    other: %d videos
```

``` js
<%= __('index.title') %>
// Home

<%= _p('index.video', 3) %>
// 3 视频
```

### 路径

您可以在前面设置页面的语言，或者在 `_config中修改 <code>i18n_dir` 设置。 ml</code> 启用十六进制自动检测。

``` yaml
i18n_dir: :lang
```

`i18n_dir` 默认值为 `:lang`, 这意味着十六进制将检测到网址第一部分中的语言。 例如：

``` plain
/index.html => en
/archives/index.html => en
/zh-tw/index.html => zh-tw
```

只有当语言文件存在时，字符串才会被用作语言。 所以 `归档` 在 `/archives/index.html` (例2) 不会被用作语言。
