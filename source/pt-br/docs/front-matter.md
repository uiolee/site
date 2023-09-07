---
title: Front-matter
---

{% youtube pfD6FCZdW4Q %}

Front-matter é um bloco de YAML ou JSON no início do arquivo que é usado para configurar as configurações de seus escritos. Front-matter é rescindido por três traços quando escritos em YAML ou três ponto-e-vírgulas quando escritos em JSON.

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

### Configurações & Seus Valores Padrão

| Configuração          | Descrição:                                                                                                     | Padrão                                                 |
| --------------------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `layout`              | Disposição                                                                                                     | [`config.default_layout`](/docs/configuration#Writing) |
| `Título`              | Título                                                                                                         | Nome do arquivo (apenas postagens)                     |
| `Data`                | Data de publicação                                                                                             | Data de criação                                        |
| `Atualizado`          | Data de atualização                                                                                            | Data de atualização                                    |
| `Comentários`         | Habilita o comentário na postagem                                                                              | verdadeiro                                             |
| `Etiquetas`           | Tags (não disponíveis para páginas)                                                                            |                                                        |
| `Categorias`          | Categorias (não disponível para páginas)                                                                       |                                                        |
| `permalink`           | Sobrescreve o link padrão do post. Permalink deve terminar com `/` ou `.html`                                  | `nulo`                                                 |
| `resumo`              | Resumo de página em texto simples. Usar [este plugin](/docs/tag-plugins#Post-Excerpt) para formatar o texto    |                                                        |
| `desabilitarNunjucks` | Desabilitar renderização da tag Nunjucks `{{ }}`/`{% %}` e [plugins de tags](/docs/tag-plugins) quando ativado | Falso                                                  |
| `lang`                | Definir o idioma para substituir [auto detecção](/docs/internationalization#Path)                              | Herdado de `_config.yml`                               |

#### Disposição

O layout padrão é `post`, de acordo com o valor de [`default_layout`](/docs/configuration#Writing) definição em `_config.yml`. Quando o layout é desativado (`layout: false`) em um artigo, ele não será processado com um tema. No entanto ele ainda será renderizado por qualquer renderizador disponível: se um artigo for escrito em Markdown e um renderizador Markdown (como o padrão [hexo-renderer](https://github.com/hexojs/hexo-renderer-marked)) estiver instalado, será renderizado para HTML.

[Plugins de tags](/docs/tag-plugins) são sempre processados independentemente do layout, a menos que esteja desabilitado pelo `disableNunjucks` setting ou [renderer](/api/renderer#Disable-Nunjucks-tags).

#### Categorias & Etiquetas

Somente os posts suportam o uso de categorias e tags. Categorias se aplicam às postagens em ordem, resultando numa hierarquia de classificações e subclassificações. Etiquetas são todas definidas no mesmo nível hierárquico e por isso a ordem em que aparecem não é importante.

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

Se você quiser aplicar múltiplas hierarquias de categorias, use uma lista de nomes ao invés de um único nome. Se o Hexo vir qualquer categoria definida desta forma em uma publicação, tratará cada categoria da publicação como sua própria hierarquia independente.

**Exemplo**

``` yaml
categorias:
- [Esportes, Baseball]
- [MLB, Liga Americana, Boston Red Sox]
- [MLB, Liga Americana, Nova Iorque]
- Rivalries
```
