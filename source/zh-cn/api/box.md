---
title: 盒（box）
---

盒（box）是一个用于处理指定文件夹中文件的容器。 在 Hexo 中有两个盒（box），分别是 `hexo.source` 和 `hexo.theme`。 前者用于处理 `source` 文件夹，而后者用于处理 `theme` 主题文件夹。

## 载入文件

盒（box）提供了两种方法来载入文件：`process`, `watch`。 `process` 用于载入文件夹内的所有文件。 `watch` 除了执行 `process` 以外，还会继续监视文件变动。

``` js
box.process().then(function(){
  // ...
});

box.watch().then(function(){
  // You can call box.unwatch() later to stop watching.
});
```

## 比对路径

盒（box）提供了许多路径匹配的方法。 您可以使用正则表达式、函数或 Express 风格模式字符串。 例如：

``` plain
posts/:id => posts/89
posts/*path => posts/2015/title
```

您可以以参考 [util.Pattern][] 以获得更多信息。

## 处理器（Processor）

处理器（Processor）是盒（box）中非常重要的元素，它用于处理文件。 您可以使用上面描述的匹配路径来限制处理器应该处理的内容。 使用 `addProcessor` 来添加处理器（processor）。

``` js
box.addProcessor('posts/:id', function(file){
  //
});
```

盒（box）将匹配文件的内容传递给处理器（processor）。 然后可以从回调中的 `file` 参数直接读取此信息：

| 属性       | 描述                                            |
| -------- | --------------------------------------------- |
| `source` | 文件完整路径                                        |
| `path`   | 文件相对于盒（box）的路径                                |
| `type`   | 文件类型。 有 `create`, `update`, `skip`, `delete`。 |
| `params` | 从路径对比中取得的信息                                   |

盒（box）还提供了一些方法，让您无须手动处理文件 I/O。

| 方法           | 描述       |
| ------------ | -------- |
| `read`       | 读取文件     |
| `readSync`   | 同步读取文件   |
| `stat`       | 读取文件状态   |
| `statSync`   | 同步读取文件状态 |
| `render`     | 渲染文件     |
| `renderSync` | 同步渲染文件   |

[util.Pattern]: https://github.com/hexojs/hexo-util#patternrule
