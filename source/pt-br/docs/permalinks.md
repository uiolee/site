---
title: Permalinks
---

Você pode especificar os permalinks do seu site em `_config.yml` ou no front-matter para cada post.

### Variáveis

Além das seguintes variáveis, você pode usar qualquer atributo no permalink.

| Variável       | Descrição:                                                                          |
| -------------- | ----------------------------------------------------------------------------------- |
| `:year`        | Ano de postagens publicado (4-dígito)                                               |
| `:month`       | Mês das postagens publicadas (2-dígito)                                             |
| `:i_mês`       | Mês publicado de publicações (sem zeros à esquerda)                                 |
| `:day`         | Dia das postagens publicadas (2-dígito)                                             |
| `:i_dia`       | Dia das postagens publicado (sem zeros à esquerda)                                  |
| `:hora`        | Hora de publicação de postagens (2-dígito)                                          |
| `:minuto`      | Minuto publicado das postagens (2-dígito)                                           |
| `:segundo`     | Segunda postagem publicada (2-dígito)                                               |
| `:title`       | Nome do arquivo (relativo à pasta "source/_posts/")                                 |
| `:name`        | Nome                                                                                |
| `:post_titulo` | Título da postagem                                                                  |
| `:id`          | ID do post (_não persistente no cache de [reset](/docs/commands#clean)_)            |
| `:categoria`   | Categorias. Se o post for descategorizado, ele usará o valor de `default_category`. |
| `:hash`        | Hash SHA1 de nome de arquivo (o mesmo que `:title`) e data (12-hexadecimal)         |

Você pode definir o valor padrão de cada variável no permalink através da configuração `permalink_defaults`:

``` yaml
permalink_defaults:
  lang: pt-BR
```

### Exemplos

``` yaml source/_posts/hello-world.md
title: Olá, World
date: 2013-07-14 17:01:34
categorias:
- foo
- barra
```

| Configuração                    | Resultado                   |
| ------------------------------- | --------------------------- |
| `:ano/:mês/:day/:title/`        | 2013/07/14/hello-world/     |
| `:year-:month-:day-:title.html` | 2013-07-14-hello-world.html |
| `:category/:title/`             | foo/barra/hello-world/      |
| `:title-:hash/`                 | hello-world-a2c8ac003b43/   |

``` yaml source/_posts/lorem/hello-world.md
title: Olá, World
date: 2013-07-14 17:01:34
categorias:
- foo
- barra
```

| Configuração             | Resultado                     |
| ------------------------ | ----------------------------- |
| `:ano/:mês/:day/:title/` | 2013/07/14/lorem/hello-world/ |
| `:ano/:mês/:day/:name/`  | 2013/07/14/hello-world/       |

### Suporte a Multi-Idiomas

Para criar um site com vários idiomas, você pode modificar as configurações `new_post_name` e `permalink` assim:

``` yaml
new_post_name: :lang/:title.md
permalink: :lang/:title/
```

Quando você criar uma nova publicação, a postagem será salva em:

``` bash
$ hexo new "Hello World" --lang tw
# => source/_posts/tw/Hello-World.md
```

e a URL será:

``` plain
http://localhost:4000/tw/hello-world/
```
