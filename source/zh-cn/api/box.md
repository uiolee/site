---
title: 框
---

Box 是一个用于处理指定文件夹中文件的容器。 十六进制使用两个不同的盒子： `十六进制源` 和 `十六进制主题`。 前者用于处理 `源` 文件夹，后者用于处理 `主题` 文件夹。

## 加载文件

Box provides two methods for loading files: `process` and `watch`. `处理` 加载文件夹中的所有文件。 `观看` 做同样的事情，但也开始观看文件更改。

``` js
box.process().then(function(){
  // ...
});

box.watch().then(function(){
  // You can call box.unwatch() later to stop watching.
});
```

## 路径匹配

方框提供了许多路径匹配的方法。 您可以使用正则表达式、函数或快速模式字符串。 例如：

``` plain
贴子:id => 贴子/89
贴子/路径=> 贴子/2015/标题
```

欲了解更多信息，请访问 [util.图案][]。

## 处理器

处理器是箱子的一个基本元素，用于处理文件。 您可以使用上面描述的匹配路径来限制处理器应该处理的内容。 注册一个新处理器使用 `addProcessor` 方法。

``` js
box.addProcessor('posts/:id', function(file){
  //
});
```

框将匹配文件的内容传递给处理器。 然后可以从回调中的 `文件` 参数直接读取此信息：

| 属性       | 描述                                 |
| -------- | ---------------------------------- |
| `source` | 文件的完整路径                            |
| `path`   | 文件框的相对路径                           |
| `type`   | 文件类型。 值可以是 `创建`, `更新`, `跳过`, `删除`. |
| `params` | 路径匹配的信息。                           |

框还提供了一些方法，所以您不必自己处理文件 IO 。

| 方法           | 描述       |
| ------------ | -------- |
| `read`       | 读取文件     |
| `readSync`   | 同步读取文件   |
| `stat`       | 读取文件状态   |
| `statSync`   | 同步读取文件状态 |
| `render`     | 渲染文件     |
| `renderSync` | 同步渲染文件   |

[util.图案]: https://github.com/hexojs/hexo-util#patternrule
