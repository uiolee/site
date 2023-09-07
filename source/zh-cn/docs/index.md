---
title: 文件
---

欢迎使用 Hexo 文档。 如果您在使用 Hexo 时遇到任何问题，请查看  [故障排除指南](troubleshooting.html)， 在 [GitHub](https://github.com/hexojs/hexo/issues) 上提出一个问题，或在 [Google Group](https://groups.google.com/group/hexo) 上开始一个主题。

## 十六进制是什么？

Hexo 是一个快速、简单和强大的博客框架。 您在 [Markdown](http://daringfireball.net/projects/markdown/) (或其他标记语言) 中写帖子，Hexo 生成一个美丽主题的静态文件。

## 安装

设置十六进制只需要几分钟时间。 If you encounter a problem and can't find the solution here, please [submit a GitHub issue](https://github.com/hexojs/hexo/issues) and we'll help.

{% youtube ARted4RniaU %}

### B. 所需经费

安装 Hexo 非常容易，只需要事先以下几项：

- [Node.js](http://nodejs.org/) (至少是 Node.js 10.13, 推荐的 12.0 或更高)
- [Git](http://git-scm.com/)

如果您的电脑已经有这些，恭喜！ 您可以跳转到 [十六进制安装](#Install-Hexo) 步骤。

如果没有，请按照以下说明安装所有要求。

### Install Git

- Windows: 下载 & 安装 [git](https://git-scm.com/download/win)
- Mac：使用 [Homebrew](https://brew.sh/)、 [MacPorts](http://www.macports.org/) 或 [安装器](http://sourceforge.net/projects/git-osx-installer/) 安装。
- Linux (Ubuntu, Debian): `sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS): `sudo yum install git-core`

{% note warn For Mac users %}
编译时可能遇到一些问题。 请先从 App Store 安装 Xcode。 Xcode 安装后， 打开 Xcode 并到 **首选项 -> 下载 -> 命令行工具 -> 安装** 以安装命令行工具
{% endnote %}

### 安装 Node.js

Node.js 为大多数平台提供 [官方安装器](https://nodejs.org/en/download/)。

替代安装方法：

- Windows：安装为 [nvs](https://github.com/jasongin/nvs/) (推荐) 或 [nvm](https://github.com/nvm-sh/nvm)
- Ma: 使用 [Homebrew](https://brew.sh/) 或 [MacPorts](http://www.macports.org/) 安装它
- Linux (DEB/RPM-based): Install it with [NodeSource](https://github.com/nodesource/distributions).
- 其它: 通过各自的软件包管理器安装它。 参考 [Node.js提供的指南](https://nodejs.org/en/download/package-manager/)。

也推荐Mac 和Linux使用nvs，以避免可能的权限问题。

{% note info Windows %}
If you use the official installer, make sure **Add to PATH** is checked (it's checked by default).
{% endnote %}

{% note warn Mac / Linux %}
如果您试图安装十六进制时遇到 `EACCES` 权限错误 请跟随 [npmjs提供的](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) 周围的工作； 极不鼓励使用root/sudo覆盖。
{% endnote %}

{% note info Linux %}
If you installed Node.js using Snap, you may need to manually run `npm install` in the target folder when [initializing](/docs/commands#init) a blog.
{% endnote %}

### 安装 Hexo

一旦安装了所有的要求，您可以使用 npm 安装 Hexo ：

``` bash
$ npm install -g hexo-cli
```

### 高级安装和使用

Advanced users may prefer to install and use `hexo` package instead.

``` bash
$ npm install hexo
```

安装完毕后，您可以通过以下两种方式运行 Hexo ：

1. `npx hexo <command>`
2. Linux users can set relative path of `node_modules/` folder:

  ``` bash
  echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
  ```

  然后使用 `十六进制 <command>` 运行十六进制功能

### 所需的 Node.js 版本

如果你被旧的 Node.js卡住，你可以考虑安装过去版本的 Hexo。

请注意我们不要为过去版本的 Hexo 提供漏洞修复。

我们强烈建议在可能的情况下始终安装 [最新版本的Hexo](https://www.npmjs.com/package/hexo?activeTab=versions) 和 [推荐版本的](#Requirements) Node.js。

| Hexo 版本     | 最小值 (Node.js 版本) | 小于 (Node.js 版本) |
| ----------- | ---------------- | --------------- |
| 6.2+        | 12.13.0          | 最新的             |
| 6.0+        | 12.13.0          | 18.5.0          |
| 5.0+        | 10.13.0          | 12.0.0          |
| 4.1 - 4.2   | 8.10             | 10.0.0          |
| 4.0         | 8.6              | 8.10.0          |
| 3.3 - 3.9   | 6.9              | 8.0.0           |
| 3.2 - 3.3   | 0.12             | 未知              |
| 3.0 - 3.1   | 0.10或iojs        | 未知              |
| 0.0.1 - 2.8 | 0.10             | 未知              |
