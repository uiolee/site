---
title: Configuração
---

Você pode modificar as configurações do site em `_config.yml` ou em um [arquivo de configuração alternativo](#Using-an-Alternate-Config).

### site

| Configuração     | Descrição:                                                                                                                                                                                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Título`         | O título do seu site                                                                                                                                                                                                                                         |
| `legenda`        | A legenda do seu site                                                                                                                                                                                                                                        |
| `Descrição`      | A descrição do seu site                                                                                                                                                                                                                                      |
| `Palavras-chave` | As palavras-chave de seu site. Suporta vários valores.                                                                                                                                                                                                       |
| `autor`          | Seu Nome                                                                                                                                                                                                                                                     |
| `Idioma`         | O idioma do seu site. Use um código [2-letter ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) ou opcionalmente [sua variante](/docs/internationalization). O padrão é `en`.                                                                |
| `timezone`       | O fuso horário do seu site. Hexo usa a configuração no seu computador por padrão. You can find the list of available timezones [here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). Alguns exemplos são `América/New_York`, `Japão`e `UTC`. |

### URL:

| Configuração                 | Descrição:                                                                                     | Padrão                   |
| ---------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------ |
| `URL`                        | A URL do seu site, deve começar com `http://` ou `https://`                                    |                          |
| `raiz`                       | O diretório raiz do seu site                                                                   | `url's pathname`         |
| `permalink`                  | O formato [permalink](permalinks.html) dos artigos                                             | `:ano/:mês/:day/:title/` |
| `permalink_padrão`           | Valores padrão de cada segmento em permalink                                                   |                          |
| `url_bonita`                 | Reescreva as variáveis [`permalink`](permalinks.html) para linhar URLs                         |                          |
| `URLs_pretty_trailing_index` | Rastreando `index.html`, selecione `false` para removê-lo                                      | `verdadeiro`             |
| `modelo_urls.trailing_html`  | Rastreamento `.html`, selecionar `false` para remover (_não se aplica ao rastro `index.html`_) | `verdadeiro`             |

{% note info Website in subdirectory %}
Se o seu site estiver em um subdiretório (como `http://example.org/blog`) defina `url` para `http://exemplo. rg/blog` e definir `raiz` para `/blog/`.
{% endnote %}

Exemplos:

``` yaml
# Ex.: page.permalink é http://example.com/foo/bar/index.html
pretty_urls:
  trailing_index: false
# vira http://example.com/foo/bar/
```

### Diretório

| Configuração           | Descrição:                                                                                                                                                                         | Padrão          |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `diretório_origem`     | Pasta de origem. Onde seu conteúdo é armazenado                                                                                                                                    | `Fonte`         |
| `public_dir`           | Pasta pública. Onde o site estático será gerado                                                                                                                                    | `Público`       |
| `tag_dir`              | Diretório de tags                                                                                                                                                                  | `Etiquetas`     |
| `diretório_de_arquivo` | Diretório de arquivos                                                                                                                                                              | `arquivos`      |
| `diretório_categoria`  | Diretório de categorias                                                                                                                                                            | `Categorias`    |
| `code_dir`             | Incluir pasta de código (subdiretório de `source_dir`)                                                                                                                             | `baixar/código` |
| `i18n_dir`             | Diretório i18n                                                                                                                                                                     | `:lang`         |
| `renderizar_pula`      | Caminhos que serão copiados para `pública` cru, sem ser renderizado. You can use [glob expressions](https://github.com/micromatch/micromatch#extended-globbing) for path matching. |                 |

Exemplos:

``` yaml
skip_render: "mypage/**/*"
# irá output `source/mypage/index.html` e `source/mypage/code.js` sem alterá-los.

## Isso também pode ser usado para excluir posts,
skip_render: "_posts/test-post.md"
# irá ignorar `source/_posts/test-post.md`.
```

### Escrevendo

| Configuração                 | Descrição:                                                                                                                                         | Padrão       |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| `novo_nome_postagem`         | Formato do nome do arquivo para novas postagens                                                                                                    | `:title.md`  |
| `layout_padrão`              | Layout padrão                                                                                                                                      | `publicação` |
| `titlecase`                  | Transformar títulos em caso de título?                                                                                                             | `Falso`      |
| `Link_externo`               | Abrir links externos em uma nova aba?                                                                                                              |              |
| `Ativar_link_externo.ativar` | Abrir links externos em uma nova aba?                                                                                                              | `verdadeiro` |
| `link_externo.campo`         | Aplica-se a todo o `site` ou `post` apenas                                                                                                         | `Site`       |
| `excluir_link.externo`       | Excluir hostname. Especificar subdomínio quando aplicável, incluindo `www`                                                                         | `[]`         |
| `nome_arquivo_caso`          | Transformar nomes de arquivo para `1` minúscula; `2` maiúsculas                                                                                    | `0`          |
| `rascunhos_de_renderização`  | Exibir rascunhos?                                                                                                                                  | `Falso`      |
| `mídia_de_imagem_post`       | Ativar a Pasta de [Ativos](asset-folders.html)?                                                                                                    | `Falso`      |
| `link_relativa`              | Tornar links relativos à pasta raiz?                                                                                                               | `Falso`      |
| `futuro`                     | Mostrar postagens futuras?                                                                                                                         | `verdadeiro` |
| `Destaque`                   | Configurações de destaque de sintaxe de bloco de código, consulte [Highlight.js](/docs/syntax-highlight#Highlight-js) seção para obter guia de uso |              |
| `prismjs`                    | Configurações de destaque de sintaxe de bloco de código, consulte a seção [PrismJS](/docs/syntax-highlight#PrismJS) para obter o guia de uso       |              |

### Configuração da página inicial

| Configuração                     | Descrição:                                                                                                           | Padrão   |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- |
| `gerador_índice`                 | Gerar um arquivo de mensagens, alimentado por [hexo-generator-index](https://github.com/hexojs/hexo-generator-index) |          |
| `gerador_indexator.path`         | Caminho raiz para a página do seu blog                                                                               | `''`     |
| `gerador_índice.per_página`      | Publicações exibidas por página.                                                                                     | `10`     |
| `gerador_index.order_por`        | Ordem das publicações. Ordenar por data decrescente (nova para antiga) por padrão.                                   | `-data`  |
| `gerador_gerador.pagination_dir` | Formato da URL, consulte a configuração [Paginação](#Pagination) abaixo                                              | `Página` |

### Categoria & Tag

| Configuração       | Descrição:                       | Padrão            |
| ------------------ | -------------------------------- | ----------------- |
| `categoria_padrão` | Categoria padrão                 | `descategorizado` |
| `categoria_mapa`   | Sobrescrever slugs de categorias |                   |
| `marca_mapa`       | Sobrescrever slugs de etiquetas  |                   |

Exemplos:

``` yaml
category_map:
  "Pensamentos de ontem": ontem-pensamentos
  "C++": c-plus-plus
```

### Formato Data / Hora

Hexo usa [Moment.js](http://momentjs.com/) para datas de processo.

| Configuração       | Descrição:                                                                                               | Padrão       |
| ------------------ | -------------------------------------------------------------------------------------------------------- | ------------ |
| `formato_da_data`  | Formato da Data                                                                                          | `AAAA-MM-DD` |
| `formato_de_tempo` | Formato da hora                                                                                          | `HH:mm:ss`   |
| `opção_atualizada` | O valor [`atualizou`](/docs/variables#Page-Variables) a ser usado quando não é fornecido no front-matter | `mtime`      |

{% note info updated_option %}
U`updated_option` controla o valor `atualizado` quando não for fornecido no front-matter:

- `mtime`: Usar data de modificação de arquivo como `atualizado`. É o comportamento padrão do Hexo desde 3.0.0
- `date`: usar `date` como `atualizado`. Normalmente usado com fluxo de trabalho Git quando data de modificação de arquivo pode ser diferente.
- `vazio`: Simplesmente solte `atualizado` quando não fornecido. Pode não ser compatível com a maioria dos temas e plugins.

`use_date_for_updated` está obsoleto e será removido na próxima versão principal. Por favor, use `updated_option: 'date'`.
{% endnote %}

### Paginação

| Configuração          | Descrição:                                                          | Padrão   |
| --------------------- | ------------------------------------------------------------------- | -------- |
| `por_página`          | Número de postagens exibidas em cada página. `0` desativa paginação | `10`     |
| `diretório_paginação` | Formato URL                                                         | `Página` |

Exemplos:

``` yaml
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/awesome-pagine/2
```

### Extensões

| Configuração        | Descrição:                                                                                                                          |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `Tema`              | Nome do tema `false` desativa tema                                                                                                  |
| `configuração_tema` | Configuração do tema. Inclua qualquer configuração personalizada de tema nesta chave para substituir o tema padrão.                 |
| `implantar`         | Configurações de implantação                                                                                                        |
| `meta_generator`    | [Meta generator](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes) tag. `false` desativa a injeção da tag. |

### Incluir/Excluir Arquivos ou Pastas

Use as seguintes opções para processar explicitamente ou ignorar certos arquivos/pastas. Apoie [expressões glob](https://github.com/micromatch/micromatch#extended-globbing) para encontrar o caminho correspondente.

`incluir` e `excluir` opções apenas se aplicam à pasta `fonte/` , enquanto a opção `ignorar` aplica-se a todas as pastas.

| Configuração | Descrição:                                                                                                     |
| ------------ | -------------------------------------------------------------------------------------------------------------- |
| `incluir`    | Inclua arquivos ocultos (incluindo arquivos/pastas com um nome que comece com um sublinhado, com uma exceção*) |
| `Excluir`    | Excluir arquivos/pastas                                                                                        |
| `ignorar`    | Ignorar arquivos/pastas                                                                                        |

Exemplos:

```yaml
# Incluir/Excluir Arquivos/Pastas
incluem:
  - ".nojekyll"
  # Incluir 'source/css/_typing.css'.
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

Em vez de criar um tema, e manter uma versão personalizada com suas configurações, você pode configurá-lo em outro lugar:

**de `theme_config` no arquivo de configuração principal do site**

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

**de um arquivo `_config.[theme].yml` dedicado**

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
Recomendamos fortemente que você armazene sua configuração de tema em um só lugar. But in case you have to store your theme configuration separately, you need to know the priority of those configurations: The `theme_config` inside site's primary configuration file has the highest priority during merging, then the dedicated theme configuration file. O arquivo `_config.yml` sob o diretório do tema tem a menor prioridade.
{% endnote %}
