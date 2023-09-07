---
title: 贡献中
---

我们欢迎你参加六日的发展。 🤗

## 贸易和发展会议

我们欢迎你参加六日的发展。 此文档将帮助您完成该进程。

### 开始前

请先读取 [贡献者的行为守则](https://github.com/hexojs/hexo/blob/master/CODE_OF_CONDUCT.md)

请遵循编码风格：

- 关注 [Google JavaScript 样式指南](https://google.github.io/styleguide/jsguide.html)
- 使用两个空格缩进的软标签。
- 不要先放置逗号。

而且，Hexo 有自己的 [ESLint 配置](https://github.com/hexojs/eslint-config-hexo)，所以请确保您的贡献将使ESLint 很高兴。

### 工作流

1. Fork [hexojs/hexo][].
2. 复制存储库到您的电脑并安装依赖项。

``` bash
$ git clone https://github.com/<username>/hexo.git
$ cd hexo
$ npm install
$ git submodule update --init
```

3. 创建一个功能分支。

``` bash
$ git 结帐-b new_feature
```

4. 开始黑客。
5. 推送分支：

```
$git 推送源新功能
```

6. 创建拉请求并描述更改。

### 通知

- 请不要修改 `package.json` 中的版本号。
- 您的拉取请求只有在测试通过时才会被合并。 不要忘记在提交前运行测试。

``` bash
$npm 测试
```

## 正在更新官方插件

另外，我们也欢迎PR 或 [官方插件](https://github.com/hexojs)。 🤗

## 正在更新文档

Hexo 文档是开源的，您可以在 [十六进制/站点][] 中找到源代码。

### 工作流

1. Fork [十六进制/站点][]
2. 复制存储库到您的电脑并安装依赖项。

``` bash
$ npm install hexo-cli -g # If you don't have hexo-cli installed
$ git clone https://github.com/<username>/site.git
$ cd site
$ npm install
```

3. 开始编辑文档。 您可以启动服务器进行实时预览。

``` bash
$ 十六进制服务器
```

4. 推送分支。
5. 创建拉请求并描述更改。

### 正在翻译

1. Add a new language folder in `source` folder. (所有小写)
2. Copy Markdown and template files in `source` folder to the new language folder.
3. 将新语言添加到 `source/_data/language.yml`
4. 用 `themes/navy/languages` 复制 `en.yml` 并重命名为语言名称(所有小写)。

## 报告问题

When you encounter some problems when using Hexo, you can find the solutions in [Troubleshooting](troubleshooting.html) or ask me on [GitHub](https://github.com/hexojs/hexo/issues) or [Google Group](https://groups.google.com/group/hexo). 如果您找不到答案, 请在 GitHub 上报告。

1. Represent the problem in [debug mode](commands.html#Debug_mode).
2. 按照问题模板的步骤，在GitHub 上提交新问题时提供调试信息和版本。

[hexojs/hexo]: https://github.com/hexojs/hexo
[十六进制/站点]: https://github.com/hexojs/site
