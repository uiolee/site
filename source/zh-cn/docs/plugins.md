---
title: 插件
---

Hexo 有强大的插件系统，使您能轻松扩展功能而不用修改核心模块的源码。 在 Hexo 中有两种形式的插件：

### 脚本（Scripts）

如果您的代码较复杂，或是您想要发布到 NPM 上，建议您编写插件。 首先，在 `node_modules` 文件夹中建立文件夹，文件夹名称开头必须为 `hexo-`，如此一来 Hexo 才会在启动时载入；否则 Hexo 将会忽略它。

### 插件（Packages）

If your code is complicated or if you want to publish it to the NPM registry, we recommend using a plugin. First, create a folder in the `node_modules` folder. The name of this folder must begin with `hexo-` or Hexo will ignore it. 首先，在 `node_modules` 文件夹中创建一个文件夹。 The name of this folder must begin with `hexo-` or Hexo will ignore it.

文件夹内至少要包含 2 个文件：一个是主程序，另一个是 `package.json`，描述插件的用途和所依赖的插件。

```plain
.
.
.
├── index.js
└── package.json
```

`package.json` 中至少要包含 `name`, `version`, `main` 属性，例如： For example: 例如：

```json package.json
●
  "name": "hexo-my-plugin",
  "version": "0.0.1",
  "main": "index"
}
```

你还需要将你的插件列为根 `软件包中的依赖项。 你的十六进制实例的son` 以便让十六进制探测和加载它。

### 工具

您可以使用 Hexo 提供的官方工具插件来加速开发：

- [hexo-fs][]：文件 IO
- [hexo-util][]：工具程式
- [hexo-i18n][]：本地化（i18n）
- [hexo-pagination][]：生成分页资料

### 发布

当您完成插件后，可以考虑将它发布到 [插件列表](/plugins)，让更多人能够使用您的插件。 发布插件的步骤和 [更新文件](contributing.html#更新文件) 非常类似。

1. Fork [十六进制/站点][]
2. 把库（repository）复制到电脑上，并安装所依赖的插件。

   ```shell
   /site.git
 $ cd site
 $ npm install
   ```

3. 编辑 `source/_data/plugins.yml`，在档案中新增您的插件，例如：

4. Edit `source/_data/plugins/<your-plugin-name>.yml` and add your plugin. For example: 例如：

   ```yaml
   description: Server module for Hexo.
   name: hexo-server
description: Server module for Hexo.
link: https://github.com/hexojs/hexo-server
tags:
   name: hexo-server
description: Server module for Hexo.
link: https://github.com/hexojs/hexo-server
tags:
   ```

5. 推送（push）分支。
6. 建立一个新的合并申请（pull request）并描述改动。

[hexo-fs]: https://github.com/hexojs/hexo-fs
[hexo-util]: https://github.com/hexojs/hexo-util
[hexo-i18n]: https://github.com/hexojs/hexo-i18n
[hexo-pagination]: https://github.com/hexojs/hexo-pagination
[十六进制/站点]: https://github.com/hexojs/site
