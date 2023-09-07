---
title: 插件
---

Hexo 有一个功能强大的插件系统，它可以方便扩展功能，而不修改核心模块的源代码。 Hexo有两种插件：

### 脚本

如果你的插件相对简单，建议使用脚本。 您需要做的只是将您的 JavaScript 文件放入 `脚本` 文件夹，Hexo 将在初始化过程中加载它们。

### 插件

如果你的代码是复杂的，或者如果你想要将它发布到NPM注册表，我们建议使用一个插件。 首先，在 `node_modules` 文件夹中创建一个文件夹。 The name of this folder must begin with `hexo-` or Hexo will ignore it.

您的新文件夹必须包含至少两个文件：一个包含实际的 JavaScript 代码和 `包。 son` 文件描述了插件的目的并设置了它的依赖性。

```plain
.
├── index.js
└── package.json
```

至少，您应该设置 `名称`, `版本` 和 `主` 在 `package.json` 中的条目。 例如：

```json package.json
●
  "name": "hexo-my-plugin",
  "version": "0.0.1",
  "main": "index"
}
```

你还需要将你的插件列为根 `软件包中的依赖项。 你的十六进制实例的son` 以便让十六进制探测和加载它。

### 工具

您可以使用Hexo提供的官方工具来加速开发：

- [hexo-fs][]：File IO
- [hexo-util][]：Utilities
- [十六进制][]：本地化 (i18n)
- [hexo-pagination][]：Generate pagination data

### 发布

When your plugin is ready, you may consider publishing it to the [plugin list](/plugins) to invite other people to start using it. 发布您自己的插件非常类似于 [更新文档](contributing.html#Updating_Documentation)。

1. Fork [十六进制/站点][]
2. 复制存储库到您的电脑并安装依赖项。

   ```shell
   $ git clone https://github.com/<username>/site.git
   $cd site
   $ npm 安装
   ```

3. Create a new yaml file in `source/_data/plugins/`, use your plugin name as the file name

4. Edit `source/_data/plugins/<your-plugin-name>.yml` and add your plugin. 例如：

   ```yaml
   描述：十六进制服务器模块。
   链接：https://github.com/hexojs/hexo-server
   标签：
     - 官方
     - 服务器
     - 控制台
   ```

5. 推送分支。
6. 创建拉请求并描述更改。

[hexo-fs]: https://github.com/hexojs/hexo-fs
[hexo-util]: https://github.com/hexojs/hexo-util
[十六进制]: https://github.com/hexojs/hexo-i18n
[hexo-pagination]: https://github.com/hexojs/hexo-pagination
[十六进制/站点]: https://github.com/hexojs/site
