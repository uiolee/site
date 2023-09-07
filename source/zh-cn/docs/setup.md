---
title: 设置
---

{% youtube 0m2HnATkHOk %}

Hexo安装完毕后，运行以下命令来初始化目标 `<folder>`

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

一旦启动，您的项目文件夹将是什么样子：

``` plain
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### yml

站点 [配置](configuration.html) 文件。 您可以在这里配置大部分设置。

### json

应用程序数据。 [EJS](https://ejs.co/), [Stylus](http://learnboost.github.io/stylus/) 和 [Markdown](http://daringfireball.net/projects/markdown/) 渲染器是默认安装的。 如果你想要，你可以稍后卸载它们。

``` json package.json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependencies": {
    "hexo": "^3.8.0",
    "hexo-generator-archive": "^0.1.5",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3.1",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-renderer-marked": "^0.3.2",
    "hexo-server": "^0.3.3"
  }
}
```

### 卡福尔德

[Scaffold](writing.html#Scaffolds) 文件夹。 当你创建一个新帖子时，Hexo会把新的文件建立在架子上。

### 来源

源文件夹。 这是您放置网站内容的地方。 Hexo 忽略了隐藏文件和文件或文件夹，其名称前缀为 `_` (下划线) - 但 `_post` 文件夹除外。 可渲染文件 (例如Markdown, HTML) 将被处理并放入 `公开的` 文件夹，而其他文件将只是被复制的。

### 主题

[主题](themes.html) 文件夹。 Hexo 通过将网站内容与主题结合起来生成一个静态网站。
