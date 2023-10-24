---
title: Variáveis
---

{% youtube T9oAax-IRw0 %}

### Variáveis Globais

| Variável       | Descrição                                                                                | Tipo                                     |
| -------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------- |
| `Site`         | Informações do site.                                                                     | `object`; veja [Variáveis do Site][]     |
| `Página`       | Informações específicas da página e  variáveis personalizadas definidas no front-matter. | `object`; veja [Variáveis da Página][]   |
| `configuração` | Configuração do site.                                                                    | `object` (arquivo `_config` do seu site) |
| `Tema`         | Configuração do tema. Herda a configuração do site.                                      | `object` (arquivo `_config` do seu tema) |
| `caminho`      | Caminho da página atual                                                                  | `sequência`                              |
| `URL`          | URL completa da página atual                                                             | `sequência`                              |
| `env`          | Variáveis de ambiente                                                                    | ???                                      |

{% note warn %}
Lodash foi removido de variáveis globais desde o Hexo 5.0.0. [You-Dont-Need-Lodash-Underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore) might be helpful for your migration.
{% endnote %}

### Variáveis do Site

| Variável          | Descrição           | Tipo                      |
| ----------------- | ------------------- | ------------------------- |
| `site.posts`      | Todos as postagens  | `array` de objetos `post` |
| `site.pages`      | Todas as páginas    | `array` de objetos `page` |
| `site.categorias` | Todas as categorias | `array` de ???            |
| `tags.site`       | Todas as tags       | `array` de ???            |

### Variáveis da Página

**Artigo (`page`)**

| Variável           | Descrição                                                                       | Tipo                 |
| ------------------ | ------------------------------------------------------------------------------- | -------------------- |
| `page.title`       | Título do artigo                                                                | `sequência`          |
| `page.date`        | Data de criação do artigo                                                       | [objeto Moment.js][] |
| `atualizada`       | Data da última atualização do artigo                                            | [objeto Moment.js][] |
| `comentários`      | Comentário habilitado ou não                                                    | `boolean`            |
| `layout`           | Nome do layout                                                                  | `sequência`          |
| `page.content`     | O conteúdo completo processado do artigo                                        | `sequência`          |
| `trecho`           | Trecho do artigo                                                                | `sequência`          |
| `page.more`        | Conteúdo exceto trecho do artigo                                                | `sequência`          |
| `page.ssource`     | O caminho do arquivo de fontes                                                  | `sequência`          |
| `_fonte_de_página` | Caminho completo do arquivo de fontes                                           | `sequência`          |
| `caminho`          | A URL do artigo sem a URL raiz. Usamos geralmente `url_for(page.path)` no tema. | `sequência`          |
| `page.permalink`   | URL completa do artigo                                                          | `sequência`          |
| `page.prev`        | A postagem anterior, `null` se for a primeira postagem                          | ???                  |
| `próximo`          | A próxima postagem, `null` se for a última postagem                             | ???                  |
| `novembro`         | Os dados brutos do artigo                                                       | ???                  |
| `fotografias`      | As fotos do artigo (Usado em postagens de galeria)                              | array de ???         |
| `link_de_página`   | O link externo do artigo (Usado em postagens de link)                           | `sequência`          |

**Post (`post`):** O mesmo que o layout `page` mas adicione as seguintes variáveis.

| Variável       | Descrição                                    | Tipo           |
| -------------- | -------------------------------------------- | -------------- |
| `publicado`    | Verdadeiro se a postagem não for um rascunho | `boolean`      |
| `categoria(s)` | Todas as categorias da postagem              | `array` de ??? |
| `tags-página`  | Todas as tags da postagem                    | `array` de ??? |

**Casa (`índice`)**

| Variável               | Descrição                                                                         | Tipo        |
| ---------------------- | --------------------------------------------------------------------------------- | ----------- |
| `página_por_página`    | Postagens exibidas por página                                                     | `Número`    |
| `_total`               | Número total de páginas                                                           | `Número`    |
| `page.corrente`        | Número da página atual                                                            | `Número`    |
| `URL_de_publicação`    | A URL da página atual                                                             | `sequência` |
| `posts`                | Posts nesta página ([Modelo de Dados](https://hexojs.github.io/warehouse/))       | `objeto`    |
| `page.prev`            | Número da página anterior. `0` se a página atual for a primeira.                  | `Número`    |
| `link_de_page.previna` | A URL da página anterior. `''` se a página atual for a primeira.                  | `sequência` |
| `próximo`              | Número da próxima página. `0` se a página atual for a última.                     | `Número`    |
| `próximo_link`         | A URL da próxima página. `''` se a página atual for a última.                     | `sequência` |
| `caminho`              | A URL da página atual sem URL raiz. Costumamos usar `url_for(page.path)` no tema. | `sequência` |

**Arquivo (`archive`):** O mesmo que o layout do `index`, mas adicione as seguintes variáveis.

| Variável       | Descrição                                       | Tipo      |
| -------------- | ----------------------------------------------- | --------- |
| `page.archive` | Igual a `true`                                  | `boolean` |
| `ano_página`   | Ano do arquivo (4 - dígitos)                    | `Número`  |
| `mês`          | Mês do arquivo (2 dígitos sem zeros à esquerda) | `Número`  |

**Categoria (`category`):** O mesmo que o layout do `index` mas adicione as seguintes variáveis.

| Variável           | Descrição         | Tipo        |
| ------------------ | ----------------- | ----------- |
| `categoria-página` | Nome da categoria | `sequência` |

**Tag (`tag`):** O mesmo que o layout do `index` mas adicione as seguintes variáveis.

| Variável   | Descrição   | Tipo        |
| ---------- | ----------- | ----------- |
| `page.tag` | Nome da tag | `sequência` |

[objeto Moment.js]: http://momentjs.com/
[Variáveis do Site]: #Variaveis-do-Site
[Variáveis da Página]: #Variaveis-da-Pagina
