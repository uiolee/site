---
title: 路由器
---

路由器保存站点中使用的所有路径。

## 获取路径

The `get` method returns a [Stream][]. 例如，要将路径数据保存到指定目的地：

``` js
var data = hexo.route.get('index.html');
var test = fs.createWriteStream('somwhere');

data.pipe(dest);
```

## 设置路径

`设置` 方法需要一个字符串， [缓存][] 或一个函数。

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

您还可以设置一个是否修改路径的布尔值。 这可以加速文件生成，因为它允许忽略未修改的文件。

``` js
hexo.route.set('index.html', {
    data: 'index',
    modified: false
});

// hexo.route.isModified('index.html') => false
```

## 删除路径

``` js
hexo.route.remove('index.html');
```

## 获取路由列表

``` js
十六进制列表();
```

## 格式化路径

`格式` 方法将字符串转换为有效路径。

``` js
十六进制格式('archives/');
// archives/index.html
```

[Stream]: http://nodejs.org/api/stream.html
[缓存]: http://nodejs.org/api/buffer.html
