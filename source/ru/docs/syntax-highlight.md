---
title: Подсветка синтаксиса
---

Hexo has two built-in syntax highlight libraries, [highlight.js](https://github.com/highlightjs/highlight.js) and [prismjs](https://github.com/PrismJS/prism). Этот учебный материал показывает, как интегрировать встроенную подсветку синтаксиса Hexo в ваш шаблон.

## Как использовать блок кода в сообщениях

Hexo поддерживает два способа записи блока кода: [Модуль Тега - Кодовый блок](tag-plugins#Code-Block) и [Плагин Тега - Блок Backtick Code](https://hexo.io/docs/tag-plugins#Backtick-Code-Block):

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
Третий синтаксис — это защищённый от Markdown код синтаксис и Hexo расширяет его для поддержки большего количества функций. Ознакомьтесь с [Tag Plugin Docs](tag-plugins#Code-Block) , чтобы узнать доступные параметры.
> Совет: Hexo поддерживает сообщения, записанные в любом формате, до тех пор пока установлен соответствующий плагин для визуализации. Это может быть в markdown, ejs, swig, nunjucks, pug, asciidoc. Независимо от используемого формата, эти три блока кода всегда будут доступны.
## Конфигурация

```yaml
# _Конфигурация ml
highlight:
  enable: true
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: ''
  exclude_languages:
    - пример
  wrap: true
  hljs: false
prismjs:
  enable: false
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

Выше YAML является настройкой по умолчанию Hexo.

## Отключено

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  enable: false
```

Когда `highlight.enable` и `prismjs. nable` являются `false`, вывод HTML блока кода управляется соответствующим рендером. For example, [`marked.js`](https://github.com/markedjs/marked) (used by [`hexo-renderer-marked`](https://github.com/hexojs/hexo-renderer-marked), the default markdown renderer of Hexo) will add the language code to the `class` of `<code>`:

````markdown
```yaml
hello: hexo
```
````

```html
<pre>
  <code class="yaml">hello: hexo</code>
</pre>
```

When no built-in syntax highlight is enabled, you can either install third-party syntax-highlight plugin, or use a browser-side syntax hilighter (e.g. `highlight.js` and `prism.js` both support running in browser).

## Подсветка.js

```yaml
# _Конфигурация ml
highlight:
  enable: true
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: ' '
  exclude_languages:
    - пример
  wrap: true
  hljs: false
prismjs:
  enable: false 
 enable: false 

```

`выделение. s` включен по умолчанию и используется в качестве подсветки на стороне сервера в Hexo; он должен быть отключен, если вы предпочитаете запустить подсветку `. s` на стороне браузера.

> Серверные средства, подсветка синтаксиса создается во время `hexo генерировать` или `hexo server`.

### автоопределение

`auto_detect` является функцией `highlight.js` автоматически, которая определяет язык блока кода.

> Подсказка: если вы хотите использовать подсветку "подсветки", включите `auto_detect` и не помечайте язык как блок кода.

{% note warn "Warning!" %}
`auto_detect` очень ресурсоемкий. Не включайте её, если вам не нужен подсветка "подсветка" или не предпочитайте отмечать язык при написании блока кода.
{% endnote %}

### номер строки

`highlight.js` [does not](https://highlightjs.readthedocs.io/en/latest/line-numbers.html) support line number.

Hexo добавляет номер строки путем вывода обертки внутри `<figure>` и `<table>`:

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

Это не поведение подсветки `. s` и требует пользовательский CSS для `<figure>` и `<table>` элементов; некоторые темы имеют встроенную поддержку.

You might also notice that all `class` has no `hljs-` prefixed, we will revisit it [later part](#hljs).

### строка_порог (+6.1.0)

Принимает необязательный порог, чтобы показывать только номера строк, если количество строк блока кода превышает такой порог. По умолчанию `0`.

### таб_замена

Замените вкладки внутри блока кода заданной строкой. По умолчанию это 2 пробела.

### исключать_языки (+6.1.0)

Переносите только `<pre><code class="lang"></code></pre>` и не отразится на всех тегах (`распространяется`, и `br`) в содержимом, если языки соответствуют этой опции.

### обернуть

Hexo _wraps_ the output inside `<figure>` and `<table>` to support line number. You need to disable **both** `line_number` and `wrap` to revert to `highlight.js`'s behavior:

```html
<pre><code class="yaml">
<span class="comment"># _config.yml</span>
<span class="attr">шестнадцатерично:</span> <span class="string">шестнадцатеричное</span>
</code></pre>
```

{% note warn "Warning!" %}
Поскольку функция `line_number` основывается на `обертке`, вы не можете отключить опцию `обвязки` с помощью `line_number` включено: Если вы установите `line_number` на `true`, `перенос` будет автоматически включен.
{% endnote %}

### hljs

When `hljs` is set to `true`, all the HTML output will have `class` prefixed with `hljs-` (regardless `wrap` is enabled or not):

```html
<pre><code class="yaml hljs">
<span class="hljs-comment"># _config.yml</span>
<span class="hljs-attr">шестнадцатерично:</span> <span class="hljs-string">шестнадцатеричное</span>
</code></pre>
```

> Подсказка: когда у `line_number` установлено значение `false`, `перенос` установлен на false, а `hljs` установлен на `true`, Вы можете использовать подсветку `. s` [тема](https://github.com/highlightjs/highlight.js/tree/master/src/styles) прямо на вашем сайте.

## Призма

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  enable: true
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

Prismjs отключён по умолчанию. Перед включением prismjs необходимо установить `highlight.enable` на `false`.

### предпроцесс

Встроенный Hexo prismjs поддерживает обе стороны браузера (`preprocess` set to `false`) и сервер-сторона (`preprocess` set to `true`).

При использовании режима на стороне сервера (установите `preprocess` на `true`вам нужно только включить в ваш сайт тему (css stylesheet). При использовании браузера (установите `preprocess` на `false`), вы также должны включить библиотеку javascript.

Prismjs предназначен для использования в браузере, поэтому в режиме `предварительного процесса` поддерживается только ограниченный плагин prismjs:

- [Line Numbers](https://prismjs.com/plugins/line-numbers/): Требуется только `prism-numbers.css` и не нужно включать `prism-line-numbers.js` на вашем сайте. Hexo сгенерирует необходимый HTML-маркер вверх для вас.
- [Show Languages](https://prismjs.com/plugins/show-language/): В Hexo всегда будет атрибут `data-language` добавлен до тех пор, пока язык задан для кодового блока.
- Любые другие плагины, которым не нужна специальная разметка HTML, также поддерживаются, но необходимо будет включить Javascript для этих плагинов.

Все плагины призмы поддерживаются, если `preprocess` установлен на `false`. Вот несколько вещей, которые вы все еще должны обратить внимание:

- [Line Numbers](https://prismjs.com/plugins/line-numbers/): Hexo не сгенерирует требуемую HTML-отметку, когда `preprocess` установлен в `false`. Требуется `prism-line-numbers.css` и `prism-line-numbers.js`.
- [Show Languages](https://prismjs.com/plugins/show-language/): В Hexo всегда будет атрибут `data-language` добавлен до тех пор, пока язык задан для кодового блока.
- [Line Highlight](https://prismjs.com/plugins/line-highlight/): И Hexo [Tag Plugin - Code Block](tag-plugins#Code-Block) и [Tag Plugin - Backtick Code](https://hexo.io/docs/tag-plugins#Backtick-Code-Block) поддерживает Line Highlight синтаксис (`mark` option). Когда `отметка` указана, Hexo будет генерировать соответствующую разметку HTML.

### номер строки

С заданием `preprocess` и `line_number` в true ``, просто нужно включить номера строк `призмы. ss` для создания нумерации строк. Если вы установите `preprocess` и `line_number` в false, вам понадобятся и `призм-строки.css` и `призм-строки-числа.js`.

### строка_порог (+6.1.0)

Принимает необязательный порог, чтобы показывать только номера строк, если количество строк блока кода превышает такой порог. По умолчанию `0`.

### таб_замена

Заменить блок кода `\t` заданной строкой. По умолчанию это 2 пробела.

## Другая полезная информация

- [Подсветка.js](https://highlightjs.readthedocs.io/en/latest/)
- [Призма](https://prismjs.com/)

Исходные коды подсветки синтаксиса Hexo доступны в:

- [Подсветка функций утилиты js](https://github.com/hexojs/hexo-util/blob/master/lib/highlight.ts)
- [Функции утилиты PrismJS](https://github.com/hexojs/hexo-util/blob/master/lib/prism.ts)
- [Модуль Tag - Кодовый блок](https://github.com/hexojs/hexo/blob/master/lib/plugins/tag/code.js)
- [Плагин тегов - Блок Backtick Code](https://github.com/hexojs/hexo/blob/master/lib/plugins/filter/before_post_render/backtick_code_block.js)
