---
title: 指令
---

## init

``` bash
美元十六进制 [folder]
```

新建一个网站。 如果没有设置 `folder` ，Hexo 默认在目前的文件夹建立网站。

本命令相当于执行了以下几步：

1. Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) 和 [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape) 主题到当前目录或指定目录。
2. 使用 [Yarn 1](https://classic.yarnpkg.com/lang/en/)、[pnpm](https://pnpm.js.org) 或 [npm](https://docs.npmjs.com/cli/install) 包管理器下载依赖（如有已安装多个，则列在前面的优先）。 npm 默认随 [Node.js](/docs/#Install-Node-js) 安装。

## 新的

``` bash
美元新增 [layout] <title>
```

新建一篇文章。 如果没有设置 `layout` 的话，默认使用 [_config.yml](configuration.html) 中的 `default_layout` 参数代替。 Use the layout `draft` to create a draft. 如果标题包含空格的话，请使用引号括起来。

| 选项                | 描述                  |
| ----------------- | ------------------- |
| `-p`, `--path`    | 后期路径。 自定义新文章的路径     |
| `-r`, `--replace` | 如果存在的话替换当前帖子。       |
| `-s`, `--slug`    | 发布slug。 自定义帖子的 URL。 |

默认情况下，Hexo 会使用文章的标题来决定文章文件的路径。 对于独立页面来说，Hexo 会创建一个以标题为名字的目录，并在目录中放置一个 `index.md` 文件。 你可以使用 `--path` 参数来覆盖上述行为、自行决定文件的目录：

```bash
十六进制新页面 --path about/me "关于我"
```

以上命令会创建一个 `source/about/me.md` 文件，同时 Front Matter 中的 title 为 `"About me"`

注意！ title 是必须指定的！ 例如，这不会导致您可能期望的行为：

```bash
十六进制新页面 --path about/me
```

此时 Hexo 会创建 `source/_posts/about/me.md`，同时 `me.md` 的 Front Matter 中的 title 为 `"page"`。 这是因为在上述命令中，hexo-cli 将 `page` 视为指定文章的标题、并采用默认的 `layout`。

## 生成

``` bash
$ 十六进制生成
```

生成静态文件。

| 选项                    | 描述                       |
| --------------------- | ------------------------ |
| `-d`, `--deplement`   | 生成完成后部署                  |
| `-w`, `--watch`       | 监视文件变动                   |
| `-b`, `--bail`        | 生成过程中如果发生任何未处理的异常则抛出异常   |
| `-f`, `--force`       | 强制重新生成                   |
| `-c`, `--concurrency` | 最大同时生成文件的数量，默认无限制 默认是无限的 |

## 发布

``` bash
$十六进制发布 [layout] <filename>
```

发表草稿。

## 服务器

``` bash
$ 十六进制服务器
```

启动服务器。 默认情况下，访问网址为： `http://localhost:4000/`。

| 选项               | 描述                            |
| ---------------- | ----------------------------- |
| `-p`, `--端口`     | 重设端口                          |
| `-s`, `--static` | 只使用静态文件                       |
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

从其他博客系统 [迁移内容](migration.html)。

## 清理

``` bash
美元十六进制清理
```

清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)。

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

## 选项

### 安全模式

``` bash
$ hexo --safe
```

在安全模式下，不会载入插件和脚本。 当您在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

### 调试模式

``` bash
$ hexo --debug
```

在终端中显示调试信息并记录到 `debug.log`。 如果你遇到了任何问题，请尝试使用 Hexo 当您碰到问题时，可以尝试用调试模式重新执行一次，并 [提交调试信息到 GitHub](https://github.com/hexojs/hexo/issues/new)。

### 简洁模式

``` bash
$ 十六进制--静音
```

静音输出到终端。

### 自定义配置文件的路径

``` bash
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml 和 custom2.json，其中 custom2.json 优先级更高
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

自定义配置文件的路径，指定这个参数后将不再使用默认的 `_config.yml`。 还接受一个 JSON 或 YAML 配置文件的逗号分隔列表 (无空格) 将文件合并为单个的 `_multiconfig.yml`。

``` bash
# 使用 custom.yml 代替默认的 _config.yml
$ hexo server --config custom.yml

# 使用 custom.yml, custom2.json 和 custom3.yml，其中 custom3.yml 优先级最高，其次是 custom2.json
$ hexo generate --config custom.yml,custom2.json,custom3.yml
```

### 显示草稿

``` bash
$ 十六进制--draft
```

显示 `source/_drafts` 文件夹中的草稿文章。

### 自定义 CWD

``` bash
$ hexo --cwd /path/to/cwd
```

自定义当前工作目录（Current working directory）的路径。
