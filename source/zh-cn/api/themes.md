---
title: 主题
---

`hexo.theme` 除了继承 [Box](box.html) 外，还具有存储模板的功能。

## 获取视图

``` js
十六进制主题.getView(路径)；
```

## 设置视图

``` js
hexo.theme.setView(路径，数据)；
```

## 移除视图

``` js
十六进制主题.移除视图(路径)；
```

## 查看

模板本身有两个方法可供使用：`render` 和 `renderSync`。 These two methods are identical, but the former is asynchronous and the latter is synchronous. So for the sake of simplicity, we will only discuss `render` here. 所以为了简洁起见，我们将只在这里讨论 `变成`。

``` js
var view = hexo.theme.getView('layout.swig');

view.render({foo: 1, bar: 2}).then(function(result){
  // ...
});
});
});
```

您可以以向 `render` 方法传入对象作为参数，`render` 方法会先使用对应的渲染引擎进行解析，并加载 [辅助函数](helper.html)。 当渲染完成时，它会尝试找到布局是否存在。 When rendering is complete, it will try to find whether a layout exists. If `layout` is `false` or if it doesn't exist, the result will be returned directly.
