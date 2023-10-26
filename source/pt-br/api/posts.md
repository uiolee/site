---
title: Postagens
---

## Criar uma Postagem

``` js
hexo.post.create(data, replace);
```

| Argumento    | Descrição                     |
| ------------ | ----------------------------- |
| `Dados`      | Dados                         |
| `substituir` | Substitui arquivos existentes |

Os atributos de uma postagem podem ser definidos em `data`. A tabela abaixo inclui as informações mais importantes. Atributos adicionais podem vir a ser adicionados no front-matter.

| Dado      | Descrição                                                                                             |
| --------- | ----------------------------------------------------------------------------------------------------- |
| `Título`  | Título                                                                                                |
| `eixo`    | URL:                                                                                                  |
| `layout`  | Leiaute Usa a configuração `default_layout` como padrão.                                              |
| `caminho` | Caminho. Por padrão, o Hexo constrói o caminho da postagem de acordo com a definição `new_post_path`. |
| `Data`    | Data. Utiliza a data atual como padrão.                                                               |

## Publicar um Rascunho

``` js
hexo.post.publish(dados, substituir);
```

| Argumento    | Descrição                     |
| ------------ | ----------------------------- |
| `Dados`      | Dados                         |
| `substituir` | Substitui arquivos existentes |

Os atributos de uma postagem podem ser definidos em `data`. A tabela abaixo inclui as informações mais importantes. Atributos adicionais podem vir a ser adicionados no [front-matter](front-matter.html).

| Dados    | Descrição                                             |
| -------- | ----------------------------------------------------- |
| `eixo`   | Nome do arquivo (Campo obrigatório)                   |
| `layout` | Leiaute Usa a definição `default_layout` como padrão. |

## Renderizar

``` js
hexo.post.render(fonte, dados);
```

| Argumento | Descrição                                 |
| --------- | ----------------------------------------- |
| `Fonte`   | Caminho completo de um arquivo (Opcional) |
| `Dados`   | Dados                                     |

O argumento `data` deve conter o atributo `content`. Caso não inclua, o Hexo tentará carregar o arquivo inicial. As etapas de execução dessa função são listadas abaixo:

- Executa os filtros de `before_post_render`
- Renderiza utilizando Markdown ou outros renderizadores (dependendo da extensão do arquivo)
- Renderiza utilizando [Nunjucks][]
- Executa os filtros de `after_post_render`

[Nunjucks]: https://mozilla.github.io/nunjucks/

