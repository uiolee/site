---
title: 主题
---

{% youtube 5ROIU_9dYe4 %}

构建Hexo主题很容易——你只需要创建一个新的文件夹。 要开始使用您的主题，请修改网站 `_config.yml` 中的 `主题` 设置。 主题应具有以下结构：

```plain
.
├── _config.yml
├── languages
├── layout
├── scripts
└── source
```

### \_config.yml

主题配置文件。 与网站的主配置文件不同的是，修改这个文件不需要重新启动服务器。

### 语言

语言文件夹。 更多信息请访问 [国际化 (i18n)](internationalization.html)。

### 布局

布局文件夹。 此文件夹包含主题的模板文件，用于定义您网站的外观。 Hexo 默认提供 [Nunjucks][] 模板引擎 但您可以轻松地安装额外的插件来支持替代引擎，例如 [EJS][], [Haml][], [Jade][], 或 [Pug][] Hexo 基于模板的文件扩展名选择模板引擎 (就像帖子一样)。 例如：

```plain
layout.ejs - 使用 EJS
layout.njk - 使用 Nunjucks
```

更多信息请访问 [模板](templates.html)。

### 脚本

脚本文件夹。 Hexo 将在初始化过程中自动加载此文件夹中的所有JavaScript文件。 欲了解更多信息，见 [插件](plugins.html)。

### 来源

源文件夹。 将您的素材 (例如CSS 和 JavaScript 文件) 放在这里。 Hexo 忽略隐藏文件和文件或文件夹以 `_` (下划线)。

Hexo 将处理所有可渲染的文件并保存到 `公共` 文件夹。 不可渲染的文件将直接复制到 `公共` 文件夹。

### 发布

当你完成构建你的主题时，你可以发布到 [主题列表](/themes) 在这样做之前，您应该运行 [主题单元测试](https://github.com/hexojs/hexo-theme-unit-test) ，以确保所有的操作都正常。 The steps for publishing a theme are very similar to those for [updating documentation](contributing.html#Updating_Documentation).

1. Fork [十六进制/站点][]
2. 复制存储库到您的电脑并安装依赖项。

   ```shell
   $ git clone https://github.com/<username>/site.git
   $cd site
   $ npm 安装
   ```

3. 在 `source/_data/themes/`中创建一个新的 yaml 文件，使用您的主题名称作为文件名

4. Edit `source/_data/themes/<your-theme-name>.yml` and add your theme. 例如：

   ```yaml
   描述：一个全新的 Hexo 默认主题。
   link: https://github.com/hexojs/hexo-theme-lassive
   preview: http://hexo.io/hexo-theme-language
   tags:
     - official
     - response
     - widgets
     - two_color
     - one_colume
   ```

5. Add a screenshot (with the same name as the theme) to `source/themes/screenshots`. 它必须是 800\*500px PNG。
6. 推送分支。
7. 创建拉请求并描述更改。

[EJS]: https://github.com/hexojs/hexo-renderer-ejs
[Haml]: https://github.com/hexojs/hexo-renderer-haml
[Jade]: https://github.com/hexojs/hexo-renderer-jade
[Pug]: https://github.com/maxknee/hexo-render-pug
[十六进制/站点]: https://github.com/hexojs/site
[Nunjucks]: https://mozilla.github.io/nunjucks/
