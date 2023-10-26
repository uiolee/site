---
title: 注入器（Injector）
---

注入器被用于将静态代码片段注入生成的 HTML 的 `<head>` 和/或 `<body>` 中。 Hexo 将在 `after_render:html` 过滤器 **之前** 完成注入。

## 概要

```js
hexo.extend.injector.register(条目，值至)
```

### 条目 `<string>`

代码注入在 HTML中的位置。

支持这些值：

- `head_begin`: 注入在 `<head>` 之后（默认）
- `head_end`: 注入在 `</head>` 之前
- `body_begin`: 注入在 `<body>` 之后
- `body_end`: 注入在 `</body>` 之前

### 值 `<string> | <Function>`

> 除了字符串，也支持返回值为字符串的函数

需要注入的代码片段。

### 到 `<string>`

哪个页面会代码片段被注入.

- `default`: 注入到每个页面（默认值）
- `home`: 只注入到主页（`is_home()` 为 `true` 的页面）
- `post`: 只注入到文章页面（`is_post()` 为 `true` 的页面）
- `page`: 只注入到独立页面（`is_page()` 为 `true` 的页面）
- `archive`: 只注入到归档页面（`is_archive()` 为 `true` 的页面）
- `category`: 只注入到分类页面（`is_category()` 为 `true` 的页面）
- `tag`: 只注入到标签页面（`is_tag()` 为 `true` 的页面）
- 或是其他自定义 layout 名称，自定义 layout 参见 [写作 - 布局（Layout）](/zh-cn/docs/writing#布局（Layout）)

----

注入器还有一些内部函数，如果你要使用它们，请参考 [hexojs/hexo#4049](https://github.com/hexojs/hexo/pull/4049)。

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

上述代码将会把 `APlayer.min.css`（`<link>` 标签）和 `APlayer.min.js` （`<script>` 标签）注入到所有 layout 为 `music` 的页面的 `</head>` 和 `</body>` 之前，以及将 `jquery.js`（`<script>` 标签）注入到每一个生成的页面的 `</body>` 之前。 另外， `jquery.js` (`<script>` 标签)将被注入到 `</body>` 每个生成的页面中。

## 访问用户配置

使用以下任何一个选项：

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
