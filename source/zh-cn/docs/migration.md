---
title: 移 民
---

## RSS

首先，安装 `十六进制迁移器-rss` 插件。

``` bash
$ npm install hexo-migrator-rss --save
```

一旦插件安装完毕，运行下面的命令从RSS迁移所有帖子。 `源` 可以是一个文件路径或 URL。

``` bash
美元十六进制迁移rss <source>
```

## 杰基尔

将Jekyll `_posts` 文件夹中的所有文件移动到 `source/_posts` 文件夹。

修改 `_config.yml` 中的 `新的 post_name` 设置：

``` yaml
new_post_name: :ye:month-:day:title.md
```

## 偶像

Move all files in the Octopress `source/_posts` folder to `source/_posts`

修改 `_config.yml` 中的 `新的 post_name` 设置：

``` yaml
new_post_name: :ye:month-:day:title.md
```

## WordPress

首先，安装 `十六进制迁移器-wordpress` 插件。

``` bash
$ npm install hexo-migrator-wordpress --save
```

导出您的 WordPress 网站到WordPress 控制面板中的“工具” -> “导出” -> “WordPress” (详情请参阅 [WordPress 支持页面](http://en.support.wordpress.com/export/))。

正在运行：

``` bash
美元十六进制迁移wordpress <source>
```

`源` 是到 WordPress 导出文件的文件路径或 URL。

## Joomla

首先，安装 `十六进制迁移-joomla` 插件。

```bash
$ npm install hexo-migrator-joomla --save
```

使用 [J2XML](http://extensions.joomla.org/extensions/migration-a-conversion/data-import-a-export/12816?qh=YToxOntpOjA7czo1OiJqMnhtbCI7fQ%3D%3D) 组件导出您的 Joomla 文章。

正在运行：

```bash
$ hexo migrate joomla <source>
```

`源` 是文件路径或 URL 到 Joomla 导出文件。
