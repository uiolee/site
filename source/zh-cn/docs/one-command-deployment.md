---
title: 单命令部署
---

Hexo提供了一个快速和简便的部署战略。 你只需要一个命令才能将你的网站部署到你的服务器。

```bash
$十六进制部署
```

安装与服务器/仓库提供的部署方法兼容的必要插件。

部署通常通过 **\_config.yml** 进行配置。 有效的配置必须有 `类型` 字段。 例如：

```yaml
部署:
  类型: git
```

您可以使用多个部署器。 Hexo 将按顺序执行每个部署器。

```yaml
部署：
- 类型：git
  仓库：
- 类型：英雄
  仓库：
```

请参阅 [插件](https://hexo.io/plugins/) 列表以获取更多部署插件。

## Git

1. 安装 [十六进制部署器][]

```bash
$ npm 安装十六进制部署器-git --save
```

2. 编辑 **\_config.yml** (下面显示的示例值作为评论)：

```yaml
部署:
  类型: git
  repo: <repository url> # https://bitbucket.org/JohnSmith/johnsmith.bitbucket.io
  分支: [branch]
  消息: [message]
```

| 选项     | 描述                                   | 默认设置                                                                                |
| ------ | ------------------------------------ | ----------------------------------------------------------------------------------- |
| `repo` | 目标存储库的 URL                           |                                                                                     |
| `分支`   | 分支名称。                                | `gh-pages` (GitHub)<br>`coding-pages` (Coding.net)<br>`master` (others) |
| `留言`   | 自定义提交消息。                             | `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`               |
| `令牌`   | 使用仓库进行身份验证的可选代币值。 前缀 `$` 读取环境变量令牌的前缀 |                                                                                     |

3. 部署您的网站 `净化 && 十六进制部署`

  - 您将会被使用目标仓库的用户名和密码提示, 除非您使用令牌或ssh键进行身份验证。
  - 十六进制部署器不存储您的用户名和密码。 Use [git-credential-cache](https://git-scm.com/docs/git-credential-cache) to store them temporarily.

4. 导航到您的资源库设置，然后将“页面”分支更改为 `gh-pages` (或在您的配置中指定的分支)。 所部署的站点应该在"页面"设置显示的链接上实用。

## Heroku

Install [hexo-deployer-heroku][].

```bash
$ npm installing hexo-depuer-hartuku --save
```

编辑设置。

```yaml
部署:
  类型: 英雄的
  仓库: <repository url>
  消息: [message]
```

| 选项            | 描述                                                                                                          |
| ------------- | ----------------------------------------------------------------------------------------------------------- |
| `repo`, `存储库` | Heroku 仓库 URL                                                                                               |
| `留言`          | Customize commit message (Default to `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`) |

## 网络化

[Netlife](https://www.netlify.com/) 提供了持续的部署 (Git-触发的构建)、一个智能的全球CDN、完整的DNS (包括自定义域)、自动的 HTTPS、资产加速等等。 这是一个统一的平台，用于自动创建高性能，易于维护的网站和网站应用程序。

在Netlife上部署您的站点有两种不同的方式。 最常见的方式是使用 web UI 。 访问 [创建一个新的站点页面](https://app.netlify.com/start), 从GitHub 、 GitLab或 Bitbucket 选择您的项目仓库, 然后跟随提示。

或者，您可以使用Netlify的 [基于节点的 CLI](https://www.netlify.com/docs/cli/) 工具来管理和部署Netlify上的站点，而无需离开您的终端。

您也可以在您的README中添加一个 [部署到 Netlife 按钮](https://www.netlify.com/docs/deploy-button/) 。 文件允许他人创建你的仓库副本，并通过一次点击部署到Netlify。

## 同步。

Install [hexo-deployer-rsync][].

```bash
$ npm 安装十六进制部署-rsync --sync
```

编辑设置。

```yaml
部署:
  类型: rsync
  主机: <host>
  用户: <user>
  root: <root>
  端口: [port]
  删除: [true|false]
  详细: [true|false]
  忽略错误: [true|false]
```

| 选项        | 描述          | 默认设置  |
| --------- | ----------- | ----- |
| `主机`      | 远程主机地址      |       |
| `用户`      | 用户名         |       |
| `根目录`     | 远程主机的根目录    |       |
| `端口`      | 端口          | 22    |
| `删除`      | 删除远程主机上的旧文件 | true  |
| `verbose` | 显示详细消息      | true  |
| `忽略错误`    | 忽略错误        | false |

## 打开 Shift

安装 [十六进制部署-openshift][]

```bash
$ npm 安装十六进制部署-openshift --save
```

编辑设置。

```yaml
部署:
  类型: openshift
  仓库: <repository url>
  消息: [message]
```

| 选项     | 描述                                                                                                          |
| ------ | ----------------------------------------------------------------------------------------------------------- |
| `repo` | OpenShift 仓库 URL                                                                                            |
| `留言`   | Customize commit message (Default to `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`) |

## FTPSync

安装 [十六进制部署-ftsync][]

```bash
$ npm 安装十六进制部署器-ftsync --save
```

编辑设置。

```yaml
部署:
  类型: ftsync
  主机: <host>
  用户: <user>
  密码: <password>
  远程: [remote]
  端口: [port]
  忽略: [ignore]
  连接: [connections]
  详细: [true|false]
```

| 选项        | 描述         | 默认设置  |
| --------- | ---------- | ----- |
| `主机`      | 远程主机地址     |       |
| `用户`      | 用户名        |       |
| `通过`      | 密码         |       |
| `远程`      | 远程主机的根目录   | `/`   |
| `端口`      | 端口         | 21    |
| `忽略`      | 忽略主机或远程的文件 |       |
| `连接`      | 连接数        | 1     |
| `verbose` | 显示详细消息     | false |

## SFTP

安装 [十六进制部署者sftp][] 通过 SFTP 部署站点，允许使用 ssh-agent 连接无密码。

```bash
$ npm 安装十六进制部署者sftp --save
```

编辑设置。

```yaml
部署:
  类型: sftp
  主机: <host>
  用户: <user>
  密码: <password>
  远程路径: [远程路径]
  port: [port]
  私钥: [path/to/privateKey]
  密码: [passphrase]
  代理: [path/to/agent/socket]
```

| 选项     | 描述                 | 默认设置             |
| ------ | ------------------ | ---------------- |
| `主机`   | 远程主机地址             |                  |
| `端口`   | 端口                 | 22               |
| `用户`   | 用户名                |                  |
| `通过`   | 密码                 |                  |
| `私钥`   | Sh 私钥路径            |                  |
| `口令`   | 私钥可选密码             |                  |
| `代理`   | Ssh-agent 套接字路径    | `$SSH_AUTH_SOCK` |
| `遥控路径` | 远程主机的根目录           | `/`              |
| `强制上传` | 覆盖现有文件             | false            |
| `同义词`  | 同时处理的 SFTP 任务的最大数量 | 100              |

## Vercel

[Vercel](https://vercel.com) 是一个云平台，使开发人员能够托管即时部署的 Jamstack 网站和网络服务。 自动缩放，无需监督，所有配置都为零。 他们提供了一个全局边缘网络，SSL加密，资产压缩，缓存无效等等。

第 1 步：将构建脚本添加到您的 `package.json` 文件：

```json
{
  "scripts": {
    "build": "hexo generate"
  }
}
```

步骤 2: 部署你的 Hexo 网站到Vercel

To deploy your Hexo app with a [Vercel for Git Integration](https://vercel.com/docs/git-integrations), make sure it has been pushed to a Git repository.

使用 [导入流程](https://vercel.com/import/git) 导入项目到Vercel。 During the import, you will find all relevant options preconfigured for you; however, you can choose to change any of these options, a list of which can be found [here](https://vercel.com/docs/build-step#build-&-development-settings).

After your project has been imported, all subsequent pushes to branches will generate [Preview Deployments](https://vercel.com/docs/platform/deployments#preview), and all changes made to the [Production Branch](https://vercel.com/docs/git-integrations#production-branch) (commonly "main") will result in a [Production Deployment](https://vercel.com/docs/platform/deployments#production).

或者，您可以点击下面的部署按钮来创建一个新项目：

[![部署Vercel](https://vercel.com/button)](https://vercel.com/new/hexo)

## 偏移量

[Bip](https://bip.sh) 是一种商业托管服务，它提供零下班时间部署、全局CDN、SSL、无限制带宽以及更多静态网站。 计划可以随时随地收取，按领域收取费用。

启动是快速而简便的，因为Bip 提供了十六进制的盒子支持。 This guide assumes you already have [a Bip domain and Bip CLI installed](https://bip.sh/getstarted).

1： 初始化您的项目目录

```bash
$ bip init
```

跟随提示, 你会被问及你想要部署到哪个域。 Bip 将检测到您正在使用 Hexo, 并将工程设置为源文件目录。

2： 部署您的网站

```bash
$ 十六进制生成 - 部署 && bip 部署
```

几分钟后，您的网站将被部署。

## RSS3

[RSS3](https://rss3.io) 是一个为Web 3.0 时代的内容和社交网络设计的开放协议。

1. 安装 [十六进制部署-rss3][]

2. 修改配置。

  ``` yaml
  deploy: # The root configuration block for all deployers
  - type: rss3
    endpoint: https://hub.rss3.io
    privateKey: 47e18d6c386898b424025cd9db446f779ef24ad33a26c499c87bb3d9372540ba
    ipfs:
      deploy: true
      gateway: pinata
      api:
        key: d693df715d3631e489d6
        secret: ee8b74626f12b61c1a4bde3b8c331ad390567c86ba779c9b18561ee92c1cbff0
  ```

| 参数                | 描述               |
| ----------------- | ---------------- |
| `endpoint`        | 连接RSS3 Hub       |
| `私钥`              | 您的私钥64字节         |
| `ipf/部署`          | 是否部署到 IPFS       |
| `ipfs/gateway`    | IPFS API gateway |
| `ipfs/api/key`    | IPFS 网关相关身份验证内容  |
| `ipfs/api/secret` | IPFS 网关相关身份验证内容  |

3. 生成静态文件

4. 部署

出于与部署有关的考虑，您可以参阅 [我们的文档](https://github.com/NaturalSelectionLabs/hexo-deployer-rss3/blob/develop/README.md)

## Edgio (原Layer0)

[Edgio (原为Layer0)](https://docs.edg.io) 是一个互联网规模的平台，使团队更容易构建， 释放、保护和加速他们的 web 应用程序和API。

1. 在你的十六进制项目目录中，安装Edgio CLI：

```bash
npm i -g @edgio/cli
```

2. 通过 Edgio安装 Hexo 连接器：

```bash
edgio init --connector=@edgio/hexo
```

3. 部署

```bash
编辑已部署
```

或者，您可以点击下面的部署按钮来创建一个新项目：

[![部署到编辑](https://docs.edg.io/button.svg)](https://app.layer0.co/deploy?repo=https%3A%2F%2Fgithub.com%2Fedgio-docs%2Fedgio-hexo-example)

## 其他方法

所有生成的文件都保存在 `公共` 文件夹中。 你可以将它们复制到你喜欢的任何地方。

[十六进制部署器]: https://github.com/hexojs/hexo-deployer-git
[hexo-deployer-heroku]: https://github.com/hexojs/hexo-deployer-heroku
[hexo-deployer-rsync]: https://github.com/hexojs/hexo-deployer-rsync
[十六进制部署-openshift]: https://github.com/hexojs/hexo-deployer-openshift
[十六进制部署-ftsync]: https://github.com/hexojs/hexo-deployer-ftpsync
[十六进制部署者sftp]: https://github.com/lucascaro/hexo-deployer-sftp
[十六进制部署-rss3]: https://github.com/NaturalSelectionLabs/hexo-deployer-rss3
