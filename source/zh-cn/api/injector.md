---
title: 喷射器
---

注入器用于将静态代码片段添加到 `<head>` 或和 `<body>` 生成的 HTML 文件。 Hexo 运行注射器 **之前的** `之后执行了render:html` 过滤器。

## 简述

```js
hexo.extend.injector.register(条目，值至)
```

### 条目 `<string>`

代码注入在 HTML中的位置。

支持这些值：

- `head_begt`: 紧接着 `<head>` (默认)。
- `head_end`: 在 `</head>` 之前注入代码片段
- `body_start`: `<body>` 之后注入代码片段
- `body_end`: 在 `</body>` 之前注入代码片段

### 值 `<string> | <Function>`

> 支持返回字符串的函数。

要注入的代码片段

### 到 `<string>`

哪个页面会代码片段被注入.

- `默认`: 注入每个页面 (默认)
- `首页`：仅注入首页 (包含 `is_home()` 助手为 `true`)
- `post`: Only inject to post pages (which has `is_post()` helper being `true`)
- `第`页：仅注入页面 (有 `is_page)` helper 是 `true`)
- `archive`: 只注入归档页面 (其中有 `is_archive)` haper 是 `true`)
- `category`: Only inject to category pages (which has `is_category()` helper being `true`)
- `标签`: 只注入标签页 (包含 `is_tag()` 助手为 `true`)
- Custom layout name could be used as well, see [Writing - Layout](/docs/writing#Layout).

----

There are other internal functions, see [hexojs/hexo#4049](https://github.com/hexojs/hexo/pull/4049) for more details.

## 示例

```js
const css = hexo.extend.helper.get('css').bind(hexo);
const js = hexo.extend.helper.get('js').bind(hexo);

hexo.extend.injector.register('head_end', () => {
  return css('https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css');
}, 'music');

hexo.extend.injector.register('body_end', '<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js">', 'music');

hexo.extend.injector.register('body_end', () => {
  return js('/js/jquery.js');
});
```

在设置上方会弹出 `APlayer.min。 ss` (`<link>` 标签) 到 `</head>` 任何页面布局为 `音乐`和 `应用层。 in.js` (`<script>` tag) to the `</body>` 另外， `jquery.js` (`<script>` 标签)将被注入到 `</body>` 每个生成的页面中。

## 访问用户配置

使用以下任一选项：

1.

``` js
const css = hexo.extend.helper.get('css').bind(hexo);

hexo.extend.injector.register('head_end', () => {
  const { cssPath } = hexo.config.fooPlugin;
  return css(cssPath);
});
```

2.

``` js index.js
/* 全局十六进制*/

hexo.extend.injector.register('head_end', require('./lib/inject').bindhexo.extend (hexo))
```

``` js lib/inject.js
module.exports = function () {
  const css = this.extend.helper.get('css');
  const { cssPath } = this.config.fooPlugin;
  return css(cssPath);
}
```

``` js lib/inject.js
function injectFn() {
  const css = this.extend.helper.get('css');
  const { cssPath } = this.config.fooPlugin;
  return css(cssPath);
}

module.exports = injectFn;
```

3.

``` js index.js
/* 全局十六进制*/

hexo.extend.injector.register('head_end', require('./lib/inject')(hexo))
```

``` js lib/inject.js
module.exports = (hexo) => () => {
  const css = hexo.extend.helper.get('css').bind(hexo);
  const { cssPath } = hexo.config.fooPlugin;
  return css(cssPath);
};
```

``` js lib/inject.js
const injectFn = (hexo) => {
  const css = hexo.extend.helper.get('css').bind(hexo);
  const { cssPath } = hexo.config.fooPlugin;
  return css(cssPath);
};

module.exports = (hexo) => injectFn(hexo);
```
