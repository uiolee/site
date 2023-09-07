---
title: 控制台（Console）
---

控制台是 Hexo 与开发者之间沟通的桥梁。 它注册并描述可用的控制台命令。

## 概要

``` js
hexo.extend.console.register(name, desc, options, function(args){
  // ...
});
});
});
```

| 参数     | 描述 |
| ------ | -- |
| `名称`   | 名称 |
| `desc` | 描述 |
| `选项`   | 选项 |

一个参数 `args` 将会传入函数中。 这是用户输入终端的参数。 An argument `args` will be passed into the function. This is the argument that users type into the terminal. It's parsed by [Minimist][].

## 选项

### 用法

The usage of a console command. For example: 例如：

``` js
{用法: '[layout] <title>
// 十六进制新 [layout] <title>
```

### 参数

控制台各个参数的说明，例如： 例如：

``` js
许
  参数：[
    {name: 'layout', desc: 'Post layout'},
    {name: 'title', desc: 'Post title'}
  ]
}
```

### 选项

The description of each option of a console command. For example: 例如：

``` js
许
  选项：[
    {name: '-r, --replace', desc: 'Replace existing files'}
  ]
}
```

### desc

关于控制台命令的更详细的信息。

## 范例

``` js
hexo.extend.console.register('config', 'Display configuration', function(args){
  console.log(hexo.config);
});
```

[Minimist]: https://github.com/minimistjs/minimist
