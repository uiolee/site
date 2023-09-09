---
title: 控制台（Console）
---

控制台是 Hexo 与开发者之间沟通的桥梁。 It registers and describes the available console commands.

## 概要

``` js
hexo.extend.console.register(name, desc, options, function(args){
  // ...
});
});
```

| Argument  | 描述 |
| --------- | -- |
| `name`    | 名称 |
| `desc`    | 描述 |
| `options` | 选项 |

An argument `args` will be passed into the function. This is the argument that users type into the terminal. It's parsed by [Minimist][].

## 选项

### 用法

The usage of a console command. For example:

``` js
{usage: '[layout] <title>'}
// hexo new [layout] <title>
```

### arguments

控制台各个参数的说明，例如： For example:

``` js
{
  arguments: [
    {name: 'layout', desc: 'Post layout'},
    {name: 'title', desc: 'Post title'}
  ]
}
```

### options

The description of each option of a console command. For example:

``` js
{
  options: [
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
