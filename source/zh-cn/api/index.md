---
title: API
---

此文档提供了更多关于API的详细信息，对于想要修改Hexo源代码或编写新插件的人将特别有用。 If you are interested in more basic usage of Hexo, please refer to the [docs](../docs) instead.

请注意，此文档仅适用于 Hexo 3及以上。

## 初始化

首先，我们必须创建一个十六进制实例。 一个新实例需要两个参数：网站根目录， `base_dir`和一个包含初始化选项的对象。 接下来，我们通过调用 `init` 方法初始化这个实例，这将导致Hexo 加载它的配置和插件。

``` js
var Hexo = require('hexo');
var hexo = new Hexo(process.cwd(), {});

hexo.init().then(function(){
  // ...
});
```

| 选项          | 描述                                                                                         | 默认设置               |
| ----------- | ------------------------------------------------------------------------------------------ | ------------------ |
| `debug`     | 启用调试模式。 Display debug messages in the terminal and save `debug.log` in the root directory. | `false`            |
| `安全`        | 启用安全模式。 不加载任何插件。                                                                           | `false`            |
| `静音`        | 启用静音模式。 不在终端中显示任何消息。                                                                       | `false`            |
| `配置`        | 指定配置文件的路径。                                                                                 | `yml`              |
| `草稿` / `草稿` | 启用以将草稿添加到帖子列表。<br> 示例：当您使用 `hexo.locals.get('posts')`                                | `渲染草稿` _config.yml |

## 加载文件

Hexo 提供了两种加载文件的方法： `负载` 和 `观察`。 `加载` 用于加载 `源` 中的所有文件以及主题数据。 `观看` 做了同样的事情。 `加载` 做了同样的事情，但也将开始持续监视文件的更改。

这两种方法都会加载文件列表并传递给相应的处理器。 在所有文件处理完毕后，他们将呼叫发电机来创建路线。

``` js
hexo.load().then(function(){
  // ...
(ii)

hexo.watch().then(function()}); 

 hexo.watch().then(函数().
  // 你可以稍后调用 hexo.unwatch() 以停止监视。
});
```

## 执行命令

任何控制台命令都可以在 Hexo 实例上明确使用 `调用` 方法。 这种调用需要两个论点：控制台命令的名称和选项参数。 不同的控制台命令有不同的选项。

``` js
hexo.call('generate', {}).then(function()@un.org.
/...
});
```

``` js
hexo.call('list', { _: ['post'] }).then(function() {
  // ...
})
```

## 退出

当控制台命令完成成功或失败时，您应该调用 `退出` 方法。 这使Hexo能够体面地退出并完成保存数据库等重要工作。

``` js
hexo.call('generate').then(function()own
  return hexo.exit();
}).catch(function(err)paper.
  return hexo.exit(err);
});
```
