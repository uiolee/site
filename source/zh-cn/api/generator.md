---
title: 生成器
---

生成器基于已处理文件构建路由。

## 简述

``` js
hexo.extend.generator.register(name, functification(locals)@un.org.
/...
});
```

`locals` 参数将被传递到函数中，包含 [站点变量](../docs/variables.html#Site-Variables)。 您应该使用此参数获取网站数据，从而避免直接访问数据库。

## 更新路由

``` js
hexo.extend.generator.register('test', function(locals)}.
  // Object
  return {
    path: 'foo',
    data: 'foo'
  };

  // 数组
  return [
    {path: 'foo', data: 'foo'},
    {path: 'bar', data: 'bar'}
  ];
});
```

| 属性   | 描述                                            |
| ---- | --------------------------------------------- |
| `路径` | Path not including the prefixing `/`.         |
| `数据` | 数据                                            |
| `布局` | 布局。 指定渲染的布局。 值可以是字符串或数组。 如果它被忽略，路由将直接返回 `数据`。 |

当源文件被更新时，Hexo将执行所有的发电机并重建路径。 **Please return the data and do not access the router directly.**

## 示例

### 归档页面

Create an archive page at `archives/index.html`. 我们将所有帖子作为数据传递到模板中。 此数据等于模板中的 `页面` 变量。

Next, set the `layout` attribute to render with the theme templates. 我们在此示例中设置两个布局：如果 `存档` 布局不存在，则将使用 `索引` 布局。

``` js
hexo.extend.generator.register('archive', function(locals){
  return {
    path: 'archives/index.html',
    data: locals,
    layout: ['archive', 'index']
  }
});
```

### 带分页归档页面

您可以使用方便的官方工具 [十六进制][] 来轻松构建带分页的归档页面。

``` js
var pagination = require('hexo-pagination');

hexo.extend.generator.register('archive', funculturals', locals)power
  // hexo-pagination make 一个索引。 tml for the /archives route
  return pagination('archives', locals. osts, 常务副秘书长,
    perPage: 10,
    layout: ['archive', 'index']，
    数据：{}
  })；
})；
```

### 生成所有帖子

Iterate over all posts in `locals.posts` and create routes for all the posts.

``` js
hexo.extend.generator.register('post', function(locals){
  return locals.posts.map(function(post){
    return {
      path: post.path,
      data: post,
      layout: 'post'
    };
  });
});
```

### 复制文件

这次我们不会明确返回数据，而是将 `数据` 设置为一个函数，因此路由将会生成 `fs。 eadStream` 只在需要时进行。

``` js
var fs = require('hexo-fs');

hexo.extend.generator.register('asset', funcult(locals))_
  return
    path: 'file.txt',
    data: function()_
      return fs.createReadStream('path/to/file.txt')
    }
  };
});
```

[十六进制]: https://github.com/hexojs/hexo-pagination
