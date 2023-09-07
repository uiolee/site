---
title: 框
---

Box is a container used for processing files in a specified folder. 「Box」是 Hexo 用来处理特定文件夹中的文件的容器，在 Hexo 中有两个 Box，分别是 `hexo.source` 和 `hexo.theme`，前者用于处理 `source` 文件夹，而后者用于处理主题文件夹。 「Box」是 Hexo 用来处理特定文件夹中的文件的容器，在 Hexo 中有两个 Box，分别是 `hexo.source` 和 `hexo.theme`，前者用于处理 `source` 文件夹，而后者用于处理主题文件夹。 前者用于处理 `源` 文件夹，后者用于处理 `主题` 文件夹。

## 载入文件

Box 提供了两种方法来载入文件：`process`, `watch`，前者用于载入文件夹内的所有文件；而后者除了执行 `process` 以外，还会继续监视文件变动。 `处理` 加载文件夹中的所有文件。 `process` loads all files in the folder. `watch` does the same, but also starts watching for file changes.

``` js
box.process().then(function(){
  // ...
box.process().then(function(){
  // ...
box.process().then(function(){
  // ...
});

box.watch().then(function(){
  // 之后可调用 box.unwatch()，停止监视文件
});
});
});
```

## 比对路径

方框提供了许多路径匹配的方法。 Box provides many ways for path matching. You can use a regular expression, a function or an Express-style pattern string. For example: 例如：

``` plain
贴子:id => 贴子/89
贴子/路径=> 贴子/2015/标题
```

您可以以参考 [util.Pattern][] 以获得更多信息。

## 处理器（Processor）

处理器（Processor）是 Box 中非常重要的元素，它用于处理文件，您可以使用上述的路径对比来限制该处理器所要处理的文件类型。 You can use path matching as described above to restrict what exactly the processor should process. 使用 `addProcessor` 来添加处理器。 使用 `addProcessor` 来添加处理器。

``` js
box.addProcessor('posts/:id', function(file){
  //
});
```

框将匹配文件的内容传递给处理器。 Box passes the content of matched files to processors. This information can then be read straight from the `file` argument in the callback:

| 属性       | 描述                                            |
| -------- | --------------------------------------------- |
| `来源`     | 文件完整路径                                        |
| `路径`     | 文件相对于 Box 的路径                                 |
| `类型`     | 文件类型。 有 `create`, `update`, `skip`, `delete`。 |
| `params` | 从路径对比中取得的信息                                   |

Box 还提供了一些方法，让您无须手动处理文件 I/O。

| 方法     | 描述       |
| ------ | -------- |
| `已读`   | 读取文件     |
| `读取同步` | 同步读取文件   |
| `统计`   | 读取文件状态   |
| `状态`   | 同步读取文件状态 |
| `渲染`   | 渲染文件     |
| `渲染同步` | 同步渲染文件   |

[util.Pattern]: https://github.com/hexojs/hexo-util#patternrule
