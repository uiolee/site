---
title: 命令
---

## init

``` bash
美元十六进制 [folder]
```

初始化一个网站。 如果没有提供 `文件夹` ，Hexo 将在当前目录中设置一个网站。

此命令是一个运行以下步骤的快捷方式：

1. Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) includes [hexo-theme-scription](https://github.com/hexojs/hexo-theme-landscape) into current 目录或目标文件夹，如果指定的话。
2. 使用软件包管理器安装依赖关系: [Yarn 1](https://classic.yarnpkg.com/lang/en/) [pnpm](https://pnpm.js.org) 或 [npm](https://docs.npmjs.com/cli/install), 以安装者为准； 如果有多个安装，优先级将列在列表中。 npm 默认与 [Node.js](/docs/#Install-Node-js) 捆绑。

## 新的

``` bash
美元新增 [layout] <title>
```

创建新文章 If no `layout` is provided, Hexo will use the `default_layout` from [_config.yml](configuration.html). Use the layout `draft` to create a draft. 如果 `标题` 包含空格，用引号环绕它。

| 选项                | 描述                  |
| ----------------- | ------------------- |
| `-p`, `--path`    | 后期路径。 自定义帖子路径。      |
| `-r`, `--replace` | 如果存在的话替换当前帖子。       |
| `-s`, `--slug`    | 发布slug。 自定义帖子的 URL。 |

默认情况下，Hexo 将使用标题来定义文件的路径。 对于页面来说，它将创建一个该名称的目录和其中的 `index.md` 文件。 使用 `--path` 选项来覆盖该行为并定义文件路径：

```bash
十六进制新页面 --path about/me "关于我"
```

将创建 `源代码/about/me.md` 文件，标题“关于我” 设置在前端。

请注意标题是强制性的。 例如，这不会导致您可能期望的行为：

```bash
十六进制新页面 --path about/me
```

will create the post `source/_posts/about/me.md` with the title "page" in the front matter. 这是因为只有一个参数(`页`)，而默认的布局是 `帖子`。

## 生成

``` bash
$ 十六进制生成
```

生成静态文件。

| 选项                    | 描述                    |
| --------------------- | --------------------- |
| `-d`, `--deplement`   | 生成完成后部署               |
| `-w`, `--watch`       | 监视文件更改                |
| `-b`, `--bail`        | 在生成过程中抛出任何未处理异常时出现错误  |
| `-f`, `--force`       | 强制重新生成                |
| `-c`, `--concurrency` | 要同时生成的文件的最大数量。 默认是无限的 |

## 发布

``` bash
$十六进制发布 [layout] <filename>
```

发布草稿。

## 服务器

``` bash
$ 十六进制服务器
```

启动本地服务器。 By default, this is at `http://localhost:4000/`.

| 选项               | 描述                            |
| ---------------- | ----------------------------- |
| `-p`, `--端口`     | 覆盖默认端口                        |
| `-s`, `--static` | 仅用于静态文件                       |
| `-l`, `--log`    | 启用日志。 Override logger format. |

## 部署

``` bash
$十六进制部署
```

部署您的网站。

| 选项                 | 描述     |
| ------------------ | ------ |
| `-g`, `--generate` | 在部署前生成 |

## 渲染

``` bash
$ hexo render <file1> [file2] ...
```

渲染文件。

| 选项               | 描述   |
| ---------------- | ---- |
| `-o`, `--output` | 输出目标 |

## 迁移

``` bash
美元十六进制迁移 <type>
```

[从其它博客系统迁移了](migration.html) 内容。

## 清理

``` bash
美元十六进制清理
```

清除缓存文件 (`db.json`并生成文件 (`public`).

## 邮件列表

``` bash
美元十六进制列表 <type>
```

列出所有路线。

## 版本

``` bash
$ 十六进制版本
```

显示版本信息。

## 备选方案

### 安全模式

``` bash
$ hexo --safe
```

禁用加载插件和脚本。 如果您在安装新插件后遇到问题，请尝试此操作。

### 调试模式

``` bash
$ hexo --debug
```

Logs verbose messages to the terminal and to `debug.log`. 如果你遇到了任何问题，请尝试使用 Hexo If you see errors, please [raise a GitHub issue](https://github.com/hexojs/hexo/issues/new).

### 静音模式

``` bash
$ 十六进制--静音
```

静音输出到终端。

### 自定义配置文件路径

``` bash
$ hexo --config custom.yml
```

使用自定义配置文件(而不是 `_config.yml`)。 还接受一个 JSON 或 YAML 配置文件的逗号分隔列表 (无空格) 将文件合并为单个的 `_multiconfig.yml`。

``` bash
$ hexo --config custom.yml,custom2.json
```

### 显示草稿

``` bash
$ 十六进制--draft
```

显示草稿帖子(存储在 `source/_draft` 文件夹中)。

### 自定义 CWD

``` bash
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录的路径。
