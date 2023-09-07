---
title: Pastas de ativos
---

## Pasta global de ativos

Os assets são arquivos não-post na pasta `fonte` , como imagens, arquivos CSS ou JavaScript. Por exemplo, se você vai ter apenas algumas imagens no projeto Hexo, então o jeito mais fácil é mantê-los em um diretório `fonte/imagens`. Então, você pode acessá-los usando algo como `![](/images/image.jpg)`.

## Postar pasta do conteúdo

{% youtube feIDVQ2tz0o %}

Para usuários que esperam regularmente servir imagens e/ou outros ativos, e para aqueles que preferem separar seus ativos em uma base de post--post, o Hexo também fornece uma maneira mais organizada de gerenciar ativos. Isto está um pouco mais envolvido, mas uma abordagem muito conveniente para o gerenciamento de ativos pode ser ativada definindo a configuração `post_asset_folder` em `_config. ml` para true.

``` yaml _config.yml
pasta_de_post_asset: verdadeiro
```

Com o gerenciamento de pasta de ativos habilitado, Hexo vai criar uma pasta toda vez que você fizer uma nova postagem com o comando `hexo new [layout] <title>`. Esta pasta de ativos terá o mesmo nome que o arquivo markdown associado ao post. Coloque todos os arquivos relacionados ao seu post na pasta associada, e você poderá referenciá-los usando um caminho relativo, tornando um fluxo de trabalho mais fácil e mais conveniente.

## Plugins de tags para referência de caminho relativo

Referenciar imagens ou outros ativos usando a sintaxe markdown e caminhos relativos normais pode levar a uma exibição incorreta no arquivo ou páginas de índice. Plugins foram criados pela comunidade para resolver esse problema no Hexo 2. No entanto, com o lançamento do Hexo 3, vários novos plugins [tag](/docs/tag-plugins#Include-Assets) foram adicionados ao núcleo. Estes permitem que você faça referência a seus conteúdos mais facilmente em postagens:

```
{% asset_path slug %}
{% asset_img slug [title] %}
{% asset_link slug [title] %}
```

Por exemplo, com a pasta post asset habilitada, se você colocar uma imagem `exemplo. pg` em sua pasta de arquivos, ele não irá *nem* aparecer na página inicial se você o referenciar usando um caminho relativo com o normal `! ](exemplo. pg)` sintaxe markdown (entretanto, ela funcionará como esperado na própria publicação).

A maneira correta de fazer referência à imagem estará usando a sintaxe do plugin de tag em vez de markdown:

```
{% asset_img example.jpg This is an example image %}
{% asset_img "spaced asset.jpg" "spaced title" %}
```

Desta forma, a imagem será exibida tanto dentro do post quanto no índice e nas páginas de arquivo.

## Incorporando uma imagem usando markdown

[hexo-renderer-marked](https://github.com/hexojs/hexo-renderer-marked) 3.1.0 introduziu uma nova opção que permite incorporar uma imagem em markdown sem usar o plugin de tag `asset_img`.

Para ativar:

``` yml _config.yml
post_asset_folder: verdadeiro
marcado:
  prependRoot: verdadeiro
  postAsset: verdadeiro
```

Uma vez ativado, uma imagem do asset será automaticamente resolvida para o caminho do post correspondente. Por exemplo, "image.jpg" está localizado em "/2020/01/02/foo/image.jpg", ou seja, é uma imagem de ativo de "/2020/01/02/foo/", `![](image pg)` será renderizado como `<img src="/2020/01/02/foo/image.jpg">`.
