---
title: 服务器
---

## [十六进制服务器][]

在 Hexo 3 发布后，服务器已经从主模块中分离。 要开始使用服务器，您必须先安装 [十六进制服务器][]。

``` bash
$ npm 安装十六进制服务器 --save
```

一旦服务器安装完毕，运行以下命令启动服务器。 Your website will run at `http://localhost:4000` by default. 当服务器正在运行时，Hexo将监视文件更改并自动更新，因此无需手动重启服务器。

``` bash
$ 十六进制服务器
```

If you want to change the port or if you're encountering `EADDRINUSE` errors, use the `-p` option to set a different port.

``` bash
$ 十六进制服务器-p 5000
```

### 静态模式

在静态模式下，只有 `公共` 文件夹中的文件将被服务，文件监视被禁用。 You have to run `hexo generate` before starting the server. 通常用于生产。

``` bash
$ 十六进制服务器 -s
```

### 自定义 IP

Hexo 默认在 `0.0.0.0` 运行服务器。 您可以覆盖默认IP设置。

``` bash
$十六进制服务器 -i 192.168.1.1
```

[十六进制服务器]: https://github.com/hexojs/hexo-server
