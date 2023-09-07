---
title: 筛选器
---

过滤器用于修改某些指定的数据。 十六进制将数据按顺序传递给过滤器，然后过滤器逐个修改数据。 这个概念是从 [WordPress](http://codex.wordpress.org/Plugin_API#Filters) 借用的。

## 简述

``` js
hexo.extend.filter.register(type, function() {
  // User configuration
  const { config } = this;
  if (config.external_link.enable) // do something...

  // 主题配置
  const { config: themeCfg } = 这个主题；
  if (athemeCfg.fancybox) // 做一些事情...

}，优先事项；
```

您可以定义 `优先级`。 降低 `优先级` 意味着它将先执行。 默认 `优先级` 是 10。 我们建议使用用户可以在配置中指定的用户配置优先级值，例如： `hexo.config.your_plugin.priority`。

## 执行过滤器

``` js
hexo.extend.filter.exec(type, data, options);
hexo.extend.filter.execSync(type, data, options);
```

| 选项     | 描述            |
| ------ | ------------- |
| `上下文：` | 二. 背景         |
| `args` | 参数. 这必须是一个数组。 |

第一个参数传递到每个过滤器中的 `数据`。 传递到下一个过滤器的 `数据` 可以通过返回一个新的值来修改。 如果没有返回，数据将保持不变。 您甚至可以使用 `args` 在过滤器中指定其他参数。 例如：

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

## 取消注册过滤器

``` js
hexo.extend.filter.unregister(类型，过滤)；
```

**示例**

``` js
// 取消注册一个已命名函数

const filterFn = (data) => Power
  data = 'something';
  返回数据;
};
十六进制. xtend.filter.register('example', filterFn);

hexo.extend.filter.unregister('example', filterFn);
```

``` js
// Unregister a filter which is registered with commonjs module

hexo.extend.filter.register('example', require('path/to/filter'));

hexo.extend.filter.unregister('example', require('path/to/filter'));
```

## 筛选列表

这是十六进制使用的过滤器列表。

### previ_post_render

在帖子渲染之前执行. Refer to [post rendering](posts.html#Render) to learn the execution steps.

例如，要将标题转换为较低的案件：

``` js
hexo.extend.filter.register('before_post_render', function(data){
  data.title = data.title.toLowerCase();
  return data;
});
```

### 后 post_render

在一个帖子呈现后执行。 Refer to [post rendering](posts.html#Render) to learn the execution steps.

例如，要将 `@username` 替换为 Twitter 配置文件的链接：

``` js
hexo.extend.filter.register('after_post_render', function(data){
  data.content = data.content.replace(/@(\d+)/, '<a href="http://twitter.com/$1">#$1</a>');
  return data;
});
```

### 退出前

十六进制将要退出前执行 — — 这将在 `十六进制后正常运行。 退出`

``` js
hexo.extend.filter.register('before_exit', function()}.
  // ...
});
```

### 之前生成

在生成开始之前执行。

``` js
hexo.extend.filter.register('befor_generate', function()}.
  // ...
});
```

### 生成后

生成完成后执行。

``` js
hexo.extend.filter.register('after_generate', function(){
  // ...
});
```

### template_locals

在模板中修改 [本地变量](../docs/variables.html)。

例如，要将当前时间添加到模板的本地变量：

``` js
hexo.extend.filter.register('template_locals', functions(locals)}.
  locals.now = Date.no();
  return locals;
});
```

### 输入后

Executed after Hexo is initialized -- this will run right after `hexo.init` completes.

``` js
hexo.extend.filter.register('after_init', function()@un.org.
/...
});
```

### 新 post_post路径

创建一个帖子时执行，以确定新帖子的路径。

``` js
hexo.extend.filter.register('new_post_path', function(data, replace)).P.
  // ...
});
```

### 帖子永久链接

用于确定帖子的永久链接。

``` js
hexo.extend.filter.register('post_permalink', function(data){
  // ...
});
```

### 渲染后

渲染完成后执行。 您可以看到 [渲染](rendering.html#after_render_Filters) 获取更多信息。

### 清理后

Executed after generated files and cache are removed with `hexo clean` command.

``` js
hexo.extend.filter.register('after_clean', function()Pop
  // 移除一些其他临时文件
});
```

### server_midleware

添加中间件到服务器。 `App` 是一个 [连接][] 实例。

例如，要将 `X-Poed-by: Hexo` 添加到响应头部：

``` js
hexo.extend.filter.register('server_middlewares', function(app)_
  app.use(function(req, res, next)_
    res.setHeader('X-Powere-By', 'Hexo');
    next ();
  });
});
```

[连接]: https://github.com/senchalabs/connect
