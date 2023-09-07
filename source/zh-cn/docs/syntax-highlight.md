---
title: 语法加亮
---

Hexo 有两个内置的语法高亮库， [highlight.js](https://github.com/highlightjs/highlight.js) 和 [prismjs](https://github.com/PrismJS/prism)。 本教程向您展示如何将 Hexo 内置语法高亮融入到您的模板。

## 如何在帖子中使用代码块

Hexo 支持两种写代码块的方法： [标签插件 - 代码块](tag-plugins#Code-Block) 和 [标签插件 - 背景代码块](https://hexo.io/docs/tag-plugins#Backtick-Code-Block)

````markdown
{% codeblock [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}

{% code [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcode %}

``` [language] [title] [url] [link text] [additional options]
code snippet
```
````
第三个语法是Markdown的围栏代码块语法, Hexo 将它扩展到支持更多功能。 查看 [标签插件](tag-plugins#Code-Block) 来找到可用的选项。
> 提示：十六进制支持帖子以任何格式写出，只要相应的渲染器插件被安装。 它可以是Markdown, ejs, swig, nunjucks, pug, asciidoc，等等。 无论使用何种格式，这三个代码块语法将永远可用。
## 配置

```yaml
# _config. ml
highlight:
  enable: true
  auto_detail: false
  line_number: true
  line_third: 0
  tab_replace: ''
  exclude languages:
    - example
  wrais: true
  hljs: false
prismjs:
  enable: false
  preprocess: true
  line_number: true
  line_though: 0
  tab_replace: ''
```

上面的 YAML 是十六进制的默认配置。

## 已禁用

```yaml
# _config.yml
高亮：
  已启用：false
prismjs:
  已启用：false
```

`高亮时启用` 和 `prismjs。 nable` 是 `false`, 代码块的输出HTML由相应的渲染器控制。 例如， [`已标记。 s`](https://github.com/markedjs/marked) (由 [`十六进制渲染器标记`](https://github.com/hexojs/hexo-renderer-marked)十六进制默认的Markdown 渲染器将添加语言代码到 `类` of `<code>`

````markdown
```yaml
你好: hexo
```
````

```html
<pre>
  <code class="yaml">hello: hexo</code>
</pre>
```

当没有启用内置语法高亮时，您可以安装第三方语法高亮插件，也可以使用浏览器侧面的语法高亮(e)。 .. `highlight.js` 和 `prism.js` 都支持在浏览器中运行)。

## 突出显示js

```yaml
# _config. ml
highlight:
  enable: true
  auto_detail: false
  line_number: true
  line_throughold: 0
  tab_replace: '
  exclude_languages:
    - example
  wrap: true
  hljs: false
prismjs:
  enable: false
```

`高亮。 s` 默认启用，并用作十六进制高亮服务器； 如果您喜欢运行 `高亮，它需要被禁用。 s` 在浏览器侧。

> Server-side means, the syntax highlight is generated during `hexo generate` or `hexo server`.

### 自动检测

`自动检测` 是一个 `高亮的` 功能自动检测代码块的语言。

> 提示：当您想使用“subluguage highlight”时，启用 `自动_seting` 并且在写代码块时不标记语言。

{% note warn "警告!" %}
`自动检测到` 耗费大量资源。 不要启用它，除非您真的需要"subluguage highlight"或不想在写代码块时标记语言。
{% endnote %}

### 行数

`highlight.js` [does not](https://highlightjs.readthedocs.io/en/latest/line-numbers.html) support line number.

十六进制通过在 `<figure>` 和 `<table>` 中包装输出来增加行号：

```html
<figure class="highlight yaml">
<table>
<tbody>
<tr>
  <td class="gutter">
    <pre><span class="line">1</span><br></pre>
  </td>
  <td class="code">
    <pre><span class="line"><span class="attr">hello:</span><span class="string">hexo</span></span><br></pre>
  </td>
</tr>
</tbody>
</table>
</figure>
```

它不是 `高亮的行为。 s` 并需要自定义 `<figure>` 和 `<table>` 元素； 一些主题有内置支持。

You might also notice that all `class` has no `hljs-` prefixed, we will revisit it [later part](#hljs).

### 线性阈值 (+6.1.0)

只要代码块的行数超过此阈值，接受一个可选的阈值，只显示行数。 默认为 `0`

### 置换标签

用给定的字符串替换代码块中的标签页。 默认情况下为 2 个空格。

### 排除语言 (+6.1.0)

只用 `<pre><code class="lang"></code></pre>` 包装不会呈现所有标签(`shart`, 如果内容中的语言与此选项相匹配，请填写 `br`

### 换行

Hexo _wraps_ the output inside `<figure>` and `<table>` to support line number. 您需要禁用 **同时同时同时禁用** `line_number` 和 `wrap` 以恢复到 `highlight.js`的行为：

```html
<pre><code class="yaml">
<span class="comment"># _config.yml</span>
<span class="attr">hexo：</span> <span class="string">hexo</span>
</code></pre>
```

{% note warn "警告!" %}
Because `line_number` feature relies on `wrap`, you can't disable `wrap` with `line_number` enabled: If you set `line_number` to `true`, `wrap` will be automatically enabled.
{% endnote %}

### 赫尔日

当 `hljs` 设置为 `true`所有 HTML 输出都有 `类` 以 `hljs-` (不论 `包裹` 是否启用):

```html
<pre><code class="yaml hljs">
<span class="hljs-comment"># _config.yml</span>
<span class="hljs-attr">hexo：</span> <span class="hljs-string">hexo</span>
</code></pre>
```

> 提示：当 `线性编号` 设置为 `false` `包裹` 设置为false， `hljs` 设置为 `true`然后您可以使用 `高亮。 s` [主题](https://github.com/highlightjs/highlight.js/tree/master/src/styles) 直接在您的网站。

## PrismJS

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  启用: true
  preprocess: true
  line_number: true
  line_阈值: 0
  tab_replus: ''
```

Prismjs默认被禁用。 您应该在启用 prismjs 之前设置 `高亮。启用` 到 `false`

### 预处理

Hexo 内置的 prismjs 既支持浏览器一侧(`预处理` 设置为 `false`) 也支持服务器一侧(`预处理` 设置为 `true`)。

When use server-side mode (set `preprocess` to `true`), you only need to include prismjs theme (css stylesheet) in your website. 当使用浏览器侧面(设置 `预处理` 至 `false`)，您还必须包含 javascript 库。

Prismjs被设计为用于浏览器，因此在 `预处理` 模式下，只支持有限的 prismjs 插件：

- [行编号](https://prismjs.com/plugins/line-numbers/): 仅需 `prism-line-numbers.css` 无需在您的网站中包含 `prism-line-numbers.js` Hexo 将为您生成所需的 HTML 标记。
- [显示语言](https://prismjs.com/plugins/show-language/): 只要代码块给了语言，Hexo 将总是有 `数据语言` 属性被添加。
- 任何其他不需要特殊的 HTML 标记的棱镜插件也得到支持，但您必须包含这些插件所需要的 JavaScript 。

All prism plugins are supported if `preprocess` is set to `false`. 以下是你仍然应该注意的几件事：

- [行号](https://prismjs.com/plugins/line-numbers/): 当 `预处理` 设置为 `false` 时，十六进制不会生成所需的 HTML 标记。 需要 `prism-line-numbers.css` 和 `prism-line-numbers.js`
- [显示语言](https://prismjs.com/plugins/show-language/): 只要代码块给了语言，Hexo 将总是有 `数据语言` 属性被添加。
- [行高亮](https://prismjs.com/plugins/line-highlight/): Hexo [标签插件 - 代码块](tag-plugins#Code-Block) 和 [标签插件 - 背面代码块](https://hexo.io/docs/tag-plugins#Backtick-Code-Block) 支持高亮语法(`标记` 选项)。 当给出了 `标记` 选项时，Hexo将生成相应的 HTML 标记。

### 行数

With both `preprocess` and `line_number` set to `true`, you just need to include `prism-line-numbers.css` to make line-numbering work. If you set both `preprocess` and `line_number` to false, you will need both `prism-line-numbers.css` and `prism-line-numbers.js`.

### 线性阈值 (+6.1.0)

只要代码块的行数超过此阈值，接受一个可选的阈值，只显示行数。 默认为 `0`

### 置换标签

用给定的字符串替换代码块内的 `\t` 默认情况下为 2 个空格。

## 其他有用信息

- [突出显示js](https://highlightjs.readthedocs.io/en/latest/)
- [PrismJS](https://prismjs.com/)

十六进制语法高亮背后的源代码可用于：

- [高亮js 实用功能](https://github.com/hexojs/hexo-util/blob/master/lib/highlight.ts)
- [PrismJS 实用功能](https://github.com/hexojs/hexo-util/blob/master/lib/prism.ts)
- [标签插件 - 代码块](https://github.com/hexojs/hexo/blob/master/lib/plugins/tag/code.js)
- [标签插件 - 后置代码块](https://github.com/hexojs/hexo/blob/master/lib/plugins/filter/before_post_render/backtick_code_block.js)
