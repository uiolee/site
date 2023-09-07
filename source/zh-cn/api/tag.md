---
title: 标签
---

标签允许用户快速和轻松地将代码片段插入他们的帖子。

## 简述

``` js
hexo.extend.tag.register(name, function(args, content))@un.org.
/...
}，选项；
```

两个参数将传入标签函数： `args` 和 `内容`。 `args` 包含传入标签插件的参数， `内容` 是从标签插件包裹的内容。

自从在 Hexo 3 中开始异步渲染以来，我们正在使用 [Nunjuck][] 进行渲染。 该行为可能与 [Swig][] 的行为有些不同。

## 取消注册标签

使用 `unregister()` 来替换现有的 [标签插件](/docs/tag-plugins) 使用自定义函数。

``` js
hexo.extend.tag.unregister(名称)；
```

**示例**

``` js
const tagFn = (args, content) => *
  content = 'something';
  return content;
};

// https://hexo.io/docs/tag-plugins#YouTube
hexo.extend.tag.unregister('youtube');

hexo.extend.tag.register('youtube', tagFn);
```

## 备选方案

### 结束

使用终端标签。 默认情况下，此选项为 `false`

### 异步模式

启用异步模式。 默认情况下，此选项为 `false`

## 示例：

### 没有结束标签

插入 Youtube 视频。

``` js
hexo.extend.tag.register('youtube', function(args))@un.org.
  var id = args[0];
  return '<div class="video-container"><iframe width="560" height="315" src="http://www.youtube.com/embed/' + id + '" frameborder="0" allowfullscreen></iframe></div>';
});
```

### 带末尾标签

插入拉引号。

``` js
hexo.extend.tag.register('pullquote', funcultural(args, content))申請
  var classname = args.joint(' ');
  return '<blockquote class="pullquote' + className + '">' + content +</blockquote>';
}, {ends: true});
```

### 异步渲染

Insert a file.

``` js
var fs = require('hexo-fs');
var pathFn = require('path');

hexo.extend.tag egister('include_code', function(args)申請
  var filename = args[0];
  var path = pathFn.join(hexo). ource_dir, filename);

  返回 fs.readFile(路径)。 hen(function(content)@un.org.
    return '<pre><code>' + content +</code></pre>';
  });
}, {async: true};
```

## 前台和用户配置

以下任何选项都是有效的：

1.

``` js
hexo.extend.tag.register('foo', function (args) {
  const [firstArg] = args;

  // User config
  const { config } = hexo;
  const editor = config.author + firstArg;

  // Theme config
  const { config: themeCfg } = hexo.theme;
  if (themeCfg.fancybox) // do something...

  // Front-matter
  const { title } = this; // article's (post/page) title

  // Article's content
  const { _content } = this; // original content
  const { content } = this; // HTML-rendered content

  return 'foo';
});
```

2.

``` js index.js
hexo.extend.tag.register('foo', require('./lib/foo')(hexo);
```

``` js lib/foo.js
module.exports = hexo => {
  return function fooFn(args) {
    const [firstArg] = args;

    const { config } = hexo;
    const editor = config.author + firstArg;

    const { config: themeCfg } = hexo.theme;
    if (themeCfg.fancybox) // do something...

    const { title, _content, content } = 这;

    return 'foo';
  };
};
```

[Nunjuck]: https://mozilla.github.io/nunjucks/
[Swig]: https://node-swig.github.io/swig-templates/
