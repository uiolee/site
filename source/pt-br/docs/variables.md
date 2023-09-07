---
title: Variáveis
---

{% youtube T9oAax-IRw0 %}

### Variáveis globais

| Variável       | Descrição:                                                                              | tipo                                        |
| -------------- | --------------------------------------------------------------------------------------- | ------------------------------------------- |
| `Site`         | Informações do Site.                                                                    | `objeto`; ver [Variáveis do site][]         |
| `Página`       | Informações específicas da página e variáveis personalizadas definidas no front-matter. | `objeto`; ver [Variáveis de Página][]       |
| `configuração` | Configuração do site.                                                                   | `objeto` (arquivo de _config do site)       |
| `Tema`         | Configuração do tema. Herda da configuração do site.                                    | `objeto` (arquivo de _configuração do tema) |
| `caminho`      | Caminho da página atual                                                                 | `sequência`                                 |
| `URL`          | URL completo da página atual                                                            | `sequência`                                 |
| `env`          | Variáveis de ambiente                                                                   | ???                                         |

{% note warn %}
Lodash foi removido de variáveis globais desde o Hexo 5.0.0. [You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore) might be helpful for your migration.
{% endnote %}

### Variáveis do Site

| Variável          | Descrição:          | tipo                         |
| ----------------- | ------------------- | ---------------------------- |
| `site.posts`      | Todas as postagens  | `array` de `postar objetos`  |
| `site.pages`      | Todas as páginas    | `array` da página `` objetos |
| `site.categorias` | Todas as categorias | `array` de ???               |
| `tags.site`       | Todas as tags       | `array` de ???               |

### Variáveis da Página

**Artigo (`página`)**

| Variável           | Descrição:                                                                     | tipo                 |
| ------------------ | ------------------------------------------------------------------------------ | -------------------- |
| `page.title`       | Título do artigo                                                               | `sequência`          |
| `page.date`        | Data de criação                                                                | [objeto Moment.js][] |
| `atualizada`       | Última data de atualização do artigo                                           | [objeto Moment.js][] |
| `comentários`      | Comentário habilitado ou não                                                   | `boolean`            |
| `layout`           | Nome do layout                                                                 | `sequência`          |
| `page.content`     | O conteúdo processado completo do artigo                                       | `sequência`          |
| `trecho`           | Resumo do artigo                                                               | `sequência`          |
| `page.more`        | Conteúdo exceto resumo do artigo                                               | `sequência`          |
| `page.ssource`     | O caminho do arquivo de origem                                                 | `sequência`          |
| `_fonte_de_página` | Caminho completo do arquivo de origem                                          | `sequência`          |
| `caminho`          | A URL do artigo sem URL raiz. Normalmente usamos `url_for(page.path)` no tema. | `sequência`          |
| `page.permalink`   | URL completa (codificada) do artigo                                            | `sequência`          |
| `page.prev`        | O post anterior, `null` se a publicação é a primeira postagem                  | ???                  |
| `próximo`          | A próxima publicação, `null` se a publicação for a última publicação           | ???                  |
| `novembro`         | Os dados brutos do artigo                                                      | ???                  |
| `fotografias`      | As fotos do artigo (Usado em publicações de galeria)                           | matriz de ???        |
| `link_de_página`   | O link externo do artigo (Usado em postagens de links)                         | `sequência`          |

**Post (`post`):** O mesmo que o layout `página` mas adicione as seguintes variáveis.

| Variável       | Descrição:                                   | tipo           |
| -------------- | -------------------------------------------- | -------------- |
| `publicado`    | Verdadeiro se a postagem não for um rascunho | `boolean`      |
| `categoria(s)` | Todas as categorias da postagem              | `array` de ??? |
| `tags-página`  | Todas as tags da postagem                    | `array` de ??? |

**Casa (`índice`)**

| Variável               | Descrição:                                                                           | tipo        |
| ---------------------- | ------------------------------------------------------------------------------------ | ----------- |
| `página_por_página`    | Posts exibidos por página                                                            | `Número`    |
| `_total`               | Número total de páginas                                                              | `Número`    |
| `page.corrente`        | Número de página atual                                                               | `Número`    |
| `URL_de_publicação`    | A URL da página atual                                                                | `sequência` |
| `posts`                | Posts nesta página ([Modelo de Dados](https://hexojs.github.io/warehouse/))          | `objeto`    |
| `page.prev`            | Número de página anterior. `0` se a página atual é a primeira.                       | `Número`    |
| `link_de_page.previna` | A URL da página anterior. `''` if the current page is the first.                     | `sequência` |
| `próximo`              | Próximo número da página. `0` se a página atual for a última.                        | `Número`    |
| `próximo_link`         | O URL da próxima página. `''` if the current page is the last.                       | `sequência` |
| `caminho`              | A URL da página atual sem URL raiz. Normalmente usamos `url_for(page.path)` no tema. | `sequência` |

**Archive (`archive`):** O mesmo que o layout `índice` , mas adicione as seguintes variáveis.

| Variável       | Descrição:                                         | tipo      |
| -------------- | -------------------------------------------------- | --------- |
| `page.archive` | Equals `true`                                      | `boolean` |
| `ano_página`   | Ano de arquivo (4 dígitos)                         | `Número`  |
| `mês`          | Arquivar mês (dois algarismos sem zero à esquerda) | `Número`  |

**Categoria (`categoria`):** Igual ao layout `índice` , mas adiciona as seguintes variáveis.

| Variável           | Descrição:        | tipo        |
| ------------------ | ----------------- | ----------- |
| `categoria-página` | Nome da categoria | `sequência` |

**Tag (`tag`):** O mesmo que o layout `índice` , mas adicione as seguintes variáveis.

| Variável   | Descrição:  | tipo        |
| ---------- | ----------- | ----------- |
| `page.tag` | Nome da Tag | `sequência` |

[objeto Moment.js]: http://momentjs.com/
[Variáveis do site]: #Site-Variables
[Variáveis de Página]: #Page-Variables
