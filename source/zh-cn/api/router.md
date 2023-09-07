---
title: 路由
---

路由存储了网站中所用到的所有路径。

## 获取路径

`get` 方法会传回一个 [Stream][]，例如把该路径的资料存储到某个指定位置。 例如，要将路径数据保存到指定目的地：

``` js
var data = hexo.route.get('index.html');
var test = fs.createWriteStream('somwhere');

data.pipe(dest);
```

## 设置路径

您可以在 `set` 方法中使用字符串、[Buffer][] 或函数，如下：

``` js
// String
hexo.route.set('index.html', 'index')

// Buffer
hexo.route.set('index.html', new Buffer('index');

// 函数(Promise)
hexo.route.set('index. tml', function()pension()post.
  return new Promise(function(resolve, reject))por
    resolve('index');
  });
});

// 函数 (Callback)
hexo. oute.set('index.html', function(callback)@un.org,
  callback(null, 'index');
});
```

You can also set a boolean for whether a path has been modified or not. This can speed up file generation as it allows for ignoring the unmodified files. 这可以加速文件生成，因为它允许忽略未修改的文件。

``` js
hexo.route.set('index.html', {
    data: 'index',
    modified: false
});

// hexo.route.isModified('index.html') => false
```

## 移除路径

``` js
hexo.route.remove('index.html');
```

## 获取路由列表

``` js
十六进制列表();
```

## 格式化路径

`format` 方法可将字符串转为合法的路径。

``` js
十六进制格式('archives/');
// archives/index.html
```

[Stream]: http://nodejs.org/api/stream.html
[Buffer]: http://nodejs.org/api/buffer.html
