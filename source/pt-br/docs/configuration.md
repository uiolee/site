---
title: Configuração
---

Você pode modificar as configurações do site em `_config.yml` ou em um [arquivo de configuração alternativo](#Usando-uma-Configuracao-Alternativa).

### site

| Configuração     | Descrição                                                                                                                                                                                                                                                                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Título`         | O título do seu site                                                                                                                                                                                                                                                         |
| `legenda`        | O subtítulo do seu site                                                                                                                                                                                                                                                      |
| `Descrição`      | A descrição do seu site                                                                                                                                                                                                                                                      |
| `Palavras-chave` | As palavras-chave de seu site. Suporta vários valores.                                                                                                                                                                                                                       |
| `autor`          | Seu nome                                                                                                                                                                                                                                                                     |
| `Idioma`         | O idioma do seu site. Use a [2-lettter ISO-639-1 code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). O padrão é `en`.                                                                                                                                              |
| `timezone`       | O fuso horário do seu site. O Hexo usa a configuração do seu computador por padrão. Você pode encontrar a lista de fusos horários disponíveis [aqui](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Alguns exemplos são `America/New_York`, `Japan` e `UTC`. |

### URL:

| Configuração                 | Descrição                                                                                      | Padrão                   |
| ---------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------ |
| `URL`                        | A URL do seu site, must starts with `http://` or `https://`                                    |                          |
| `raiz`                       | O diretório raiz do seu site                                                                   | `url's pathname`         |
| `permalink`                  | O formato de [permalink](permalinks.html) dos artigos                                          | `:ano/:mês/:day/:title/` |
| `permalink_padrão`           | Valores padrão de cada segmento no permalink                                                   |                          |
| `url_bonita`                 | Rewrite the [`permalink`](variables.html) variables to pretty URLs                             |                          |
| `URLs_pretty_trailing_index` | Rastreando `index.html`, selecione `false` para removê-lo                                      | `verdadeiro`             |
| `modelo_urls.trailing_html`  | Rastreamento `.html`, selecionar `false` para remover (_não se aplica ao rastro `index.html`_) | `verdadeiro`             |

{% note info Site em subdiretório %}
Se o seu site estiver em um subdiretório (como por exemplo `http://example.org/blog`) defina `url` para `http://example.org/blog` e defina `root` para `/blog/`.
{% endnote %}

Exemplo:

``` yaml
# Ex.: page.permalink é http://example.com/foo/bar/index.html
pretty_urls:
  trailing_index: false
# vira http://example.com/foo/bar/
```

### Diretório

| Configuração           | Descrição                                                                                                                                                                      | Padrão          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- |
| `diretório_origem`     | Diretório dos fonte. Onde seu conteúdo está armazenado                                                                                                                         | `Fonte`         |
| `public_dir`           | Diretório dos arquivos públicos. Onde o site estático será gerado                                                                                                              | `Público`       |
| `tag_dir`              | Diretório de tags                                                                                                                                                              | `Etiquetas`     |
| `diretório_de_arquivo` | Diretório de archives                                                                                                                                                          | `arquivos`      |
| `diretório_categoria`  | Diretório de categorias                                                                                                                                                        | `Categorias`    |
| `code_dir`             | Diretório de código (subdiretório de `source_dir`)                                                                                                                             | `baixar/código` |
| `i18n_dir`             | Diretório de internacionalização (i18n)                                                                                                                                        | `:lang`         |
| `renderizar_pula`      | Caminhos que não devem ser renderizados. Você pode usar [expressões globais](https://github.com/micromatch/micromatch#extended-globbing) para fazer correspondência de caminho |                 |

Transformar títulos em maiúsculo?

``` yaml
skip_render: "mypage/**/*"
# irá output `source/mypage/index.html` e `source/mypage/code.js` sem alterá-los.

## Isso também pode ser usado para excluir posts,
skip_render: "_posts/test-post.md"
# irá ignorar `source/_posts/test-post.md`.
```

### Escrita

| Configuração                 | Descrição                                                                                                         | Padrão       |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------ |
| `novo_nome_postagem`         | O formato do nome do arquivo para novas postagens                                                                 | `:title.md`  |
| `layout_padrão`              | Layout padrão                                                                                                     | `publicação` |
| `titlecase`                  | Transformar títulos em caso de título?                                                                            | `Falso`      |
| `Link_externo`               | Abrir links externos em uma nova aba?                                                                             |              |
| `Ativar_link_externo.ativar` | Abrir links externos em uma nova aba?                                                                             | `verdadeiro` |
| `link_externo.campo`         | Aplica-se a todo o `site` ou `post` apenas                                                                        | `Site`       |
| `excluir_link.externo`       | Excluir hostname. Especificar subdomínio quando aplicável, incluindo `www`                                        | `[]`         |
| `nome_arquivo_caso`          | Converter nomes de arquivos para minúsculos `1`; maiúsculos `2`                                                   | `0`          |
| `rascunhos_de_renderização`  | Exibir rascunhos?                                                                                                 | `Falso`      |
| `mídia_de_imagem_post`       | Ativar o [diretório de Asset](asset-folders.html)?                                                                | `Falso`      |
| `link_relativa`              | Links para o diretório raiz?                                                                                      | `Falso`      |
| `futuro`                     | Exibir postagens futuras?                                                                                         | `verdadeiro` |
| `Destaque`                   | Configurações de bloco de código, see [Highlight.js](/docs/syntax-highlight#Highlight-js) section for usage guide |              |
| `prismjs`                    | Configurações de bloco de código, see [PrismJS](/docs/syntax-highlight#PrismJS) section for usage guide           |              |

### Configuração da página inicial

| Configuração                | Descrição                                                                                                            | Padrão   |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- |
| `gerador_índice`            | Gerar um arquivo de mensagens, alimentado por [hexo-generator-index](https://github.com/hexojs/hexo-generator-index) |          |
| `gerador_indexator.path`    | Caminho raiz para a página do seu blog                                                                               | `''`     |
| `gerador_índice.per_página` | Publicações exibidas por página.                                                                                     | `10`     |
| `gerador_index.order_por`   | Ordem das publicações. Ordenar por data decrescente (nova para antiga) por padrão.                                   | `-data`  |
| `Diretório de paginação`    | Formato da URL, consulte a configuração [Paginação](#Pagination) abaixo                                              | `Página` |

### Categoria & Tag

| Configuração       | Descrição                        | Padrão            |
| ------------------ | -------------------------------- | ----------------- |
| `categoria_padrão` | Mapa de Categoria                | `descategorizado` |
| `categoria_mapa`   | Sobrescrever slugs de categorias |                   |
| `marca_mapa`       | Sobrescrever slugs de etiquetas  |                   |

O Hexo irá ignorar os arquivos e diretórios listados abaixo deste campo

``` yaml
category_map:
  "Pensamentos de ontem": ontem-pensamentos
  "C++": c-plus-plus
```

### Formato de Data / Hora

Hexo usa [Moment.js](http://momentjs.com/) para processar datas.

| Configuração       | Descrição                                                                                                      | Padrão       |
| ------------------ | -------------------------------------------------------------------------------------------------------------- | ------------ |
| `formato_da_data`  | Formato de data                                                                                                | `AAAA-MM-DD` |
| `formato_de_tempo` | Formado de hora                                                                                                | `HH:mm:ss`   |
| `opção_atualizada` | The [`updated`](/pt-br/docs/variables#Variaveis-da-Pagina) value to used when not provided in the front-matter | `mtime`      |

{% note info updated_option %}
U`updated_option` controla o valor `atualizado` quando não for fornecido no front-matter:

- `mtime`: Usar data de modificação de arquivo como `atualizado`. É o comportamento padrão do Hexo desde 3.0.0
- `date`: usar `date` como `atualizado`. Normalmente usado com fluxo de trabalho Git quando data de modificação de arquivo pode ser diferente.
- `vazio`: Simplesmente solte `atualizado` quando não fornecido. Pode não ser compatível com a maioria dos temas e plugins.

`use_date_for_updated` está obsoleto e será removido na próxima versão principal. Por favor, use `updated_option: 'date'`.
{% endnote %}

### Paginação

| Configuração          | Descrição                                                                        | Categoria padrão |
| --------------------- | -------------------------------------------------------------------------------- | ---------------- |
| `por_página`          | A quantidade de postagens exibidas em uma única página. `0` desabilita paginação | `10`             |
| `diretório_paginação` | Formato URL                                                                      | `Página`         |

Exibir rascunhos?

``` yaml
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/awesome-pagine/2
```

### Extensões

| Configuração        | Descrição                                                                                                                           |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `Tema`              | Nome do tema. `false` desabilita o tema                                                                                             |
| `configuração_tema` | Configuração do tema. Inclui quaisquer configurações de tema personalizado sob esta chave para substituir os padrões do tema.       |
| `implantar`         | Configurações de implantação                                                                                                        |
| `meta_generator`    | [Meta generator](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes) tag. `false` desativa a injeção da tag. |

### Incluir/Excluir Arquivos ou Diretórios

Use as seguintes opções para processar explicitamente ou ignorar certos arquivos/pastas. Apoie [expressões glob](https://github.com/micromatch/micromatch#extended-globbing) para encontrar o caminho correspondente.

`incluir` e `excluir` opções apenas se aplicam à pasta `fonte/` , enquanto a opção `ignorar` aplica-se a todas as pastas.

| Por padrão, o Hexo ignora os arquivos e diretórios ocultos, mas configurar este campo fará com que o Hexo os processe também | Descrição:                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `incluir`                                                                                                                    | Inclua arquivos ocultos (incluindo arquivos/pastas com um nome que comece com um sublinhado, com uma exceção*)                                      |
| `Excluir`                                                                                                                    | No arquivo de configuração, defina a chave de include/exclude para que o hexo processe ou ignore, explicitamente, determinados arquivos/diretórios. |
| `ignorar`                                                                                                                    | Ignorar arquivos/pastas                                                                                                                             |

Mapa de Tag

```yaml
# Incluir/Excluir Arquivos/Diretórios
include:
  - ".nojekyll"
  # Include 'source/css/_typing.css'.
  - "css/_typing.css"
  # Inclui qualquer arquivo em 'source/_css/'.
  - "_css/*"
  # Inclui qualquer arquivo e subpasta em 'source/_css/'.
  - "_css/**/*"

exclui:
  # Excluir 'source/js/test.js'.
  - "js/test.js"
  # Excluir qualquer arquivo em 'source/js/'.
  - "js/*"
  # Excluir qualquer arquivo e subpasta em 'source/js/'.
  - "js/**/*"
  # Exclui qualquer arquivo com nome de arquivo que começa com 'test' em 'source/js/'.
  - "js/test*"
  # Exclui qualquer arquivo com nome de arquivo que começa com 'test' em 'source/js/' e suas subpastas.
  - "js/**/test*"
  # Não use isso para excluir postagens na 'source/_posts/'.
  # Use skip_render para isso. Ou preceda um sublinhado ao nome do arquivo.
  # - "_posts/hello-world.md" # Não funciona.

ignore:
  # Ignore qualquer pasta chamada 'foo'.
  - "**/foo"
  # Ignore a pasta 'foo' somente na pasta 'themes/'.
  - "**/themes/*/foo"
  # O mesmo que acima, mas se aplica a todas as subpastas de 'themes/'.
  - "**/themes/**/foo"
```

Cada valor da lista deve ser entre aspas únicas/duplas.

`inclui:` e `exclue:` não se aplica à pasta `temas/`. Either use `ignore:` or alternatively, prepend an underscore to the file/folder name to exclude.

\* Exceção notável é a pasta `source/_posts` , mas qualquer arquivo ou pasta com um nome que começa com um sublinhado nessa pasta ainda seria ignorado. Using `include:` rule in that folder is not recommended.

### Usando uma Configuração Alternativa

Um caminho de arquivo de configuração personalizado pode ser especificado adicionando o sinalizador `--config` aos seus comandos `hexo` com o caminho para um arquivo de configuração YAML ou JSON alternativo ou uma lista separada por vírgulas (sem espaços) de vários arquivos YAML ou JSON.

``` bash
# use 'custom.yml' no lugar de '_config.yml'
$ hexo server --config custom.yml

# use 'custom. ml' & 'custom2.json', priorizando 'custom2.json'
$ servidor hexo --config custom.yml,custom2.json
```

Usar vários arquivos combina todos os arquivos de configuração e salva as configurações mescladas para `_multiconfig.yml`. Os valores posteriores têm prioridade. Ele funciona com qualquer número de arquivos JSON e YAML com objetos arbitrariamente profundos. Note que **não são permitidos espaços na lista**.

Por exemplo, no exemplo acima se `foo: bar` está em `personalizado. ml`, mas `"foo": "dinossauro"` está no `personalizado2. son`, `_multiconfig.yml` conterá `foo: dinossauro`.

### Configuração alternativa de tema

Temas Hexo são projetos independentes, com arquivos `separados de A_config.yml`.

Instead of forking a theme, and maintaining a custom branch with your settings, you can configure it from somewhere else.

**`theme_config` in site's primary configuration file**

> Suportado desde o Hexo 2.8.2

```yml
# _config.yml
tema: "meu-tema"
theme_config:
  bio: "Meu nome incrível"
  foo:
    bar: 'a'
```

```yml
# temas/meu-tema/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

Resultado na configuração do tema:

```json
{
  bio: "Minha bio" incrível",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

**dedicated `_config.[theme].yml` file**

> Suportado desde Hexo 5.0.0

O arquivo deve ser colocado na pasta do site, tanto `yml` quanto `json` são suportados. `tema` dentro `_config.yml` deve ser configurado para que o Hexo leia `_config.[theme].yml`

```yml
# _config.yml
tema: "meu-tema"
```

```yml
# _config.my-theme.yml
bio: "Minha bio" incrível
foo:
  bar: 'a'
```

```yml
# temas/meu-tema/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

Resultado na configuração do tema:

```json
{
  bio: "Minha bio" incrível",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

{% note %}
We strongly recommends you to store your theme configuration in one place. But in case you have to store your theme configuration separately, those information is quite important: The `theme_config` inside site's primary configuration file has the highest priority during merging, then the dedicated theme configuration file. the `_config.yml` file under the theme directory has the lowest priority.
{% endnote %}
