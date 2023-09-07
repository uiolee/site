---
title: 正在生成
---

使用 Hexo 生成静态文件是相当容易和快速的。

``` bash
$ 十六进制生成
```

{% youtube viEJQPVCoLU %}

### 监视文件更改

Hexo 可以立即监视文件更改并重新生成文件。 Hexo 将比较您的文件的 SHA1 校验和，并且只在检测到文件更改时写入。

``` bash
$ 十六进制生成 --watch
```

### 生成后部署

要在生成后进行部署，您可以运行以下一个命令。 两者之间没有区别。

``` bash
$ hexo 生成 --depution
$ hexo 部署 --generate
```
