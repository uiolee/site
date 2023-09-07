---
title: 控制台
---

该控制台是Hexo与其用户之间的桥梁。 它注册并描述可用的控制台命令。

## 简述

``` js
hexo.extend.console.register(name, desc, options, function(args))@un.org.
  // ...
});
```

| 参数     | 描述   |
| ------ | ---- |
| `名称`   | 名称   |
| `desc` | 描述   |
| `选项`   | 备选方案 |

一个参数 `args` 将会传入函数中。 这是用户输入终端的参数。 由 [最小化][] 解析。

## 备选方案

### 使用情况

控制台命令的使用。 例如：

``` js
{用法: '[layout] <title>
// 十六进制新 [layout] <title>
```

### 参数

控制台命令的每个参数的描述。 例如：

``` js
许
  参数：[
    {name: 'layout', desc: 'Post layout'},
    {name: 'title', desc: 'Post title'}
  ]
}
```

### 选项

控制台命令的每个选项的描述。 例如：

``` js
许
  选项：[
    {name: '-r, --replace', desc: 'Replace existing files'}
  ]
}
```

### desc

更多关于控制台命令的详细信息。

## 示例

``` js
hexo.extend.console.register('config', 'Display configuration', function(args){
  console.log(hexo.config);
});
```

[最小化]: https://github.com/minimistjs/minimist
