---
title: Plugins de Tags
---

Plugins de tags são diferentes dos posts tags. São reportados a partir de Outubro e fornecem uma maneira útil de adicionar rapidamente conteúdo específico às suas publicações.

Embora você possa escrever suas postagens em qualquer formato, mas os plugins de tags sempre estarão disponíveis e a sintaxe permanece a mesma.

{% youtube I07XMi7MHd4 %}

_Plugins de tags não devem ser envolvidos dentro da sintaxe Markdown, por exemplo, `[]({% post_path lorem-ipsum %})` não é suportado._

## Citação em Bloco

Perfeito para adicionar citações ao seu post, com informações opcionais de autor, fonte e título.

**Apelido: Apelido:** citação

```
{% blockquote [author[, source]] [link] [source_link_title] %}
conteúdo
{% endblockquote %}
```

### Exemplos

**Sem argumentos. Bloqueio sem formatação.**

```
{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}
```

{% blockquote %}
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque hendrerit lacus ut purus iaculis feugiat. Sed nec tempor elit, quis aliquam neque. Curabitur sed diam eget dolor fermentum semper at eu lorem.
{% endblockquote %}

**Citação de um livro**

```
{% blockquote David Levithan, Wide Awake %}
Não procure apenas a felicidade para si mesmo. Procure felicidade por todos. Pela bondade. Através da piedade.
{% endblockquote %}
```

{% blockquote David Levithan, Wide Awake %}
Não apenas busque felicidade para si mesmo. Procure felicidade por todos. Pela bondade. Através da piedade.
{% endblockquote %}

**Citação do Twitter**

```
{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NEW: DevDocs agora vem com destaque de sintaxe. http://devdocs.io
{% endblockquote %}
```

{% blockquote @DevDocs https://twitter.com/devdocs/status/356095192085962752 %}
NOVO: DevDocs agora vem com destaque de sintaxe. http://devdocs.io
{% endblockquote %}

**Citação de um artigo na web**

```
{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Bem-vindo ao Marketing de Ilhas %}
Toda interação é tanto preciosa quanto uma oportunidade de encantar.
{% endblockquote %}
```

{% blockquote Seth Godin http://sethgodin.typepad.com/seths_blog/2009/07/welcome-to-island-marketing.html Bem-vindo ao Marketing de Ilha %}
Toda a interacção é simultaneamente preciosa e uma oportunidade para se regozijar.
{% endblockquote %}

## Bloco de código

Recurso útil para adicionar trechos de código à sua publicação.

**Alias:** code

```
{% codeblock [title] [lang:language] [url] [texto do link] [opções adicionais] %}
código snippet
{% endcodeblock %}
```

Especificar opções adicionais no formato `option:value` , ex.: `line_number:false first_line:5`.

| Opções adicionais | Descrição:                                                                                                                                                                                    | Padrão       |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `número_linha`    | Mostrar número de linha                                                                                                                                                                       | `verdadeiro` |
| `limite_linha`    | Mostrar apenas números de linha contanto que os números de linhas do bloco de código excedam esse limite.                                                                                     | `0`          |
| `Destaque`        | Ativar destaque de código                                                                                                                                                                     | `verdadeiro` |
| `primeira_linha`  | Especifique o número da primeira linha                                                                                                                                                        | `1`          |
| `marcar`          | Destaque de linha linha específica, cada valor separado por uma vírgula. Especifique o intervalo de números usando um traço<br>Exemplo: `marca:1,4-7,10` marcará a linha 1, 4 a 7 e 10. |              |
| `embrulhar`       | Envolva o bloco de código em [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table)                                                                               | `verdadeiro` |

### Exemplos

**Um bloco de código simples**

```
{% codeblock %}
alert('Olá Mundo!');
{% endcodeblock %}
```

{% codeblock %}
alert('Olá Mundo!');
{% endcodeblock %}

**Especificando o idioma**

```
{% codeblock lang:objc %}
[rectangle setX: 10 y: 10 width: 20 height: 20];
{% endcodeblock %}
```

{% codeblock lang:objc %}
[retângulo setX: 10: 10 largura: 20 altura: 20];
{% endcodeblock %}

**Adicionando uma legenda ao bloco de código**

```
{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}
```

{% codeblock Array.map %}
array.map(callback[, thisArg])
{% endcodeblock %}

**Adicionando uma legenda e um URL**

```
{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]);
=> [1, 2, 3]
{% endcodeblock %}
```

{% codeblock _.compact http://underscorejs.org/#compact Underscore.js %}
_.compact([0, 1, false, 2, '', 3]); => [1, 2, 3]
{% endcodeblock %}

## Bloco de Backtick

Isso é idêntico ao uso de um bloco de código, mas ao invés disso, usa três backticks para delimitar o bloco.

{% raw %}
&#96`[language] [title] [url] [texto do link]
código snippet
&#96;`
{% endraw %}

## Puxar Cotação

Para adicionar cotações aos seus posts:

```
{% pullquote [class] %}
content
{% endpullquote %}
```

## jsFiddle

Para incorporar um trecho jsFiddle

```
{% jsfiddle shorttag [tabs] [skin] [width] [height]%}
```

## Neblina

Para incorporar um trecho Gist

```
{% gist gist_id [filename]%}
```

## iframe

Para incorporar um iframe:

```
{% iframe url [width] [height] %}
```

## Imagem:

Insere uma imagem com um tamanho especificado.

```
{% img [nomes de classes] /path/to/image [width] [height] '"title text" "alt text"' %}
```

## Vincular

Insere um link com `target="_blank"` atributo

```
{% link texto url [external] [title]%}
```

## Incluir código

Insere códigos de snippets na pasta `source/downloads/code`. O local da pasta pode ser especificado através da opção `code_dir` na configuração.

```
{% include_code [title] [lang:language] [from:line] [to:line] caminho/para/arquivo %}
```

### Exemplos

**Incorporar todo o conteúdo dos test.js**

```
{% include_code lang:javascript test.js %}
```

**Inserir linha somente 3**

```
{% include_code lang:javascript from:3 to:3 test.js %}
```

**Inserir linha 5 a 8**

```
{% include_code lang:javascript from:5 to:8 test.js %}
```

**Inserir linha 5 no final do arquivo**

```
{% include_code lang:javascript from:5 test.js %}
```

**Inserir linha de 1 a 8**

```
{% include_code lang:javascript to:8 test.js %}
```

## Youtube

Insere um vídeo do YouTube.

```
{% youtube video_id [type] [cookie]%}
```

### Exemplos

**Incorporar um vídeo**

```
{% youtube lJIrF4YjHfQ %}
```

**Incorporar uma playlist**

```
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' %}
```

**Ativar modo privado aprimorado**

Cookie do YouTube não é usado neste modo.

```
{% youtube lJIrF4YjHfQ false %}
{% youtube PL9hW1uS6HUfscJ9DHkOSoOX45MjXduUxo 'playlist' false %}
```

## Vimeo

Insere um vídeo de tamanho responsivo ou específico Vimeo.

```
{% vimeo video_id [width] [height]%}
```

## Incluir postagens

Incluir links para outros posts.

```
{% post_path filename %}
{% post_link filename [title] [escape]%}
```

Você pode ignorar as informações de permalink e pasta, como idiomas e datas, ao usar esta tag.

Por exemplo: `{% raw %}{% post_link how-to-bake-a-cake %}{% endraw %}`.

Isso funcionará contanto que o nome de arquivo do post seja `como fazer para fazer bolo. d`, mesmo que a publicação esteja localizada em `fonte/posts/2015-02-meu-feriado-` e tenha permalink `2018/en/how-to-bake-a-cake`.

É possível personalizar o texto para exibir, ao invés de exibir o título do post.

O título do post e o texto personalizado são escapados por padrão. Você pode usar a opção `escape` para desativar fuga.

Por exemplo:

**Exibe o título da mensagem.**

`{% raw %}{% post_link hexo-3-8-released %}{% endraw %}`

{% post_link hexo-3-8-released %}

**Exibir texto personalizado.**

`{% raw %}{% post_link hexo-3-8-released 'Link to a post' %}{% endraw %}`

{% post_link hexo-3-8-released 'Link to a post' %}

**Título da fuga.**

```
{% post_link hexo-4-released 'Como usar a tag <b> no título' %}
```
{% post_link hexo-4-released 'How to use <b> tag in title' %}

**Não escape do título.**

```
{% post_link hexo-4 lançado '<b>bold</b> título personalizado falso %}
```

{% post_link hexo-4 lançado '<b>bold</b> título personalizado falso %}

## Incluir Ativos

Inclua conteúdos publicados, para ser usado em conjunto com [`post_asset_folder`](/docs/asset-folders).

```
{% asset_path filename %}
{% asset_img [nome de classe] slug [width] [height] [título texto [alt text]] %}
{% asset_link filename [title] [escape]%}
```

### Incorporar imagem

_hexo-renderer-marked 3.1.0+ can (optionally) resolves the post's path of an image automatically, refer to [this section](/docs/asset-folders#Embedding-an-image-using-markdown) on how to enable it._

"foo.jpg" está localizado em `http://example.com/2020/01/02/hello/foo.jpg`.

**Padrão (sem opção)**

`{% asset_img foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg">
```

**Classe personalizada**

`{% asset_img post-image foo.jpg %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" class="post-image">
```

**Tamanho da exibição**

`{% asset_img foo.jpg 500 400 %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" width="500" height="400">
```

**Título & Alt**

`{% asset_img foo.jpg "lorem ipsum'dolor'" %}`

``` html
<img src="/2020/01/02/hello/foo.jpg" title="lorem ipsum" alt="dolor">
```

## RAW

Se determinado conteúdo estiver causando problemas de processamento em suas publicações, envolva-o com a tag `raw` para evitar erros de renderização.

```
{% raw %}
conteúdo
{% endraw %}
```

## Postar resumo

Use o texto colocado antes da tag `<!-- more -->` como um trecho para a publicação. `excerpt:` value in the [front-matter](/docs/front-matter#Settings-amp-Their-Default-Values), if specified, will take precedent.

**Exemplos:**

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
<!-- more -->
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
