---
title: 渲染器
---

渲染器用于渲染内容。

## 简述

``` js
hexo.extend.renderer.register(name, output, function(data, options){
  // ...
}，同步；
```

| 参数   | 描述                      |
| ---- | ----------------------- |
| `名称` | 输入文件名扩展名 (小写，不带前端的 `。`) |
| `输出` | 输出文件名扩展名 (小写，不带前端的 `。`) |
| `同步` | 同步模式                    |

三个参数将传递到渲染函数中：

| 参数         | 描述                                     |
| ---------- | -------------------------------------- |
| `数据`       | 包含两个属性：文件路径 `` 和文件内容 `文本`。 `路径` 不一定存在。 |
| `选项`       | 备选方案                                   |
| `callback` | 两个参数 `err`, `值` 的回调函数。                 |

## 示例

### 异步模式

``` js
var stylus = require('stylus');

// Callback
hexo.extend.renderer.register('styl', 'css', function(data, options, callback){
  stylus(data.text).set('filename', data.path).render(callback);
});

// Promise
hexo.extend.renderer.register('styl', 'css', function(data, options){
  return new Promise(function(resolve, reject){
    resolve('test');
  });
});
```

### 同步模式

``` js
var ejs = require('ejs');

hexo.extend.render.register('ejs', 'html', functions, functions, options)_
  options.filename = data.path;
  return ejs.render(data.text, options);
}, true);
```

### 禁用 Nunjucks 标签

Nunjucks 标签 `{{ }}` 或 `{% %}` (被 [标签插件](/docs/tag-plugins)使用) 默认处理以禁用：

``` js
function lessFn(data, options) PDF
  // do some


lessFn.disableNunjucks = true

hexo.extend.render.register('less', 'css', lessFn);
```
