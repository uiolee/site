---
title: 生成文件
---

使用 Hexo 生成静态文件快速而且简单。

``` bash
$ 十六进制生成
```

{% youtube viEJQPVCoLU %}

### 监视文件变动

Hexo 可以立即监视文件更改并重新生成文件。 Hexo 能够监视文件变动并立即重新生成静态文件，在生成时会比对文件的 SHA1 checksum，只有变动的文件才会写入。

``` bash
$ 十六进制生成 --watch
```

### 完成后部署

要在生成后进行部署，您可以运行以下一个命令。 两者之间没有区别。

``` bash
$ hexo 生成 --depution
$ hexo 部署 --generate
```
