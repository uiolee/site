---
title: Escrevendo
---

{% youtube AIqBubK6ZLc %}

Para criar uma nova postagem ou uma nova página, você pode executar o seguinte comando:

``` bash
$ hexo novo [layout] <title>
```

`post` é o padrão `layout`, mas você pode fornecer o seu próprio. Você pode alterar o layout padrão editando a configuração `default_layout` em `_config.yml`.

## Disposição

Existem três layouts padrão no Hexo: `postar`, `página` e `rascunho`. Arquivos criados por cada um deles são salvos em um caminho diferente. Posts recém-criados são salvos na pasta `fonte/_posts`.

| Disposição   | Caminho             |
| ------------ | ------------------- |
| `publicação` | `origem/_postagens` |
| `Página`     | `Fonte`             |
| `rascunho`   | `rascunhos/origem`  |

{% note tip Disabling layout %}
Se você não quer que um artigo (post/página) seja processado com um tema, defina `layout: false` em seu front-matter. Consulte [esta seção](/docs/front-matter#Layout) para obter mais detalhes.
{% endnote %}

## Nome

Por padrão, o Hexo usa o título do post como seu nome de arquivo. Você pode editar a configuração `new_post_name` em `_config.yml` para alterar o nome de arquivo padrão. Por exemplo, `:year-:month-:day-:title.md` irá prefixar nomes de arquivos com a data de criação do post. Você pode usar os seguintes placeholders:

| Espaço reservado | Descrição:                                                             |
| ---------------- | ---------------------------------------------------------------------- |
| `:title`         | Título da publicação (minúsculas, com espaços substituídos por hífens) |
| `:year`          | Ano criado, por exemplo, `2015`                                        |
| `:month`         | Created month (leading zeros), e.g. `04`                               |
| `:i_mês`         | Mês criado (sem zeros principais), por exemplo, `4`                    |
| `:day`           | Dia criado (zeros à curva), por exemplo, `07`                          |
| `:i_dia`         | Dia criado (sem zeros à liderança), por exemplo, `7`                   |

## Rascunhos

Anteriormente, mencionamos um layout especial no Hexo: `rascunho`. Posts inicializados com este layout são salvos na pasta `fonte/_drafts`. Você pode usar o comando `publish` para mover rascunhos para a pasta `source/_posts`. `publicar` funciona de uma maneira semelhante ao comando `new`.

``` bash
$ hexo publish [layout] <title>
```

Rascunhos não são exibidos por padrão. Você pode adicionar a opção `--draft` ao executar o Hexo ou habilitar a configuração `render_drafts` em `_config.yml` para renderizar rascunhos.

## Andaimes

Ao criar posts, o Hexo criará arquivos baseados no arquivo correspondente na pasta `scaffolds`. Por exemplo:

``` bash
$ nova foto hexo "Minha Galeria"
```

Quando você executar esse comando, Hexo tentará encontrar `foto. d` no diretório `scaffolds` e crie o post com base nele. Os seguintes espaços reservados estão disponíveis nos andaimes:

| Espaço reservado | Descrição:      |
| ---------------- | --------------- |
| `layout`         | Disposição      |
| `Título`         | Título          |
| `Data`           | Data de criação |

## Formatos suportados

Hexo suporta postagens escritas em qualquer formato, desde que o plugin de renderização correspondente esteja instalado.

Por exemplo, Hexo possui `hexo-renderer-marked` e `hexo-renderer-ejs` instalado por padrão, para que você possa escrever suas postagens em `markdown` ou em `ejs`. Se você tiver o `hexo-renderer-pug` instalado, então você pode até mesmo escrever seu post no idioma pug.

Você pode renomear as suas postagens e mudar para a extensão de arquivo de `.md` para `. js`, então Hexo usará `hexo-renderer-ejs` para renderizar esse arquivo, assim como os outros formatos.
