---
title: 资源文件夹
---

## 全局资源文件夹

Assets are non-post files in the `source` folder, such as images, CSS or JavaScript files. For instance, If you are only going to have a few images in the Hexo project, then the easiest way is to keep them in a `source/images` directory. 然后你可以使用类似 `的东西访问他们！[](/image.jpg)`

## 发布资源文件夹

{% youtube feIDVQ2tz0o %}

对于期望定期为图像和/或其他资产服务的用户， 对于那些宁愿按每个员额分开资产的人，Hexo也提供了一种更有条理的管理资产的方式。 这略多一些。 但非常方便的资产管理方法可以通过在 `_config中设置 <code>post_asset_folder` 设置。 ml</code> 对。

``` yaml _config.yml
post_asset_folder: true
```

With asset folder management enabled, Hexo will create a folder every time you make a new post with the `hexo new [layout] <title>` command. 此资源文件夹的名称将与帖子关联的 markdown 文件相同。 将与您的帖子相关的所有资产放入关联的文件夹， 并且您将能够使用相对路径引用它们，从而更容易和更方便的工作流程。

## 用于相对路径引用的标签插件

使用普通Markdown 语法和相对路径引用图像或其他资产可能导致在存档或索引页面显示错误。 社区已经创建插件来解决这个问题在 Hexo 2 中。 然而，随着Hexo 3的发布，核心添加了几个新的 [标签插件](/docs/tag-plugins#Include-Assets)。 这使您能够更容易地在帖子中引用您的资产：

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

For example, with post asset folders enabled, if you place an image `example.jpg` into your asset folder, it will *not* appear on the index page if you reference it using a relative path with regular `![](example.jpg)` markdown syntax (however, it will work as expected in the post itself).

因此引用图像的正确方式将是使用标签插件语法而不是标记：

```
{% asset_img example.jpg This is an example image %}
{% asset_img "spaced asset.jpg" "spaced title" %}
```

这样，图像将出现在帖子以及索引和归档页面中。

## 使用 markdown 嵌入图像

[hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked) 3.1.0 introduced a new option that allows you to embed an image in markdown without using `asset_img` tag plugin.

要启用：

``` yml _config.yml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

一旦启用，资产图像将自动解析到其相应的帖子路径。 例如，"image.jpg"位于"/2020/01/02/food/image.jpg"，意思是一个资产图像为 "/2020/01/02/food/" 帖子， `![](图像)。 pg)` 将以 `<img src="/2020/01/02/foo/image.jpg">` 格式呈现。
