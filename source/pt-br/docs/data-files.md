---
title: Arquivos de dados
---

Às vezes, você pode precisar usar alguns dados em templates que não estão diretamente disponíveis nas suas publicações, ou você deseja reutilizar os dados em outro lugar. Para tais casos de uso, o Hexo 3 introduziu os novos arquivos **Dados**. Esse recurso carrega arquivos YAML ou JSON na pasta `source/_data` para que você possa usá-los no seu site.

{% youtube CN31plHbI-w %}

Por exemplo, adicione o `menu.yml` na pasta `source/_data`.

``` yaml
Casa: /
Galeria: /gallery/
Arquivos: /archives/
```

E você pode usá-los nos templates:

```
<% for (var link in site.data.menu) { %>
  <a href="<%= site.data.menu[link] %>"> <%= link %> </a>
<% } %>
```

renderizar assim:

```
<a href="/"> Casa </a>
<a href="/gallery/"> Galeria </a>
<a href="/archives/"> Arquiva </a>
```
