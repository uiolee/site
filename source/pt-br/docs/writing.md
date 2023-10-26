---
title: Escrevendo
---

{% youtube AIqBubK6ZLc %}

Para criar uma nova postagem ou uma nova página, você pode rodar o seguinte comando:

``` bash
$ hexo novo [layout] <title>
```

O `layout` padrão é o `post`, mas você pode fornecer o seu próprio. Você pode alterar o layout padrão editando a configuração `default_layout` em `_config.yml`.

## Disposição

Existem três layouts padrões no Hexo: `post`, `page` e `draft`. Os arquivos criados por cada um deles são salvos em um caminho diferente. As postagens criadas recentemente são salvas no diretório `source/_posts`.

| Disposição   | Caminho             |
| ------------ | ------------------- |
| `publicação` | `origem/_postagens` |
| `Página`     | `Fonte`             |
| `rascunho`   | `rascunhos/origem`  |

{% note tip Disabling layout %}
Se você não quer que um artigo (post/página) seja processado com um tema, defina `layout: false` em seu front-matter. Consulte [esta seção](/docs/front-matter#Layout) para obter mais detalhes.
{% endnote %}

## Nome de Arquivo

Por padrão, o Hexo usa o título da postagem como seu nome de arquivo. Você pode editar a configuração `new_post_name` em `_config.yml` para alterar o nome do arquivo padrão. Por exemplo, `:year-:month-:day-:title.md` prefixará nomes de arquivos com a data de criação de postagem. Você pode usar os seguintes placeholders:

| Espaço reservado | Descrição                                                        |
| ---------------- | ---------------------------------------------------------------- |
| `:title`         | Título do post (minúsculas, com espaços substituídos por hifens) |
| `:year`          | Ano de criação, ex: `2015`                                       |
| `:month`         | Mês de criação (com zero à esquerda), ex: `04`                   |
| `:i_mês`         | Mês de criação (sem zero à esquerda), ex: `4`                    |
| `:day`           | Dia de criação (com zero à esquerda), ex: `07`                   |
| `:i_dia`         | Dia de criação (sem zero à esquerda), ex: `7`                    |

## Rascunhos

Anteriormente, mencionamos um layout especial no Hexo: `draft`. As postagens inicializadas com este layout são salvas no diretório `source/_drafts`. Você pode usar o comando `publish` para mover os rascunhos para o diretório `source/_posts`. O comando `publish` funciona de forma semelhante ao comando `new`.

``` bash
$ hexo publish [layout] <title>
```

Os rascunhos não são exibidos por padrão. Você pode adicionar a opção `--draft` ao executar o Hexo ou habilitar a configuração `render_drafts` em `_config.yml` para renderizar rascunhos.

## Andaimes

Ao criar postagens, o Hexo irá construir arquivos com base no arquivo correspondente no diretório `scaffolds`. Por exemplo:

``` bash
$ nova foto hexo "Minha Galeria"
```

Quando você executa este comando, o Hexo tentará encontrar `photo.md` no diretório `scaffolds` e criar a postagem com base nele. Os seguintes placeholders estão disponíveis em scaffolds:

| Espaço reservado | Descrição                  |
| ---------------- | -------------------------- |
| `layout`         | Disposição                 |
| `Título`         | Título                     |
| `Data`           | Data de criação do arquivo |

## Formatos suportados

Hexo suporta postagens escritas em qualquer formato, desde que o plugin de renderização correspondente esteja instalado.

Por exemplo, Hexo possui `hexo-renderer-marked` e `hexo-renderer-ejs` instalado por padrão, para que você possa escrever suas postagens em `markdown` ou em `ejs`. Se você tiver o `hexo-renderer-pug` instalado, então você pode até mesmo escrever seu post no idioma pug.

Você pode renomear as suas postagens e mudar para a extensão de arquivo de `.md` para `. js`, então Hexo usará `hexo-renderer-ejs` para renderizar esse arquivo, assim como os outros formatos.
