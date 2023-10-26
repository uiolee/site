---
title: Helpers
---

Os Helpers são usados em templates para ajudá-lo a inserir snippets (trechos de código) rapidamente.  Os helpers não podem ser usados em arquivos de source (arquivos de postagem em Markdown por exemplo).

Você pode usar os helpers padrões do Hexo ou [criar seus próprios helpers personalizados](../api/helper.html).

{% youtube Uc53pW0GJHU %}

## URL:

### url_para

Retorna uma url com o caminho raiz prefixado. Você deve usar esse helper em vez de `config.root + path` desde a versão 2.7 do Hexo.

``` js
<%- url_for(path) %>
```

| Opção      | Descrição              | Padrão                          |
| ---------- | ---------------------- | ------------------------------- |
| `relativo` | Link relativo de saída | Valor do `config.relative_link` |

**Exemplos:**

``` yml
_config.yml
root: /blog/ # exemplo
```

``` js
<%- url_for('/a/path') %>
// /blog/a/path
```

Link relativo, segue a opção `relative_link` por padrão por exemplo, caminho do post/página é '/foo/bar/index.html'

``` yml
_config.yml
relative_link: verdadeiro
```

``` js
<%- url_for('/css/style.css') %>
// ../../css/style. ss

/* Sobrescrever a opção
 * você também poderia desativá-la para saída de um link não relativo,
 * mesmo quando `relative_link` está ativado e vice-versa.
 */
<%- url_for('/css/style.css', {relative: false}) %>
// /css/style.css
```

### URL_relativa

Retorna a URL relativa de `from` para `to`.

``` js
<%- relative_url(de, to) %>
```

**Exemplos:**

``` js
<%- relative_url('foo/bar/', 'css/style.css') %>
// ../../css/style.css
```

### url_completo

Retorna uma url com `config.url` prefixado. A saída é codificada automaticamente.

``` js
<%- full_url_for(path) %>
```

**Exemplos:**

``` yml
_config.yml
url: https://example.com/blog # exemplo
```

``` js
<%- full_url_for('/a/path') %>
// https://example.com/blog/a/path
```

### gravatar

Retorna a URL da imagem do gravatar a partir de um e-mail.

Se você não especificar o parâmetro [options], as opções padrão serão aplicadas. Caso contrário, você pode configurá-lo para um número que será passado como parâmetro de tamanho para o Gravatar. Finalmente, se você configurá-lo para um objeto, ele será convertido em uma string de consulta de parâmetros para o Gravatar.

``` js
<%- gravatar(email, [options]) %>
```

| Opção | Descrição     | Padrão |
| ----- | ------------- | ------ |
| `s`   | Opção         | 40     |
| `d`   | Imagem Padrão |        |
| `fr`  | Forçar padrão |        |
| `ru`  | Classificação |        |

Mais informações: [Gravatar](https://en.gravatar.com/site/implement/images/)

**Exemplos:**

``` js
<%- gravatar('a@abc.com') %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787

<%- gravatar('a@abc.com', 40) %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787?s=40

<%- gravatar('a@abc.com' {s: 40, d: 'https://via.placeholder.com/150'}) %>
// https://www.gravatar.com/avatar/b9b00e66c6b8a70f88c73cb6bdb06787?s=40&d=https%3A%2F%2Fvia.placeholder.com%2F150
```

## Tags HTML

### css

Carrega arquivos CSS. Onde `path` pode ser um array ou uma string. Se `path` não for prefixado com `/` ou com qualquer protocolo, ele será prefixado com a URL raiz. Se você não adicionar a extensão `.css` após `path`, ela será adicionada automaticamente. Use o tipo de objeto para atributos personalizados.

``` js
<%- css(path, ...) %>
```

**Exemplos:**

``` js
<%- css('style.css') %>
// <link rel="stylesheet" href="/style.css">

<%- css(['style.css', 'screen.css']) %>
// <link rel="stylesheet" href="/style.css">
// <link rel="stylesheet" href="/screen.css">

<%- css({ href: 'style.css', integrity: 'foo' }) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">

<%- css([{ href: 'style.css', integrity: 'foo' }, { href: 'screen.css', integrity: 'bar' }]) %>
// <link rel="stylesheet" href="/style.css" integrity="foo">
// <link rel="stylesheet" href="/screen.css" integrity="bar">
```

### js

Carrega arquivos JavaScript. O `path` pode ser uma array ou uma string. [`/<root>/`](/docs/configuration#URL) value is prepended while `.js` extension is appended to the `path` automatically. Use o tipo de objeto para atributos personalizados.

``` js
<%- js(path, ...) %>
```

**Exemplos:**

``` js
<%- js('script.js') %>
// <script src="/script.js"></script>

<%- js(['script.js', 'gallery.js']) %>
// <script src="/script.js"></script>
// <script src="/gallery.js"></script>

<%- js({ src: 'script.js', integrity: 'foo', async: true }) %>
// <script src="/script.js" integrity="foo" async></script>

<%- js([{ src: 'script.js', integrity: 'foo' }, { src: 'gallery.js', integrity: 'bar' }]) %>
// <script src="/script.js" integrity="foo"></script>
// <script src="/gallery.js" integrity="bar"></script>
```

### link_para

Insere um link.

``` js
<%- link_to(caminho, [text], [options]) %>
```

| Opção     | Descrição                   | Padrão |
| --------- | --------------------------- | ------ |
| `Externo` | Abre o link em uma nova aba | Falso  |
| `aula`    | Nome da classe              |        |
| `id`      | ID                          |        |

**Exemplos:**

``` js
<%- link_to('http://www.google.com') %>
// <a href="http://www.google.com" title="http://www.google.com">http://www.google.com</a>

<%- link_to('http://www.google.com', 'Google') %>
// <a href="http://www.google.com" title="Google">Google</a>

<%- link_to('http://www.google.com', 'Google', {external: true}) %>
// <a href="http://www.google.com" title="Google" target="_blank" rel="noopener">Google</a>
```

### mail_para

Insere um link de e-mail.

``` js
<%- mail_to(path, [text], [options]) %>
```

| Opção     | Descrição          |
| --------- | ------------------ |
| `aula`    | Miscelânea         |
| `id`      | ID                 |
| `assunto` | Assunto do e-mail  |
| `cc`      | CC                 |
| `Cco`     | Cco                |
| `Corpo`   | Conteúdo do e-mail |

**Exemplos:**

``` js
<%- mail_to('a@abc.com') %>
// <a href="mailto:a@abc.com" title="a@abc.com">a@abc.com</a>

<%- mail_to('a@abc.com', 'Email') %>
// <a href="mailto:a@abc.com" title="Email">E-mail</a>
```

### tag_imagem

Insere uma imagem.

``` js
<%- image_tag(caminho, [options]) %>
```

| Alternativa | Descrição                   |
| ----------- | --------------------------- |
| `alt`       | Texto alternativo da imagem |
| `aula`      | Nome da classe              |
| `id`        | ID                          |
| `width`     | Largura da imagem           |
| `Altura`    | Altura da imagem            |

### tag_favicon_favicon

Insere um favicon.

``` js
<%- favicon_tag(caminho) %>
```

### tag_feed

Insere um link de feed.

``` js
<%- feed_tag(caminho, [options]) %>
```

| Alternativa | Descrição      | Padrão         |
| ----------- | -------------- | -------------- |
| `Título`    | Título do feed | `config.title` |
| `Tipo`      | Tipo do feed   |                |

**Exemplos:**

``` js
<%- feed_tag('atom.xml') %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">

<%- feed_tag('rss.xml', { title: 'RSS Feed', type: 'rss' }) %>
// <link rel="alternate" href="/atom.xml" title="RSS Feed" type="application/rss+xml">

/* Defaults to hexo-generator-feed's config if no argument */
<%- feed_tag() %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">
```

## Tags condicionais

### está_atual

Verifica se `path` corresponde à URL da página atual. Use opções `strict` para habilitar um modo estrito de correspondência.

``` js
<%- is_current(caminho, [strict]) %>
```

### está_morada

Verifica se a página atual é a pagina home.

``` js
<%- é_home() %>
```

### is_home_first_page (+6.3.0)

Formata um título com as primeiras letras de palavras importantes em maiúsculo.

``` js
<%- é_casa_primeiro_page() %>
```

### foi_publicação

A função que altera a exibição do nome do post.

``` js
<%- is_post() %>
```

### é_página

Verifica se a página atual é uma postagem.

``` js
<%- is_page() %>
```

### é_arquivo_de_arquivo

Verifica se a página atual é uma página de arquivo.

``` js
<%- is_archive() %>
```

### é_ano

Verifica se a página atual é uma página de arquivo anual.

``` js
<%- is_ano() %>
```

### é_mês

Verifica se a página atual é uma página de arquivo mensal.

``` js
<%- is_month() %>
```

### é_categoria_

Verifica se a página atual é uma página de categoria. Se uma string for dada como parâmetro, também é verificado se a página atual corresponde à categoria dada.

``` js
<%- is_category() %>
<%- is_category('hobby') %>
```

### tag_é

Verifica se a página atual é uma página de tag. Se uma string for dada como parâmetro, também é verificado se a página atual corresponde à tag fornecida.

``` js
<%- is_tag() %>
<%- is_tag('hobby') %>
```

## Manipulação de String

### Aparar

Remove espaços em branco no inicio e fim de uma string.

``` js
<%- recortar(string) %>
```

### listra_html

Remove as tags HTML de uma string.

``` js
<%- strip_html(string) %>
```

**Exemplos:**

``` js
<%- strip_html('Não é <b>importante</b> mais!') %>
// Não é mais importante!
```

### titlecase

Transforma uma cadeia de caracteres em legendas apropriadas.

``` js
<%- titlecase(string) %>
```

**Exemplos:**

``` js
<%- titlecase('esta é uma maçã') %>
# Isto é uma Apple
```

### markdown

Renderiza um conteúdo em Markdown.

``` js
<%- markdown(str) %>
```

**Exemplos:**

``` js
<%- markdown('me faz **forte**') %>
// me faz <strong>forte</strong>
```

### renderizar

Renderiza uma string.

``` js
<%- renderização (str, engine, [options]) %>
```

**Exemplos:**

``` js
<%- render('p(class="exemplo") Teste', 'pug'); %>
// <p class="example">Teste</p>
```

See [Rendering](https://hexo.io/pt-br/api/rendering) for more details.

### embrulhar_a_palavra

Coloca uma quebra de linha no texto a partir de um limite de caracteres, o limite é `length`. Por padrão, o valor de `length` é 80.

``` js
<%- word_wrap(str, [length]) %>
```

**Exemplos:**

``` js
<%- word_wrap('Uma vez no tempo', 8) %>
// Uma vez em\n
```

### truncado

Omite o texto após um certo valor de `length`. O valor padrão de `length` é 30 caracteres.

``` js
<%- truncate(texto, [options]) %>
```

**Exemplos:**

``` js
<%- truncate('Uma vez em um mundo muito distante', {length: 17}) %>
// Uma vez pelo...

<%- truncate('Uma vez em um mundo muito distante', {length: 17, separator: ' '}) %>
// Uma vez até...

<%- truncate('E descobriram que muitas pessoas estavam dormindo melhor.', {length: 25, omissão: '... (continued)'}) %>
// E elas f... (continuando)
```

### escape_html

Escapa entidades HTML em uma string.

``` js
<%- escape_html(str) %>
```

**Exemplos:**

``` js
<%- escape_html('<p>Olá "mundo".</p>') %>
// &lt;p&gt;Olá &quot;world&quot;.&lt;&#x2F;p&gt;
```

## Modelos

### parciais

Carrega outros arquivos de template. Você pode definir variáveis locais em `locals`.

``` js
<%- parcial(layout, [locals], [options]) %>
```

| Alternativa | Descrição                                                                              | Padrão  |
| ----------- | -------------------------------------------------------------------------------------- | ------- |
| `cache`     | Conteúdo da cache (usa fragmento de cache)                                             | `Falso` |
| `apenas`    | Variáveis locais estritas. Só usa variáveis definidas em `locals` dentro de templates. | `Falso` |

### fragmentar_cache

Cache do conteúdo em um fragmento. Salva o conteúdo dentro de um fragmento e serve o cache quando a próxima requisição chegar.

``` js
<%- fragment_cache(id, fn);
```

**Exemplos:**

``` js
<%- fragment_cache('cabeçalho', function(){
  return '<header></header>';
}) %>
```

## Data & Hora

### Data

Insere a data formatada. `date` pode ser data no padrão Unix, string ISO, objeto de data ou objeto [Moment.js][]. A Opção `format` usa a definição `date_format` por padrão.

``` js
<%- data (data, [format]) %>
```

**Exemplos:**

``` js
<%- date(Date.now()) %>
// 2013-01-01

<%- date(Date.now(), 'YYYY/M/D') %>
// Jan 1 2013
```

### date_xml

Insere a data no formato XML. `date` pode ser data no padrão Unix, string ISO, objeto de data ou objeto [Moment.js][].

``` js
<%- date_xml(date) %>
```

**Exemplos:**

``` js
<%- date_xml(Date.now()) %>
// 2013-01-01T00:00:00.000Z
```

### Horário

Insere a hora formatada. `date` pode ser data no padrão Unix, string ISO, objeto de data ou objeto [Moment.js][]. A Opção `format` usa a definição `time_format` por padrão.

``` js
<%- tempo(data, [format]) %>
```

**Exemplos:**

``` js
<%- time(Date.now()) %>
// 13:05:12

<%- time(Date.now(), 'h:mm:ss a') %>
// 1:05:12 pm
```

### data_completa

Insere a data e a hora formatadas. `date` pode ser data no padrão Unix, string ISO, objeto de data ou objeto [Moment.js][]. A Opção `format` usa a definição `date_format + time_format` por padrão.

``` js
<%- full_date(data, [format]) %>
```

**Exemplos:**

``` js
<%- full_date(new Date()) %>
// Jan 1, 2013 0:00:00

<%- full_date(nova Data(), 'dddd, MMMM Do YYYY, h:mm:ss a') %>
// Terça-feira, 1 de Janeiro de 2013, 12:00:00 am
```

### hora

Biblioteca [Moment.js][].

## Lista

### lista_categorias

Insere uma lista de todas as categorias.

``` js
<%- list_categorias([options]) %>
```

| Alternativa        | Descrição                                                                                                                                                                                                                                      | Categoria padrão |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| `ordenar por`      | Critério de ordenação das categorias                                                                                                                                                                                                           | Nome             |
| `pedido`           | Tipo de ordem. `1`, `asc` para ascendente; `-1`, `desc` para descendente                                                                                                                                                                       | 1                |
| `mostrar_contagem` | Exibir o número de postagens para cada categoria                                                                                                                                                                                               | verdadeiro       |
| `estilo`           | Estilo para exibir a lista de categorias. `list` exibe as categorias em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo.                                                                                          | lista            |
| `separador`        | Separador entre categorias. (Só funciona se `style` não for `list`).                                                                                                                                                                           | ,                |
| `profundidade`     | Níveis de categorias a serem exibidos. `0` exibe todas as categorias e suas categorias filhas; `-1` é semelhante a `0`, mas exibe as categorias e suas filhas em um mesmo nível hierárquico; `1` exibe apenas as categorias de nível superior. | 0                |
| `aula`             | Nome da classe da lista de categorias.                                                                                                                                                                                                         | Categoria        |
| `transformar`      | A função que altera a exibição do nome da categoria.                                                                                                                                                                                           |                  |
| `suffix`           | Adiciona um sufixo para o link.                                                                                                                                                                                                                | Nenhuma          |

**Exemplos:**

``` js
<%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return titlecase(str);
  }
}) %>

<%- list_categories(post.categories, {
  class: 'post-category',
  transform(str) {
    return str.toUpperCase();
  }
}) %>
```

### listar_tags

Insere uma lista de tags.

``` js
<%- list_tags([options]) %>
```

| Alternativa        | Descrição                                                                                                                                 | Padrão     |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `ordenar por`      | Padrão                                                                                                                                    | Nome       |
| `pedido`           | Tipo de ordem. `1`, `asc` para ascendente; `-1`, `desc` para descendente                                                                  | 1          |
| `mostrar_contagem` | Exibir o número de postagens para cada arquivo                                                                                            | verdadeiro |
| `estilo`           | Estilo para exibir a lista de tags. `list` exibe as tags em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`        | Separador entre postagens. (Só funciona se `style` não for `list`)                                                                        | ,          |
| `aula`             | Nome da classe da lista de tags (string) ou personalizar classe de cada tag (objeto, veja abaixo).                                        | Etiqueta   |
| `transformar`      | A função que muda a exibição do nome da tag. Veja exemplos em [list_categories](#list-categories).                                        |            |
| `Quantidade`       | O número de tags a exibir (0 = ilimitado)                                                                                                 | 0          |
| `suffix`           | Adiciona um sufixo para o link.                                                                                                           | Nenhuma    |

Personalização avançada da classe:

| Alternativa       | Descrição:                                                                                                                                                               | Padrão                                                         |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| `class.ul`        | `<ul>` nome de classe (apenas para estilo `lista`)                                                                                                                 | `tag-list` (estilo da lista)                                   |
| `class.li`        | `<li>` nome de classe (apenas para estilo `lista`)                                                                                                                 | `tag-list-item` (estilo da lista)                              |
| `class.a`         | `<a>` nome da classe                                                                                                                                               | `tag-list-link` (estilo de lista) `tag-link` (estilo normal)   |
| `classe.marcador` | `<span>` nome da classe onde o rótulo da tag é armazenado (apenas para estilo normal, quando `classe. abel` é definido que a etiqueta é colocada em `<span>` | `tag-label` (estilo normal)                                    |
| `contagem.classe` | `<span>` nome da classe onde o contador de tags é armazenado (somente quando `show_count` é `true`)                                                                | `tag-list-count` (estilo de lista) `tag-count` (estilo normal) |

Exemplos:

```ejs
<%- list_tags(site.tags, {class: 'classtest', style: false, separator: ' | '}) %>
<%- list_tags(site. idades, {class: 'classtest', style: 'list'}) %>
<%- list_tags(site. ags, {class: {ul: 'ululul', li: 'lilili', a: 'aaa', count: 'ccc'}, style: false, separator: '}) %>
<%- list_tags(site. ags, {class: {ul: 'ululul', li: 'lilili', a: 'aaa', count: 'ccc'}, style: 'list'}) %>
```

### listar_arquivos

Insere uma lista de arquivos (archives).

``` js
<%- list_archives([options]) %>
```

| Alternativa        | Descrição:                                                                                                                                     | Padrão     |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `Tipo`             | Tipo. Esse valor pode ser `yearly` ou `monthly`.                                                                                               | Mensal     |
| `pedido`           | Tipo de ordem. `1`, `asc` para ascendente; `-1`, `desc` para descendente                                                                       | 1          |
| `mostrar_contagem` | A função que altera a exibição do nome do archive.                                                                                             | verdadeiro |
| `formato`          | Formato da data                                                                                                                                | AAAA MMMM  |
| `estilo`           | Estilo para exibir a lista de arquivos. `list` exibe arquivos em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`        | Separador entre arquivos. (Só funciona se `style` não for `list`)                                                                              | ,          |
| `aula`             | Nome da classe da lista de arquivos.                                                                                                           | arquivo    |
| `transformar`      | A função que muda a exibição do nome do arquivo. Veja exemplos em [list_categories](#list-categories).                                         |            |

### listar_posts

Insere uma lista de posts.

``` js
<%- list_posts([options]) %>
```

| Alternativa   | Descrição:                                                                                                                                          | Padrão     |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `ordenar por` | Critério de ordenação de postagens                                                                                                                  | Data       |
| `pedido`      | Tipo de ordem. `1`, `asc` para ascendente; `-1`, `desc` para descendente                                                                            | 1          |
| `estilo`      | Estilo para exibir a lista de postagens. `list` exibe as postagens em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`   | Separador entre tags. (Só funciona se `style` não for `list`).                                                                                      | ,          |
| `aula`        | Nome da classe da lista de postagem.                                                                                                                | publicação |
| `Quantidade`  | O número de postagens a serem exibidas (0 = ilimitado)                                                                                              | 6          |
| `transformar` | A função que muda a exibição do nome do post. Veja exemplos em [list_categories](#list-categories).                                                 |            |

### tagcloud

Insere uma nuvem de tags.

``` js
<%- tagcloud([tags], [options]) %>
```

| Alternativa              | Descrição:                                                                                                                                                                                           | Padrão    |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `min_fonte`              | Tamanho mínimo da fonte                                                                                                                                                                              | 10        |
| `max_font`               | Tamanho máximo da fonte                                                                                                                                                                              | 20        |
| `unidade`                | Unidade de tamanho de fonte                                                                                                                                                                          | px        |
| `Quantidade`             | Quantidade total de tags                                                                                                                                                                             | Ilimitado |
| `ordenar por`            | Critério de ordenação das tags                                                                                                                                                                       | Nome      |
| `pedido`                 | Tipo de ordenação. `1`, `asc` para ascendente; `-1`, `desc` para descendente                                                                                                                         | 1         |
| `cor`                    | Colorizar a nuvem de tags?                                                                                                                                                                           | Falso     |
| `cor_inicial`            | Cor inicial. Você pode usar o padrão hexadecimal (`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hsla(283, 100%, 50%, 1)`) ou [color keywords][]. Esta opção só funciona quando `color` é `true`. |           |
| `cor_fim`                | Cor final. Você pode usar o padrão hexadecimal (`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hsla(283, 100%, 50%, 1)`) ou [color keywords][]. Esta opção só funciona quando `color` é `true`.   |           |
| `aula`                   | Prefixo da classe das tags                                                                                                                                                                           |           |
| `Nível`                  | O número de diferentes nomes de aula. Esta opção só funciona quando a classe `` é definida.                                                                                                          | 10        |
| `mostrar_count` (+6.3.0) | Exibir o número de postagens para cada tag                                                                                                                                                           | Falso     |
| `count_class` (+6.3.0)   | A função que altera a exibição do nome da tag.                                                                                                                                                       | contar    |

**Exemplos:**

``` js
// Opções padrão
<%- tagcloud() %>

// Limita o número de etiquetas a 30
<%- tagcloud({amount: 30}) %>
```

## Diversos

### paginador

Insere um paginador.

``` js
<%- paginator(opcions) %>
```

| Alternativa                                                                                                                                    | Descrição:                                                                                             | Padrão                |
| ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | --------------------- |
| `Base`                                                                                                                                         | URL base                                                                                               | /                     |
| `formato`                                                                                                                                      | Formato da URL                                                                                         | página /%d/           |
| `Total`                                                                                                                                        | Número de páginas                                                                                      | 1                     |
| `corrente`                                                                                                                                     | Número da página atual                                                                                 | 0                     |
| `legislador_texto`                                                                                                                             | O texto do link da página anterior. Funciona apenas se `prev_next` estiver definido como `true`.       | Anterior              |
| `próximo_texto`                                                                                                                                | O texto do link da próxima página. Funciona apenas se `prev_next` estiver definido como `true`.        | Próximo               |
| `Espaço`                                                                                                                                       | Espaço do texto                                                                                        | &hellp;               |
| `anterior_próximo`                                                                                                                             | Exibir os links anteriores e seguintes                                                                 | verdadeiro            |
| `tamanho_final`                                                                                                                                | O número de páginas exibidas no início e no final                                                      | 1                     |
| `tamanho_meio`                                                                                                                                 | O número de páginas exibidas entre a página atual, mas não incluindo a página atual                    | 2                     |
| `mostrar_todos`                                                                                                                                | Exibir todas as páginas. Se isso for definido como `true`, `end_size` e `mid_size` não irão funcionar. | Falso                 |
| `escapar`                                                                                                                                      | Escape de tags HTML                                                                                    | verdadeiro            |
| &lt;%- strip_html('It\'s not &lt;b&gt;important&lt;/b&gt; anymore!') %&gt; // It's not important anymore! | Padrão                                                                                                 | `Padrão`              |
| `classe atual` (+6.3.0)                                                                                                                        | Descrição                                                                                              | `corrente`            |
| `space_class` (+6.3.0)                                                                                                                         | Padrão                                                                                                 | `Espaço`              |
| `prev_class` (+6.3.0)                                                                                                                          | Padrão                                                                                                 | `estender o anterior` |
| `próxima _classe` (+6.3.0)                                                                                                                     | Descrição                                                                                              | `estender próximo`    |
| `force_prev_next` (+6.3.0)                                                                                                                     | Nenhum                                                                                                 | Falso                 |


**Exemplos:**

``` js
<%- paginator({
  prev_text: '<',
  next_text: '>'
}) %>
```

``` html
<!-- Rendered as -->
<a href="/1/">&lt;</a>
<a href="/1/">1</a>
2
<a href="/3/">3</a>
<a href="/3/">&gt;</a>
```

``` js
<%- paginator({
  prev_text: '<i class="fa fa-angle-left"></i>',
  next_text: '<i class="fa fa-angle-right"></i>',
  escape: false
}) %>
```

``` html
<!-- Rendered as -->
<a href="/1/"><i class="fa fa-angle-left"></i></a>
<a href="/1/">1</a>
2
<a href="/3/">3</a>
<a href="/3/"><i class="fa fa-angle-right"></i></a>
```

### formulário_pesquisa

Insere o formulário de busca do Google.

``` js
<%- search_form(options) %>
```

| Alternativa | Descrição:                                                                                                                   | Padrão              |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| `aula`      | O nome da classe do formulário                                                                                               | formulário-pesquisa |
| `Texto`     | Palavra de sugestão de busca                                                                                                 | Pesquisa            |
| `botão`     | Exibir o botão de busca. O valor pode ser um booleano ou uma string. Quando o valor é uma string, ele será o texto do botão. | Falso               |

### formato_número

Formata um número.

``` js
<%- numero_formato(número, [options]) %>
```

| Alternativa   | Descrição:                                                                        | Padrão |
| ------------- | --------------------------------------------------------------------------------- | ------ |
| `precisão`    | A precisão do número. O valor pode ser `false` ou um número inteiro não negativo. | Falso  |
| `delimitador` | O delimitador de casa de milhares                                                 | ,      |
| `separador`   | O separador entre os dígitos fracionários e inteiros.                             | .      |

**Exemplos:**

``` js
<%- number_format(12345.67, {precision: 1}) %>
// 12,345.68

<%- number_format(12345. 7, {precision: 4}) %>
// 12,345.6700

<%- number_format(12345. 7, {precision: 0}) %>
// 12,345

<%- number_format(12345.67, {delimiter: ''}) %>
// 12345. 7

<%- formato_number(12345.67, {separator: '/'}) %>
// 12,345/67
```

### meta_generator

Insere a tag [gerador](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta).

``` js
<%- meta_generator() %>
```

**Exemplos:**

``` js
<%- meta_generator() %>
// <meta name="generator" content="Hexo 4.0.0">
```

### abrir_gráfico

Insere dados do [Open Graph][].

``` js
<%- open_graph([options]) %>
```

| Alternativa      | Descrição:                                                  | Padrão                                                      |
| ---------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `Título`         | Título da página (`og:title`)                               | `page.title`                                                |
| `Tipo`           | Tipo de página (`og:type`)                                  | blog                                                        |
| `URL`            | URL da página (`og:url`)                                    | `URL`                                                       |
| `Imagem`         | Capa da página (`og:image`)                                 | Todas as imagens do conteúdo                                |
| `autor`          | Autor do artigo (`og:article:author`)                       | `autor_configuração`                                        |
| `Data`           | Tempo de publicação do artigo (`og:article:published_time`) | Tempo de publicação                                         |
| `Atualizado`     | Tempo modificado do artigo (`og:article:modified_time`)     | Hora modificada da página                                   |
| `Idioma`         | Idioma do artigo (`og:locale`)                              | `page.lang ├page.language ├^\\config.language`            |
| `nome_site`      | Nome do site (`og:site_name`)                               | `config.title`                                              |
| `Descrição`      | Descrição da página (`og:description`)                      | Trecho da página ou os 200 primeiros caracteres do conteúdo |
| `cartão_twitter` | Tipo de Twitter card (`twitter:card`)                       | summary                                                     |
| `twitter_id`     | ID do Twitter (`twitter:creator`)                           |                                                             |
| `site_twitter`   | Site do Twitter (`twitter:site`)                            |                                                             |
| `twitter_image`  | Twitter Image (`twitter:image`)                             |                                                             |
| `google_plus`    | Link de perfil do Google+                                   |                                                             |
| `admins`         | ID de administrador do Facebook                             |                                                             |
| `fb_app_id`      | ID da aplicação do Facebook                                 |                                                             |

### toc

Analisa todas as tags de título (h1~h6) no conteúdo e insere um índice.

``` js
<%- toc(str, [options]) %>
```

| Alternativa             | Descrição:                              | Padrão            |
| ----------------------- | --------------------------------------- | ----------------- |
| `aula`                  | Nome da classe                          | `toc`             |
| `class_item` (+6.3.0)   | Descrição                               | `${class}-item`   |
| `class_link` (+6.3.0)   | Descrição                               | `Link ${class}`   |
| `class_text` (+6.3.0)   | Descrição                               | `${class}-texto`  |
| `class_child` (+6.3.0)  | Nome da classe                          | `${class}-child`  |
| `class_number` (+6.3.0) | Padrão                                  | `Numero ${class}` |
| `class_level` (+6.3.0)  | Critério de ordenação de tags           | `Nível ${class}`  |
| `número_lista`          | Exibe o número da lista                 | verdadeiro        |
| `profundeza_máx`        | Profundidade máxima do cabeçalho gerado | 6                 |
| `profundeza_mínima`     | Profundidade mínima do toc gerado       | 1                 |

**Exemplos:**

``` js
<%- toc(page.content) %>
```

#### data-toc-unnumbered (+6.1.0)

Títulos com atributo `data-toc-unnumbered="true"` serão marcados como unnumbered (o número da lista não será exibido).

{% note avise "Aviso!" %}
Para usar o `data-toc-unnumbered="true"`, o renderizador deve ter a opção de adicionar classes de CSS.

Por favor, veja abaixo de PRs.

- https://github.com/hexojs/hexo/pull/4871
- https://github.com/hexojs/hexo-util/pull/269
- https://github.com/hexojs/hexo-renderer-markdown-it/pull/174
{% endnote %}

[color keywords]: http://www.w3.org/TR/css3-color/#svg-color
[Moment.js]: http://momentjs.com/
[Open Graph]: http://ogp.me/
