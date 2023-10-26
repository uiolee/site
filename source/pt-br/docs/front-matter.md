---
title: Front-matter
---

{% youtube pfD6FCZdW4Q %}

Front-matter é um bloco de YAML ou JSON no início do arquivo que é usado para definir configurações para o conteúdo que será escrito (como páginas ou postagens). O Front-matter é terminado por três traços quando escrito em YAML ou três ponto e vírgula quando escrito em JSON.

**YAML**

``` yaml
---
título: Olá Mundo
data: 2013/7/13 20:46:25
---
```

**JSON**

``` json
"title": "Olá, mundo",
"date": "2013/7/13 20:46:25"
;;
```

### Configurações e Seus Valores Padrão

| Configuração          | Descrição                                                                                                      | Padrão                                                                                |
| --------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| `layout`              | Disposição                                                                                                     | [`config.default_layout`](/docs/configuration#Writing)                                |
| `Título`              | Título                                                                                                         | Nome do arquivo (apenas postagens)                                                    |
| `Data`                | Data de publicação                                                                                             | Data de criação do arquivo                                                            |
| `Atualizado`          | Data de atualização                                                                                            | Data de atualização do arquivo                                                        |
| `Comentários`         | Habilita o recurso de comentário para a postagem                                                               | `verdadeiro`                                                                          |
| `Etiquetas`           | Tags (Não disponível para páginas)                                                                             |                                                                                       |
| `Categorias`          | Categorias (Não disponível para páginas)                                                                       |                                                                                       |
| `permalink`           | Substitui o permalink padrão da postagem Permalink deve terminar com `/` ou `.html`                            | `nulo`                                                                                |
| `resumo`              | Resumo de página em texto simples. Usar [este plugin](/docs/tag-plugins#Post-Excerpt) para formatar o texto    |                                                                                       |
| `desabilitarNunjucks` | Desabilitar renderização da tag Nunjucks `{{ }}`/`{% %}` e [plugins de tags](/docs/tag-plugins) quando ativado | Falso                                                                                 |
| `lang`                | Definir o idioma para substituir [auto detecção](/docs/internationalization#Path)                              | Herdado de `_config.yml`                                                              |
| `Publicado`           | Se a postagem deve ser publicada                                                                               | Para postagens sob `_posts`, é `verdadeiro`, e para mensagens sob `_draft`, é `false` |

#### Disposição

The default layout is `post`, in accordance to the value of [`default_layout`]((/docs/configuration#Writing)) setting in `_config.yml`. Quando o layout é desativado (`layout: false`) em um artigo, ele não será processado com um tema. No entanto ele ainda será renderizado por qualquer renderizador disponível: se um artigo for escrito em Markdown e um renderizador Markdown (como o padrão [hexo-renderer](https://github.com/hexojs/hexo-renderer-marked)) estiver instalado, será renderizado para HTML.

[Plugins de tags](/docs/tag-plugins) são sempre processados independentemente do layout, a menos que esteja desabilitado pelo `disableNunjucks` setting ou [renderer](/api/renderer#Disable-Nunjucks-tags).

#### Categorias & Tags

Somente postagens aceitam o uso de categorias e tags. As categorias aplicam-se à postagens em ordem, resultando em uma hierarquia de classificações e subclassificações. As tags são todas definidas no mesmo nível hierárquico, de modo que a ordem em que aparecem não é importante.

**Exemplo**

``` yaml
categorias:
- Esportes
- Baseball
tags:
- Lesões
- Lute contra
- Eletrificado
```

Se você quiser aplicar várias hierarquias de categorias, use uma lista de nomes em vez de um único nome. Se o Hexo encontar qualquer categoria definida dessa forma em uma postagem, ele tratará cada categoria para essa postagem com sua própria hierarquia independente.

**Exemplo**

``` yaml
categorias:
- [Esportes, Baseball]
- [MLB, Liga Americana, Boston Red Sox]
- [MLB, Liga Americana, Nova Iorque]
- Rivalries
```
