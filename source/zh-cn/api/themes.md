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

模板本身有两个方法可供使用：`render` 和 `renderSync`。 这两种方法是相同的，但前者是异步的，后者是同步的。 所以为了简洁起见，我们将只在这里讨论 `变成`。

``` js
var view = hexo.theme.getView('layout.swig');

view.render({foo: 1, bar: 2}).then(function(result){
  // ...
});
});
```

您可以以向 `render` 方法传入对象作为参数，`render` 方法会先使用对应的渲染引擎进行解析，并加载 [辅助函数](helper.html)。 当渲染完成时，它会尝试找到布局是否存在。 如果 `布局` 为 `错误` 或者如果它不存在，结果将直接退回。
