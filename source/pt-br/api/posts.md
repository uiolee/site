---
title: Postagens
---

## Criar uma postagem

``` js
hexo.post.create(data, replace);
```

| Argumento    | Descrição:                        |
| ------------ | --------------------------------- |
| `Dados`      | Dado                              |
| `substituir` | Substituir os arquivos existentes |

Os atributos de uma postagem podem ser definidos em `dados`. A tabela abaixo não é exaustiva. Atributos adicionais podem ser adicionados ao front-matter.

| Dado      | Descrição:                                                                                |
| --------- | ----------------------------------------------------------------------------------------- |
| `Título`  | Título                                                                                    |
| `eixo`    | URL:                                                                                      |
| `layout`  | Leiaute O padrão é a configuração `default_layout`.                                       |
| `caminho` | Caminho Hexo constrói o caminho do post com base na definição `new_post_path` por padrão. |
| `Data`    | Data. O padrão é a data atual.                                                            |

## Publicar um rascunho

``` js
hexo.post.publish(dados, substituir);
```

| Argumento    | Descrição:                        |
| ------------ | --------------------------------- |
| `Dados`      | Dado                              |
| `substituir` | Substituir os arquivos existentes |

Os atributos de uma postagem podem ser definidos em `dados`. A tabela abaixo não é exaustiva. Atributos adicionais podem ser adicionados ao front-matter.

| Dado     | Descrição:                                          |
| -------- | --------------------------------------------------- |
| `eixo`   | Nome do arquivo (obrigatório)                       |
| `layout` | Leiaute O padrão é a configuração `default_layout`. |

## Renderizar

``` js
hexo.post.render(fonte, dados);
```

| Argumento | Descrição:                                |
| --------- | ----------------------------------------- |
| `Fonte`   | Caminho completo de um arquivo (opcional) |
| `Dados`   | Dado                                      |

Os dados devem conter o atributo `content`. Se não, o Hexo tentará ler o arquivo original. Os passos de execução desta função são os seguintes:

- Executar filtros `before_post_render`
- Renderizar com Markdown ou outros renderizadores (dependendo do nome da extensão)
- Renderizar com [Nunjucks][]
- Executar `after_post_render` filtros

[Nunjucks]: https://mozilla.github.io/nunjucks/

