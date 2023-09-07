---
title: 事件
---

Hexo 继承了 [EventEmitter][]，您可以用 `on` 方法监听 Hexo 所发布的事件，也可以使用 `emit` 方法对 Hexo 发布事件，更详细的说明请参阅 Node.js 的 API。 Use the `on` method to listen for events emitted by Hexo, and use the `emit` method to emit events. For more information, refer to the Node.js API documentation. 欲了解更多信息，请参阅Node.js API 文档。

### 部署前

在部署开始之前发出信号。

### 部署后

部署结束后发出。

### 退出

在 Hexo 结束前发布。

### 生成前

在代际开始之前发出信号。

### 生成

生成完成后发出。

### 新的

在文章文件建立后发布。 该事件返回文章参数。

``` js
hexo.on('new', function(post){
  // 
});
```

| 资料     | 描述        |
| ------ | --------- |
| `发布路径` | 文章文件的完整路径 |
| `内容`   | 文章文件的内容   |

### 处理前

在处理原始文件前发布。 此事件会返回一个地址，代表 Box（Box）的根目录。

### processAfter

在原始文件处理后发布。 此事件会返回一个地址，代表 Box（Box）的根目录。

### 已就绪

在初始化完成后发布。

[EventEmitter]: https://nodejs.org/dist/latest/docs/api/events.html
