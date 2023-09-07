---
title: 部署器（Deployer）
---

部署器帮助开发者将网站快速部署到远程服务器上，避免了复杂的指令。

## 概要

``` js
hexo.extend.deployer.register(name, function(args){
  // ...
});
});
});
```

在函数中会传入 `args` 参数，该参数包含了 `_config.yml` 中的 `deploy` 参数值，以及开发者在终端中所传入的参数。 它包含 `_config.yml`中设置的 `部署的` 值，以及输入他们的终端的确切输入用户。
