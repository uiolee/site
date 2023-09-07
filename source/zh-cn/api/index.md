---
title: API
---

本文件提供您更丰富的 API 信息，使您更容易修改 Hexo 源代码或编写插件。 如果您只是想查询 Hexo 的基本使用方法，请参阅 [文档](../docs/)。

在开始之前，请注意本文件仅适用于 Hexo 3 及以上版本。

## 初始化

First, we have to create a Hexo instance. 首先，我们必须建立一个 Hexo 实例（instance），第一个参数是网站的根目录，也就是 `base_dir`，而第二个参数则是初始化的选项。 首先，我们必须建立一个 Hexo 实例（instance），第一个参数是网站的根目录，也就是 `base_dir`，而第二个参数则是初始化的选项。 接着执行 `init` 方法后，Hexo 会加载插件及配置文件。

``` js
var Hexo = require('hexo');
var hexo = new Hexo(process.cwd(), {});

hexo.init().then(function(){
  // ...
});
});
});
```

| 选项          | 描述                                                              | 默认值                              |
| ----------- | --------------------------------------------------------------- | -------------------------------- |
| `debug`     | 开启调试模式。 在终端中显示调试信息，并在根目录中存储 `debug.log` 日志文件。                   | `false`                          |
| `安全`        | 开启安全模式。 不加载任何插件。                                                | `false`                          |
| `静音`        | 开启安静模式。 不在终端中显示任何信息。                                            | `false`                          |
| `配置`        | 指定配置文件的路径。                                                      | `yml`                            |
| `草稿` / `草稿` | 是否将草稿加入到文章列表中。 <br>例如在 `hexo.locals.get('posts')` 中获取草稿内容 | _config.yml 中 `render_drafts` 的值 |

## 载入文件

Hexo 提供了两种方法来载入文件：`load`, `watch`，前者用于载入 `source` 文件夹内的所有文件及主题资源；而后者除了执行 `load` 以外，还会继续监视文件变动。 `加载` 用于加载 `源` 中的所有文件以及主题数据。 `load` is used for loading all files in the `source` folder as well as the theme data. `watch` does the same things `load` does, but will also start watching for file changes continuously.

Both methods will load the list of files and pass them to the corresponding processors. After all files have been processed, they will call upon the generators to create the routes. 在所有文件处理完毕后，他们将呼叫发电机来创建路线。

``` js
hexo.load().then(function(){
  // ...
hexo.load().then(function(){
  // ...
hexo.load().then(function(){
  // ...
});

hexo.watch().then(function(){
  // 之后可以调用 hexo.unwatch()，停止监视文件
});
});
});
```

## 执行指令

Any console command can be called explicitly using the `call` method on the Hexo instance. Such a call takes two arguments: the name of the console command, and an options argument. Different options are available for the different console commands. 这种调用需要两个论点：控制台命令的名称和选项参数。 不同的控制台命令有不同的选项。

``` js
hexo.call('generate', {}).then(function(){
  // ...
});
});
});
```

``` js
hexo.call('list', { _: ['post'] }).then(function() {
  // ...
})
})
```

## 结束

You should call the `exit` method upon successful or unsuccessful completion of a console command. This allows Hexo to exit gracefully and finish up important things such as saving the database. 这使Hexo能够体面地退出并完成保存数据库等重要工作。

``` js
hexo.call('generate').then(function()own
  return hexo.exit();
}).catch(function(err)paper.
  return hexo.exit(err);
});
```
