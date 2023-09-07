---
title: 故障排除
---

如果您在使用 Hexo 时遇到问题，这里列出了一些常见问题的解决方法。 If this page doesn't help you solve your problem, try doing a search on [GitHub](https://github.com/hexojs/hexo/issues) or our [Google Group](https://groups.google.com/group/hexo).

## YAML Parsing Error

``` plain
JS-YAML: 不完全的显式映射对映射；在第 18 行，第 29 列错过了一个密钥节点:
      最后更新: 上次更新: %s
```

如果字符串包含冒号则换行符。

``` plain
JS-YAML：映射条目在第 18 行，第 31 列出现错误缩进：
      最后更新："最后更新： %s"
```

请确保您正在使用软标签，在冒号后添加空间。

您可以查看 [YAML Spec](http://www.yaml.org/spec/1.2/spec.html) 获取更多信息。

## 电子邮件错误

``` plain
错误：EMFILE太多打开的文件
```

虽然Node.js没有阻止I/O，但同步I/O的最大数量仍然受到系统限制。 当尝试生成大量文件时，您可能会遇到EMFILE错误。 您可以尝试运行以下命令来增加允许同步的 I/O 操作的数量。

``` bash
$ ulimit -n 10000
```

**错误：无法修改限制**

如果您遇到以下错误：

``` bash
$ ulimit - n 10000
ulimit: 打开文件: 不能修改限制: 操作不被允许
```

这意味着一些全系统配置正在阻止 `ulimit` 增加到一定的限制。

重写限制：

1. 在“/etc/security/limits.conf”中添加以下一行：

  ```
  * - 无文件 10000

  # '*' 适用于所有用户，'-' 设置软限制和硬限制
  ```

  * 上述设置在某些情况下可能不适用，请确保“/etc/pam.d/login”和“/etc/pam.d/lightdm”有以下行： (如果文件不存在则忽略此步骤)

  ```
  会话需要 pam_limits.so
  ```

2. 如果您是基于 [系统的](https://en.wikipedia.org/wiki/Systemd#Adoption) 分布，系统可能会覆盖"limits.conf"。 要在系统中设置限制，在“/etc/systemd/system.conf”和“/etc/systemd/user.conf”中添加以下行：

  ```
  DefaultLimitNOFILE=10000
  ```

3. Reboot

## 进程超出内存

当你在生成过程中遇到此错误：

```
FATAL 错误: CALL_AND_RETRY_LAST 配置失败 - 缺失内存
```

Increase Node.js heap memory size by changing the first line of `hexo-cli` (`which hexo` to look for the file).

```
#!/usr/bin/env 节点 --max_old_space_size=8192
```

[生成一个巨型博客 · 问题#1735 · 六边/六边”](https://github.com/hexojs/hexo/issues/1735)

## Git 部署问题

### RPC 失败

``` plain
错误：RPC 失败；结果=22, HTTP 代码 = 403

致命：'username.github.io' 似乎不是 git 资源库
```

请确保您在计算机上正确设置了 [git](https://help.github.com/articles/set-up-git) 或者尝试使用 HTTPS 存储库 URL。

### 错误：ENOENT：没有这样的文件或目录

如果您遇到一个错误，如 `错误：ENOENET：没有这样的文件或目录` 可能是由于在您的标签中混合了大写字母和小写字母。 类别或文件名。 Git 不能自动合并此更改，所以它会中断自动分支。

要解决这个问题，请试试

1. 检查每个标签和类别的大小写，并确保它们是相同的。
1. 提交
1. 清洁和构建: `./node_modules/.bin/hexo clean && /node_modules/.bin/hexo 生成`
1. 手动复制公共文件夹到桌面
1. 将分支从主分支切换到本地部署分支
1. 从桌面复制公共文件夹中的内容到部署分支
1. 提交。 您应该看到您可以手动解决的任何合并冲突。
1. 切换回主分支并正常部署： `./node_modules/.bin/hexo 部署`

## 服务器问题

``` plain
Error: listen EADDRINUSE
```

您可能同时启动了两个十六进制服务器，或者可能有另一个应用程序使用相同的端口。 尝试修改 `端口` 设置或以 `-p` 标志启动Hexo 服务器。

``` bash
$ 十六进制服务器-p 5000
```

## 插件安装问题

``` plain
npm 错误！ node-waf 配置版本
```

这个错误可能发生在尝试安装用C、C++或其他非JavaScript语言写成的插件时。 请确保您已经在计算机上安装了正确的编译器。

## Dtrace 发生错误 (Mac OS X)

```plain
难以找到模块'./build/Release/DtraceProviderBindings'] 代码: 'MODULE_NOT_FOUND' }
build/default/DTraceProviderBindings'] 代码: 'MODULE_NOT_FOUND' }
电子邮件：[错误：找不到模块'./build/Debug/DTraceProviderBindings'] 代码: 'MODULE_NOT_FOUND' }
```

Dtrace 安装可能有问题，请使用：

```sh
$ npm install hexo --no-opulatory
```

查看 [#1326](https://github.com/hexojs/hexo/issues/1326#issuecomment-113871796)

## Jade 或 Swig 上的迭代数据模型

Hexo 使用 [仓库][] 作为其数据模型。 它不是一个数组，所以你可能必须将对象转换成可迭代物。

```
{% for post in site.posts.toArray() %}
{% endfor %}
```

## 数据未更新

有些数据无法更新，或者新生成的文件与上次版本相同。 清理缓存并重试。

``` bash
美元十六进制清理
```

## 没有执行命令

当你不能得到除 `以外的任何命令时，帮助` `init` 和 `版本` 可正常工作，并不断获取 `十六进制帮助`可能是缺少 `十六进制` `软件包引起的。 son`:

```json
{
  "hexo": {
    "version": "3.2.2"
  }
}
```

## 转义内容

Hexo 使用 [Nunjucks][] 来渲染帖子 ([Swig][] 在旧版本中被使用，旧版本具有相似的语法)。 内容包裹为 `{{ }}` 或 `{% %}` 将被解析并可能引起问题。 You can skip the parsing by wrapping it with the [`raw`](/docs/tag-plugins#Raw) tag plugin, single backtick `` `{{ }}` `` or triple backtick. 或者，Nunjucks 标签可以通过渲染器的选项(如果支持的话)， [API](/api/renderer#Disable-Nunjucks-tags) 或 [front-matters](/docs/front-matter) 禁用。

```
{% raw %}
Hello {{ world }}
{% endraw %}
```

````
```
Hello {{ world }}
```
````

## ENOSPC Error (Linux)

有时当运行命令 `$十六进制服务器` 时返回一个错误：

```
错误：监视ENOSPC...
```

It can be fixed by running `$ npm dedupe` or, if that doesn't help, try the following in the Linux console:

```
$ echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

这将增加您可以观看的文件数量。

## EMPERM 错误 (window子系统 for Linux)

当在 BashOnWindows 环境中运行 `$ hexo 服务器` 时，它返回以下错误：

```
错误：监视/path/to/hexo/theme/ EMPERM
```

不幸的是，WSL 目前不支持文件系统监视器。 因此，十六进制服务器的实时更新功能目前不可用。 您仍然可以在WSL环境中运行服务器，先生成文件，然后作为静态服务器运行：

``` sh
$ 十六进制生成
$ 十六进制服务器 -s
```

This is [a known BashOnWindows issue](https://github.com/Microsoft/BashOnWindows/issues/216), and on 15 Aug 2016, the Windows team said they would work on it. You can get progress updates and encourage them to prioritize it on [the issue's UserVoice suggestion page](https://wpdev.uservoice.com/forums/266908-command-prompt-console-bash-on-ubuntu-on-windo/suggestions/13469097-support-for-filesystem-watchers-like-inotify).

## 模板渲染错误

有时当运行 `$ 十六进制生成` 它会返回一个错误：

```
致命的某些错误。 也许你可以在这里找到解决方案: http://hexo.io/docs/troubleshooting.html
模板渲染错误: (未知路径)
```

可能的原因：
- 您的文件中有一些不可识别的单词，例如不可见的零宽字符。
- [标签插件](/docs/tag-plugins) 使用或限制不正确。
  * 带有内容的Block样式标签插件不包含在 `{% endplugin_name %}`
  ```
  # 不正确的
  {% codeblock %}
  fn()
  {% codeblock %}

  # 不正确的
  {% codeblock %}
  fn()

  # 正确的
  {% codeblock %}
  fn()
  {% endcodeblock %}
  ```
  * 在标签插件中有类似于Nunjucks的语法，例如 [`{#`](https://mozilla.github.io/nunjucks/templating.html#comments)。 此示例的一个工作方案是使用 [三重背杆](/docs/tag-plugins#Backtick-Code-Block) [转义内容](/docs/troubleshooting#Escape-Contents) 部分有更多详细信息。
  ```
  {% codeblock lang:bash %}
  数组大小为 ${#ARRAY}
  {% endcodeblock %}
  ```

## YAMLException (Issue [#4917](https://github.com/hexojs/hexo/issues/4917)

Upgrading to `hexo^6.1.0` from an older version may cause the following error when running `$ hexo generate`:

```
YAMLException: 指定的 YAML 类型列表(或单个类型对象) 包含一个非类型对象。
    在...
```

这可能是一个不正确的依赖关系造成的(即)。 `js-yaml`设置无法被软件包管理器自动解决，您可能需要手动更新它：

```sh
$npm 安装js-yaml@最新版本
```
或
```sh
$ yarn 添加 js-yaml@latest
```
如果您使用 `yarn`。

[仓库]: https://github.com/hexojs/warehouse
[Swig]: https://node-swig.github.io/swig-templates/
[Nunjucks]: https://mozilla.github.io/nunjucks/
