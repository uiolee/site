---
title: 渲染
---

There are two methods for rendering files or strings in Hexo: the asynchronous `hexo.render.render` method and the synchronous `hexo.render.renderSync` method. 不足为奇的是，这两种方法非常相似，因此只有异步的 `hexo.render.render` 将在以下段落中进一步讨论。

## 渲染字符串

在渲染字符串时，您必须指定一个 `引擎` 才能让Hexo 知道它应该使用哪个渲染引擎。

``` js
hexo.render.render({text: 'example', engine: 'swig'}).then(functional) power
//
});
```

## 渲染文件

当渲染文件时， 不需要指定一个 `引擎` 因为Hexo 会自动检测到相关的渲染引擎。 当然，您也可以明确定义 `引擎`。

``` js
hexo.render.render({path: 'path/to/file.swig'}).then(函数(result)}.
  // ...
});
```

## 渲染选项

您可以作为第二个参数传递选项对象。

``` js
hexo.render.render({text: ''}, {foo: 'foo'}).then(function(result){
  // ...
});
```

## 后渲染过滤器

渲染完成后，十六进制将执行相应的 `后渲染` 过滤器。 例如，我们可以使用此功能来实现 JavaScript 迷你。

``` js
var UglifyJS = required ('uglify-js');

hexo.extend.filter.register('after_render:js', function(str,data))_
  var results = UglifyJS.minify(str);
  return result.code;
});
```

## 检查文件是否可渲染。

You can use the `isRenderable` or `isRenderableSync` method to check whether a file path is renderable. 只有当对应的渲染器已注册，这个方法才会返回 true。

``` js
hexo.renderable('layout.swig') // true
hexo.render.isRenderable('image.png') // falsel
```

## 获取输出扩展

使用 `getoutput` 方法来获取渲染输出的扩展。 如果一个文件不可渲染，方法将返回一个空字符串。

``` js
hexo.render.getOutput('layout.swig') // html
hexo.render.getOutput('image.png') // '''
```

## 禁用 Nunjucks 标签

如果您不使用 [标签插件](/docs/tag-plugins) 并且想要在您的帖子中使用 `{{ }}` 或 `{% %}` 而不使用内容 [逃避](/docs/troubleshooting#Escape-Contents), 您可以在现有渲染器中禁用处理Nunjucks标签：

``` js
// 以下示例仅适用于“.md”文件扩展名
// 你可能需要覆盖其他扩展，e。 。'.markdown', '.mkd', etc
const renderer = hexo. ender.renderer.get('md')
if (Renderer) v.
  render.disableNunjucks = true
  hexo.extend.renderer.register('md', 'html', renderer)
}
```
