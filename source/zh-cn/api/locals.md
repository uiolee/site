---
title: 本地变量
---

本地变量用于模板渲染，这是模板中的 `站点` 变量。

## 默认变量

| 变量   | 描述   |
| ---- | ---- |
| `帖子` | 所有帖子 |
| `页面` | 所有页面 |
| `类别` | 所有类别 |
| `标签` | 所有标签 |

## 获取变量

``` js
hexo.locals.get('posts')
```

## 设置变量

``` js
hexo.locals.set('posts', function()@un.org
  返回 ...
});
```

## 删除变量

``` js
hexo.locals.remove('posts');
```

## 获取所有变量

``` js
hexo.locals.toObject();
```

## 禁用缓存

``` js
hexo.locals.invalidate();
```
