---
title: Плагины тегов
---

Плагины тегов отличаются от тегов в посте. Они портированы с Octopress и обеспечивают удобный способ, чтобы быстро добавить контент для ваших постов.

Хотя вы можете писать свои сообщения в любых форматах, но плагины тегов всегда будут доступны и синтаксис остается прежним.

{% youtube I07XMi7MHd4 %}

_Плагины тегов не должны быть завернуты в синтаксис Markdown, например, `[]({% post_path lorem-ipsum %})` не поддерживается._

## Блок цитаты

Подходит для добавления цитаты в свой пост с указанием автора, источника и информационным заголовком.

**Блок данных:** цитата

```
{% blockquote [author[, source]] [link] [source_link_title] %}
содержание
{% endblockquote %}
```

### Примеры

**Без аргументов. Обычная цитата.**

```
{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}
```

{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

**Цитата из книги**

```
{% blockquote David Levithan, Wide Awake %}
Не просто ищи счастья для себя. Ищите счастье для всех. Через доброту. Через милосердие.
{% endblockquote %}
```

{% blockquote Дэвид Левитан, Широкий Awake %}
Не просто ищите счастья для себя. Ищите счастье для всех. Через доброту. Через милосердие.
{% endblockquote %}

**Цитата из Twitter**

```
{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs теперь поставляется с подсветкой синтаксиса. http://devdocs.io
{% endblockquote %}
```

{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
НОВОЕ: DevDocs теперь поставляется с подсветкой синтаксиса. http://devdocs.io
{% endblockquote %}

**Цитата из статьи в интернете**

```
{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Welcome to Island Marketing %}
Every interaction is both precious and an opportunity to delight.
{% endblockquote %}
```

{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Добро пожаловать на остров Маркетинг %}
Каждое взаимодействие – это как ценность, так и возможность порадовать.
{% endblockquote %}

## Блок с кодом

Полезная функция для добавления фрагментов кода в пост.

**Блок данных:** code (код)

```
{% codeblock [title] [lang:language] [url] [текст ссылки] [additional options] %}
code snippet
{% endcodeblock %}
```

Укажите дополнительные параметры в формате `option:value` , например `line_number:false first_line:5`.

| Дополнительные параметры | Описание                                                                                                                                                                                           | Значение по умолчанию |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| `номер строки`           | Показать номер строки                                                                                                                                                                              | `истина`              |
| `порог строки`           | Показывать только номера строк, если количество строк блока кода превышает такой порог.                                                                                                            | `0`                   |
| `подсветить`             | Включить подсветку кода                                                                                                                                                                            | `истина`              |
| `первая _строка`         | Укажите номер первой строки                                                                                                                                                                        | `1`                   |
| `метка`                  | Подсвечивать строку(и) подсвечивания строки(ов), каждое значение разделяется запятыми. Укажите диапазон чисел с помощью тире<br>Пример: `mark:1,4-7,10` будет отмечать строку 1, 4 - 7 и 10. |                       |
| `обернуть`               | Оберните кодовый блок в [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)                                                                                         | `истина`              |

### Примеры

**Простой блок кода**

```
{% codeblock %}
alert('Hello World!');
{% endcodeblock %}
```

{% codeblock %}
оповещение('Привет мир!');
{% endcodeblock %}

**С указанием языка**

```
{% codeblock lang:objc %}
[набор прямоугольника: 10 y: 10 ширина: 20 высота: 20];
{% endcodeblock %}
```

{% codeblock lang:objc %}
[прямоугольник setX: 10 y: 10 ширина: 20 высота: 20];
{% endcodeblock %}

**Добавление подписи к блоку кода**

```
{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}
```

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

**С добавлением заголовка и ссылки**

```
{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]);
=> [1, 2, 3]
{% endcodeblock %}
```

{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]); => [1, 2, 3]
{% endcodeblock %}

## Блок кода в кавычках

Тот же блок кода, но использует три обратные кавычки для отделения блока.

{% raw %}
&#96`[language] [title] [url] [текст ссылки]
код фрагмента
&#96;`
{% endraw %}

## Тянуть цитату

Добавляет цитату в пост:

```
{% pullquote [class] %}
content
{% endpullquote %}
```

## jsFiddle

Размещает фрагмент с jsFiddle:

```
{% jsfiddle shorttag [tabs] [skin] [width] [height]%}
```

## Жизнь

Размещает фрагмент с Gist:

```
{% gist_id [filename]%}
```

## iframe

Размещает iframe:

```
{% iframe url [width] [height] %}
```

## Картинка

Вставляет картинку с заданными размерами.

```
{% img [class names] /path/to/image [width] [height] '"title text" "alt text"' %}
```

## Ссылка

Вставляет ссылку с атрибутом `target="_blank"`.

```
{% link text url [external] [title] %}
```

## Включить код

Вставляет фрагменты кода из папки `source/downloads/code`. Расположение папки может быть указано с помощью опции `code_dir` в конфигурации.

```
{% include_code [title] [lang:language] [from:line] [to:line] path/to/file %}
```

### Примеры

**Встроить весь контент test.js**

```
{% include_code lang:javascript test.js %}
```

**Вставить только строку 3**

```
{% include_code lang:javascript from:3 to:3 test.js %}
```

**Встроенная строка 5-8**

```
{% include_code lang:javascript from:5 to:8 test.js %}
```

**Вставить строку 5 в конец файла**

```
{% include_code lang:javascript from:5 test.js %}
```

**Встроенная строка с 1 по 8**

```
{% include_code lang:javascript to:8 test.js %}
```

## YouTube

Вставка видео с YouTube.

```
{% youtube video_id [type] [cookie] %}
```

### Примеры

**Вставить видео**

```
{% youtube lJIrF4YjHfQ %}
```

**Вставить плейлист**

```
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' %}
```

**Включить режим секретности**

В этом режиме cookie YouTube не используется.

```
{% youtube lJIrF4YjHfQ false %}
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' false %}
```

## Vimeo

Вставляет видео отзывчивого или заданного размера.

```
{% vimeo video_id [width] [height] %}
```

## Включить сообщения

Содержит ссылку на другой пост.

```
{% post_path filename %}
{% post_link filename [title] [escape] %}
```

При использовании этого тэга вы можете игнорировать информацию о папках и языках, например языки и даты.

For instance: `{% raw %}{% post_link how-to-bake-a-cake %}{% endraw %}`.

Это будет работать до тех пор, пока файл поста будет `как-bake-a-cake. d`, даже если этот пост находится на `source/posts/2015-02-my-family-holiday` и имеет постоянную `2018/ru/how-to-bake-a-cake`.

Вы можете настроить текст для отображения, а не отображать заголовок сообщения.

Заголовок и пользовательский текст экранируются по умолчанию. Вы можете использовать опцию `escape` для отключения экрана.

Например:

**Отображать название должности.**

`{% raw %}{% post_link hexo-3-8-released %}{% endraw %}`

{% post_link hexo-3-8-released %}

**Показать пользовательский текст.**

`{% raw %}{% post_link hexo-3-8-released 'Link to a post' %}{% endraw %}`

{% post_link hexo-3-8-released 'Link to a post' %}

**Избегайте заголовка.**

```
{% post_link hexo-4-released 'How to use <b> tag in title' %}
```
{% post_link hexo-4-released 'How to use <b> tag in title' %}

**Не экранировать титул.**

```
{% post_link hexo-4-released '<b>bold</b> custom title' false %}
```

{% post_link hexo-4-released '<b>bold</b> custom title' false %}

## Включить активы

Включить активы, которые будут использоваться совместно с [`post_asset_folder`](/docs/asset-folders).

```
{% asset_path filename %}
{% asset_img [class names] slug [width] [height] [title text [alt text]] %}
{% asset_link filename [title] [escape] %}
```

### Вставить изображение

_hexo-renderer-marked 3.1.0+ can (необязательно) resolves the post path of the image automatically, refer to the [this section](/docs/asset-folders#Embedding-an-image-using-markdown) on how to enable it._

"foo.jpg" находится на `http://example.com/2020/01/02/hello/foo.jpg`.

**По умолчанию (без опции)**

`{% asset_img foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg">
```

**Пользовательский класс**

`{% asset_img post-image foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" class="post-image">
```

**Размер экрана**

`{% asset_img foo.jpg 500 400 %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" width="500" height="400">
```

**Название & Alt**

`{% asset_img foo.jpg "lorem ipsum'dolor'" %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" title="lorem ipsum" alt="dolor">
```

## URL

### url_for (7.0.0+)

Returns a url with the root path prefixed. Output is encoded automatically.

```
{% url_for text path [relative] %}
```

**Примеры:**

``` yml
_config.yml
root: /blog/ # example
```

``` 
{% url_for blog index.html %}
```

``` html
<a href="/blog/index.html">blog</a>
```

Relative link, follows `relative_link` option by default e.g. post/page path is '/foo/bar/index.html'

``` yml
_config.yml
relative_link: true
```

```
{% url_for blog index.html %}
```

``` html
<a href="../../index.html">blog</a>
```

You could also disable it to output a non-relative link, even when `relative_link` is enabled and vice versa.

```
{% url_for blog index.html false %}
```

``` html
<a href="/index.html">blog</a>
```

### full_url_for (7.0.0+)

Returns a url with the `config.url` prefixed. Output is encoded automatically.

```
{% full_url_for text path %}
```

**Examples:**

``` yml
_config.yml
url: https://example.com/blog # example
```

```
{% full_url_for index /a/path %}
```

``` html
<a href="https://example.com/blog/a/path">index</a>
```

## Сырье

Если определённый контент вызывает ошибки обработки в ваших постах, оберните его тегом `raw`, чтобы избежать ошибок обработки.

```
{% raw %}
content
{% endraw %}
```

## Отрывок из записи

Используйте текст до тега `<!-- more -->` в качестве отрывка поста. `excerpt:` value in the [front-matter](/docs/front-matter#Settings-amp-Their-Default-Values), if specified, will take precedent.

**Examples:**

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
<!-- more -->
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
