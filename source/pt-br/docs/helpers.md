---
title: Helpers
---

Os auxiliares são usados em templates para ajudar você a inserir snippets rapidamente.  Os auxiliares não podem ser usados nos arquivos de origem.

Você poderia facilmente [escrever seu próprio assistente personalizado](https://hexo.io/api/helper.html) ou usar nossos auxiliares já preparados.

{% youtube Uc53pW0GJHU %}

## URL:

### url_para

Retorna uma URL com o caminho raiz prefixado. A saída é codificada automaticamente.

``` js
<%- url_for(caminho, [option]) %>
```

| Alternativa | Descrição:             | Padrão                          |
| ----------- | ---------------------- | ------------------------------- |
| `relativo`  | Link relativo de saída | Valor do `config.relative_link` |

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

Retorna a URL relativa do `do` para o `para o`.

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

Se você não especificar o parâmetro [options] , as opções padrão serão aplicadas. Caso contrário, você pode definir para um número que será passado como o parâmetro de tamanho para o Gravatar. Finalmente, se você definir como um objeto, ele será convertido em uma string de consulta de parâmetros para Gravatar.

``` js
<%- gravatar(email, [options]) %>
```

| Alternativa | Descrição:                 | Padrão |
| ----------- | -------------------------- | ------ |
| `s`         | Tamanho da imagem de saída | 80     |
| `d`         | Imagem Padrão              |        |
| `fr`        | Forçar padrão              |        |
| `ru`        | Classificação              |        |

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

Carrega arquivos CSS. `caminho` pode ser um array ou uma string. `caminho` pode ser uma string, um array, um objeto ou um array de objetos. [`/<root>/`](/docs/configuration#URL) valor é antecipado enquanto a extensão `.css` é automaticamente anexada ao caminho `` Use o tipo de objeto para atributos personalizados.

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

Carrega arquivos JavaScript `caminho` pode ser uma string, um array, um objeto ou um array de objetos. [`/<root>/`](/docs/configuration#URL) value is prepended while `.js` extension is appended to the `path` automatically. Use o tipo de objeto para atributos personalizados.

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

| Alternativa | Descrição:                  | Padrão |
| ----------- | --------------------------- | ------ |
| `Externo`   | Abre o link em uma nova aba | Falso  |
| `aula`      | Nome da classe              |        |
| `id`        | ID                          |        |

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

| Alternativa | Descrição:          |
| ----------- | ------------------- |
| `aula`      | Nome da classe      |
| `id`        | ID                  |
| `assunto`   | Assunto da mensagem |
| `cc`        | CC                  |
| `Cco`       | Cco                 |
| `Corpo`     | Conteúdo do e-mail  |

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

| Alternativa | Descrição:                  |
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

| Alternativa | Descrição:          | Padrão         |
| ----------- | ------------------- | -------------- |
| `Título`    | Título do feed      | `config.title` |
| `Tipo`      | Tipo de alimentação |                |

**Exemplos:**

``` js
<%- feed_tag('atom.xml') %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">

<%- feed_tag('rss.xml', { title: 'RSS Feed', type: 'rss' }) %>
// <link rel="alternate" href="/atom.xml" title="RSS Feed" type="application/atom+xml">

/* Defaults to hexo-generator-feed's config if no argument */
<%- feed_tag() %>
// <link rel="alternate" href="/atom.xml" title="Hexo" type="application/atom+xml">
```

## Tags Condicionais

### está_atual

Verifique se o `caminho` coincide com a URL da página atual. Use `opções strict` para habilitar correspondência estrita.

``` js
<%- is_current(caminho, [strict]) %>
```

### está_morada

Verifique se a página atual é a página inicial.

``` js
<%- é_home() %>
```

### is_home_first_page (+6.3.0)

Verifique se a página atual é a primeira da página inicial.

``` js
<%- é_casa_primeiro_page() %>
```

### foi_publicação

Verifique se a página atual é um post.

``` js
<%- is_post() %>
```

### é_página

Verifique se a página atual é uma página.

``` js
<%- is_page() %>
```

### é_arquivo_de_arquivo

Verifique se a página atual é uma página de arquivos.

``` js
<%- is_archive() %>
```

### é_ano

Verifique se a página atual é uma página de arquivo anual.

``` js
<%- is_ano() %>
```

### é_mês

Verifique se a página atual é uma página de arquivo mensal.

``` js
<%- is_month() %>
```

### é_categoria_

Verifique se a página atual é uma página da categoria. Se uma string é dada como parâmetro, verifique se a página atual corresponde à categoria dada.

``` js
<%- is_category() %>
<%- is_category('hobby') %>
```

### tag_é

Verifique se a página atual é uma página. Se uma seqüência de caracteres for dada como parâmetro, verifique se a página atual corresponde à etiqueta fornecida.

``` js
<%- is_tag() %>
<%- is_tag('hobby') %>
```

## Manipulação de strings

### Aparar

Remove espaços de prefixos e rasto de uma string.

``` js
<%- recortar(string) %>
```

### listra_html

Desativa todas as tags HTML em uma string.

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

Renderiza uma sequência de caracteres com Markdown.

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

Consulte [Renderização](https://hexo.io/api/rendering) para mais detalhes.

### embrulhar_a_palavra

Envolve texto em linhas não mais do que `comprimento`. O comprimento `` é 80 por padrão.

``` js
<%- word_wrap(str, [length]) %>
```

**Exemplos:**

``` js
<%- word_wrap('Uma vez no tempo', 8) %>
// Uma vez em\n
```

### truncado

Trunca texto após um certo tamanho ``. O padrão é de 30 caracteres.

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

Carrega outros arquivos de template. Você pode definir variáveis locais em `locais`.

``` js
<%- parcial(layout, [locals], [options]) %>
```

| Alternativa | Descrição:                                                                            | Padrão  |
| ----------- | ------------------------------------------------------------------------------------- | ------- |
| `cache`     | Conteúdo do cache (usar cache do fragmento)                                           | `Falso` |
| `apenas`    | Variáveis locais estritas. Use apenas conjunto de variáveis em `locais` em templates. | `Falso` |

### fragmentar_cache

Cai o conteúdo em um fragmento. Ele salva o conteúdo dentro de um fragmento e serve o cache quando a próxima solicitação chegar.

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

Insere data formatada. `date` pode ser unix, string ISO, objeto de data ou [Moment.js][]. Definição `formato` é `date_format` por padrão.

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

Insere a data no formato XML. `date` pode ser unix, string ISO, objeto de data ou [Moment.js][].

``` js
<%- date_xml(date) %>
```

**Exemplos:**

``` js
<%- date_xml(Date.now()) %>
// 2013-01-01T00:00:00.000Z
```

### Horário

Insere a hora formatada. `date` pode ser unix, string ISO, objeto de data ou [Moment.js][]. Definição `formato` é `time_format` por padrão.

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

Insere data e hora formatados. `date` pode ser unix, string ISO, objeto de data ou [Moment.js][]. `format` is `date_format + time_format` setting by default.

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

| Alternativa        | Descrição:                                                                                                                                                                              | Padrão     |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `ordenar por`      | Ordem das categorias                                                                                                                                                                    | Nome       |
| `pedido`           | Ordenação de pedido. `1`, `asc` para ascender; `-1`, `desc` para decrescente                                                                                                            | 1          |
| `mostrar_contagem` | Exibir o número de postagens para cada categoria                                                                                                                                        | verdadeiro |
| `estilo`           | Estilo para exibir a lista de categorias. `list` exibe categorias em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo.                                      | lista      |
| `separador`        | Separador entre categorias. (Só funciona se o estilo `` não for `list`)                                                                                                                 | ,          |
| `profundidade`     | Níveis das categorias a serem exibidas. `0` exibe todas as categorias e categorias filhas; `-1` é semelhante a `0` mas exibida no plano; `1` exibe apenas categorias de nível superior. | 0          |
| `aula`             | Nome da classe da lista de categorias.                                                                                                                                                  | Categoria  |
| `transformar`      | A função que muda a exibição do nome da categoria.                                                                                                                                      |            |
| `suffix`           | Adicionar um sufixo ao link.                                                                                                                                                            | Nenhuma    |

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

Insere uma lista de todos os marcadores.

``` js
<%- list_tags([options]) %>
```

| Alternativa        | Descrição:                                                                                                                                   | Padrão     |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `ordenar por`      | Ordem das categorias                                                                                                                         | Nome       |
| `pedido`           | Ordenação de pedido. `1`, `asc` para ascender; `-1`, `desc` para decrescente                                                                 | 1          |
| `mostrar_contagem` | Exibir o número de postagens para cada tag                                                                                                   | verdadeiro |
| `estilo`           | Estilo para exibir a lista de tags. `list` exibe marcadores em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`        | Separador entre categorias. (Só funciona se o estilo `` não for `list`)                                                                      | ,          |
| `aula`             | Nome da classe da lista de tags (string) ou personalizar classe de cada tag (objeto, veja abaixo).                                           | Etiqueta   |
| `transformar`      | A função que muda a exibição do nome da tag. Veja exemplos em [list_categories](#list-categories).                                           |            |
| `Quantidade`       | O número de tags a exibir (0 = ilimitado)                                                                                                    | 0          |
| `suffix`           | Adicionar um sufixo ao link.                                                                                                                 | Nenhuma    |

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

Insere uma lista de arquivos.

``` js
<%- list_archives([options]) %>
```

| Alternativa        | Descrição:                                                                                                                                     | Padrão     |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| `Tipo`             | Type. Este valor pode ser `anual` ou `mensal`.                                                                                                 | Mensal     |
| `pedido`           | Ordenação de pedido. `1`, `asc` para ascender; `-1`, `desc` para decrescente                                                                   | 1          |
| `mostrar_contagem` | Exibe o número de postagens para cada arquivo                                                                                                  | verdadeiro |
| `formato`          | Formato da Data                                                                                                                                | AAAA MMMM  |
| `estilo`           | Estilo para exibir a lista de arquivos. `list` exibe arquivos em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`        | Separador entre arquivos. (Só funciona se o estilo `` não for `list`)                                                                          | ,          |
| `aula`             | Nome da classe da lista de arquivos.                                                                                                           | arquivo    |
| `transformar`      | A função que muda a exibição do nome do arquivo. Veja exemplos em [list_categories](#list-categories).                                         |            |

### listar_posts

Insere uma lista de postagens.

``` js
<%- list_posts([options]) %>
```

| Alternativa   | Descrição:                                                                                                                                       | Padrão     |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- |
| `ordenar por` | Ordem das postagens                                                                                                                              | Data       |
| `pedido`      | Ordenação de pedido. `1`, `asc` para ascender; `-1`, `desc` para decrescente                                                                     | 1          |
| `estilo`      | Estilo para exibir a lista de postagens. `list` exibe postagens em uma lista não ordenada. Use `false` ou qualquer outro valor para desativá-lo. | lista      |
| `separador`   | Separador entre postagens. (Só funciona se o estilo `` não for `list`)                                                                           | ,          |
| `aula`        | Nome da classe da lista de postagens.                                                                                                            | publicação |
| `Quantidade`  | O número de posts a exibir (0 = ilimitado)                                                                                                       | 6          |
| `transformar` | A função que muda a exibição do nome do post. Veja exemplos em [list_categories](#list-categories).                                              |            |

### tagcloud

Insere uma nuvem de tags.

``` js
<%- tagcloud([tags], [options]) %>
```

| Alternativa              | Descrição:                                                                                                                                                                                           | Padrão    |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `min_fonte`              | Tamanho mínimo da fonte                                                                                                                                                                              | 10        |
| `max_font`               | Tamanho máximo da fonte                                                                                                                                                                              | 20        |
| `unidade`                | Tamanho da unidade da fonte                                                                                                                                                                          | px        |
| `Quantidade`             | Quantidade total de marcadores                                                                                                                                                                       | Ilimitado |
| `ordenar por`            | Ordem das tags                                                                                                                                                                                       | Nome      |
| `pedido`                 | Ordem de classificação. `1`, `asc` como ascendente; `-1`, `desc` como decrescente                                                                                                                    | 1         |
| `cor`                    | Colita a nuvem de tags                                                                                                                                                                               | Falso     |
| `cor_inicial`            | Cor inicial. Você pode usar hexadecimal (`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hsla(283, 100%, 50%, 1)`) ou [palavras-chave de cor][]. Esta opção só funciona quando `cor` é verdadeira. |           |
| `cor_fim`                | Cor final. Você pode usar hexadecimal (`#b700ff`), rgba (`rgba(183, 0, 255, 1)`), hsla (`hsla(283, 100%, 50%, 1)`) ou [palavras-chave de cor][]. Esta opção só funciona quando `cor` é verdadeira.   |           |
| `aula`                   | Prefixo da classe das tags                                                                                                                                                                           |           |
| `Nível`                  | O número de diferentes nomes de aula. Esta opção só funciona quando a classe `` é definida.                                                                                                          | 10        |
| `mostrar_count` (+6.3.0) | Exibir o número de postagens para cada tag                                                                                                                                                           | Falso     |
| `count_class` (+6.3.0)   | Nome da classe da contagem de tags                                                                                                                                                                   | contar    |

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

| Alternativa                | Descrição:                                                                                      | Padrão                |
| -------------------------- | ----------------------------------------------------------------------------------------------- | --------------------- |
| `Base`                     | URL Base                                                                                        | /                     |
| `formato`                  | Formato URL                                                                                     | página /%d/           |
| `Total`                    | O número de páginas                                                                             | 1                     |
| `corrente`                 | Número de página atual                                                                          | 0                     |
| `legislador_texto`         | O texto do link da página anterior. Funciona somente se `prev_next` estiver definido como true. | Anterior              |
| `próximo_texto`            | O texto do link da próxima página. Funciona somente se `prev_next` estiver definido como true.  | Próximo               |
| `Espaço`                   | O texto da sala                                                                                 | &hellp;               |
| `anterior_próximo`         | Exibir links anteriores e seguintes                                                             | verdadeiro            |
| `tamanho_final`            | O número de páginas exibidas no início e no final                                               | 1                     |
| `tamanho_meio`             | O número de páginas exibidas entre a página atual, mas não incluindo a página atual.            | 2                     |
| `mostrar_todos`            | Exibir todas as páginas. Se definido como verdadeiro, `end_size` e `mid_size` não funcionará    | Falso                 |
| `escapar`                  | Escape de tags HTML                                                                             | verdadeiro            |
| `page_class` (+6.3.0)      | Nome da classe                                                                                  | `número-página`       |
| `classe atual` (+6.3.0)    | Nome atual da classe da página                                                                  | `corrente`            |
| `space_class` (+6.3.0)     | Nome da classe espacial                                                                         | `Espaço`              |
| `prev_class` (+6.3.0)      | Nome da página anterior                                                                         | `estender o anterior` |
| `próxima _classe` (+6.3.0) | Nome da próxima página                                                                          | `estender próximo`    |
| `force_prev_next` (+6.3.0) | Forçar exibição de links anteriores e seguintes                                                 | Falso                 |


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

Insere um formulário de pesquisa do Google.

``` js
<%- search_form(options) %>
```

| Alternativa | Descrição:                                                                                                    | Padrão              |
| ----------- | ------------------------------------------------------------------------------------------------------------- | ------------------- |
| `aula`      | O nome da classe do formulário                                                                                | formulário-pesquisa |
| `Texto`     | Pesquisar palavra da dica                                                                                     | Pesquisa            |
| `botão`     | Exibir botão de busca. O valor pode ser booleano ou string. Se o valor for uma string, será o texto do botão. | Falso               |

### formato_número

Formata um número.

``` js
<%- numero_formato(número, [options]) %>
```

| Alternativa   | Descrição:                                                               | Padrão |
| ------------- | ------------------------------------------------------------------------ | ------ |
| `precisão`    | A precisão do número. The value can be `false` or a nonnegative integer. | Falso  |
| `delimitador` | Os milhares de delimitadores                                             | ,      |
| `separador`   | O separador entre os dígitos fracionários e inteiros.                    | .      |

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

Insere [dados Open Graph][].

``` js
<%- open_graph([options]) %>
```

| Alternativa      | Descrição:                                                  | Padrão                                                      |
| ---------------- | ----------------------------------------------------------- | ----------------------------------------------------------- |
| `Título`         | Título da página (`og:title`)                               | `page.title`                                                |
| `Tipo`           | Tipo de página (`og:type`)                                  | blog                                                        |
| `URL`            | URL da Página (`og:url`)                                    | `URL`                                                       |
| `Imagem`         | Imagens de página (`og:image`)                              | Todas as imagens do conteúdo                                |
| `autor`          | Autor do artigo (`og:article:author`)                       | `autor_configuração`                                        |
| `Data`           | Tempo de publicação do artigo (`og:article:published_time`) | Tempo de publicação                                         |
| `Atualizado`     | Tempo modificado do artigo (`og:article:modified_time`)     | Hora modificada da página                                   |
| `Idioma`         | Idioma do artigo (`og:locale`)                              | `page.lang ├page.language ├^\\config.language`            |
| `nome_site`      | Nome do site (`og:site_name`)                               | `config.title`                                              |
| `Descrição`      | Descrição da página (`og:description`)                      | Resumo de página ou os primeiros 200 caracteres do conteúdo |
| `cartão_twitter` | Tipo de cartão do Twitter (`twitter:card`)                  | summary                                                     |
| `twitter_id`     | ID do Twitter (`twitter:creator`)                           |                                                             |
| `site_twitter`   | Site do Twitter (`twitter:site`)                            |                                                             |
| `google_plus`    | Link para perfil do Google+                                 |                                                             |
| `admins`         | ID do administrador do Facebook                             |                                                             |
| `fb_app_id`      | ID App do Facebook                                          |                                                             |

### toc

Analisa todas as tags de título (h1~h6) no conteúdo e insere uma tabela de conteúdo.

``` js
<%- toc(str, [options]) %>
```

| Alternativa             | Descrição:                        | Padrão            |
| ----------------------- | --------------------------------- | ----------------- |
| `aula`                  | Nome da classe                    | `toc`             |
| `class_item` (+6.3.0)   | Nome da classe do item            | `${class}-item`   |
| `class_link` (+6.3.0)   | Nome da classe do link            | `Link ${class}`   |
| `class_text` (+6.3.0)   | Nome da classe do texto           | `${class}-texto`  |
| `class_child` (+6.3.0)  | Nome da classe filho              | `${class}-child`  |
| `class_number` (+6.3.0) | Nome da classe numerar            | `Numero ${class}` |
| `class_level` (+6.3.0)  | Prefixo da classe do nível        | `Nível ${class}`  |
| `número_lista`          | Exibe o número da lista           | verdadeiro        |
| `profundeza_máx`        | Profundidade máxima do toc gerado | 6                 |
| `profundeza_mínima`     | Profundidade mínima do toc gerado | 1                 |

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

[palavras-chave de cor]: http://www.w3.org/TR/css3-color/#svg-color
[Moment.js]: http://momentjs.com/
[dados Open Graph]: http://ogp.me/
