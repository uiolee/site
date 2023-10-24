---
title: 过滤器（Filter）
---

过滤器用于修改某些指定的数据。 十六进制将数据按顺序传递给过滤器，然后过滤器逐个修改数据。 这个概念是从 [WordPress](http://codex.wordpress.org/Plugin_API#Filters) 借用的。

## 概要

``` js
hexo.extend.filter.register(type, function() {
  // User configuration
  const { config } = this;
  if (config.external_link.enable) // do something...

  // Theme configuration
  const { config: themeCfg } = this.theme;
  if (themeCfg.fancybox) // do something...

}, priority);

  // 主题配置
  const { config: themeCfg } = 这个主题；
  if (athemeCfg.fancybox) // 做一些事情...

}，优先事项；
```

您可以定义 `优先级`。 降低 `优先级` 意味着它将先执行。 您可以指定过滤器的优先级 `priority`，`priority` 值越低，过滤器会越早执行，默认的 `priority` 是 10。 我们建议提供配置选项如 `hexo.config.your_plugin.priority`、让用户自行决定过滤器的优先级。

## 执行过滤器

``` js
hexo.extend.filter.exec(type, data, options);
hexo.extend.filter.execSync(type, data, options);
```

| 选项     | 描述         |
| ------ | ---------- |
| `上下文：` | 二. 背景      |
| `args` | 参数。 必须为数组。 |

`data` 会作为第一个参数传入每个过滤器，而您可以在过滤器中通过返回值改变下一个过滤器中的 `data`，如果什么都没有返回的话则会保持原本的 `data`。 传递到下一个过滤器的 `数据` 可以通过返回一个新的值来修改。 如果没有返回，数据将保持不变。 您还可以使用 `args` 指定过滤器的其他参数。 举例来说：

``` js
hexo.extend.filter.register('test', function(data, arg1, arg2){
  // data === 'some data'
  // arg1 === 'foo'
  // arg2 === 'bar'

  return 'something';
});

hexo.extend.filter.register('test', function(data, arg1, arg2){
  // data === 'something'
});

hexo.extend.filter.exec('test', 'some data', {
  args: ['foo', 'bar']
});
```

您也可以使用以下方法来执行过滤器：

``` js
hexo.execFilter(类型、数据、选项)；
hexo.execFilterSync(类型、数据、选项)；
```

## 移除过滤器

``` js
hexo.extend.filter.unregister(类型，过滤)；
```

**示例**

``` js
// 移除一个使用具名函数注册的过滤器

const filterFn = (data) => {
  data = 'something';
  return data;
};
hexo.extend.filter.register('example', filterFn);

hexo.extend.filter.unregister('example', filterFn);
```

``` js
// 移除一个使用 CommonJS 模块注册的过滤器

hexo.extend.filter.register('example', require('path/to/filter'));

hexo.extend.filter.unregister('example', require('path/to/filter'));
```

## 过滤器列表

以下是 Hexo 所使用的过滤器。

### previ_post_render

在文章开始渲染前执行。 您可以参考 [文章渲染](posts.html#渲染) 以了解执行顺序。

举例来说，把标题转为小写：

``` js
hexo.extend.filter.register('before_post_render', function(data){
  data.title = data.title.toLowerCase();
  return data;
});
```

### 后 post_render

在文章渲染完成后执行。 您可以参考 [文章渲染](posts.html#渲染) 以了解执行顺序。

举例来说，把 `@username` 取代为 Twitter 的开发者链接。

``` js
hexo.extend.filter.register('after_post_render', function(data){
  data.content = data.content.replace(/@(\d+)/, '<a href="http://twitter.com/$1">#$1</a>');
  return data;
});
```

### 退出前

在 Hexo 即将结束时执行，也就是在 `hexo.exit` 被调用后执行。

``` js
hexo.extend.filter.register('before_exit', function(){
  // ...
});
});
```

### 之前生成

在生成器解析前执行。

``` js
hexo.extend.filter.register('before_generate', function(){
  // ...
});
});
```

### 生成后

生成完成后执行。

``` js
hexo.extend.filter.register('after_generate', function(){
  // ...
});
});
```

### template_locals

修改模板的 [局部变量](../docs/variables.html)。

举例来说，在模板的局部变量中新增当前时间：

``` js
hexo.extend.filter.register('template_locals', functions(locals)}.
  locals.now = Date.no();
  return locals;
});
```

### 输入后

在 Hexo 初始化完成后执行，也就是在 `hexo.init` 执行完成后执行。

``` js
hexo.extend.filter.register('after_init', function()@un.org.
/...
});
```

### 新 post_post路径

用来决定新建文章的路径，在建立文章时执行。

``` js
hexo.extend.filter.register('new_post_path', function(data, replace){
  // ...
});
});
```

### 帖子永久链接

用于确定帖子的永久链接。

``` js
hexo.extend.filter.register('post_permalink', function(data){
  // ...
});
});
```

### 渲染后

渲染完成后执行。 在渲染后执行，您可以参考 [渲染](rendering.html#after-render-过滤器) 以了解更多信息。

### 清理后

Executed after generated files and cache are removed with `hexo clean` command.

``` js
hexo.extend.filter.register('after_init', function(){
  // ...
});
```

### server_midleware

新增服务器的 Middleware。 `app` 是一个 [Connect][] 实例。

举例来说，在响应头中新增 `X-Powered-By: Hexo`。

``` js
hexo.extend.filter.register('server_middlewares', function(app)_
  app.use(function(req, res, next)_
    res.setHeader('X-Powere-By', 'Hexo');
    next ();
  });
});
```

[Connect]: https://github.com/senchalabs/connect
