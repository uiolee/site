---
title: Temas
---

O `hexo.theme` herda de [Box](box.html) e também guarda os templates.

## Obter uma View

``` js
hexo.theme.getView(path);
```

## Definir uma View

``` js
hexo.theme.setView(caminho, dados);
```

## Remover uma View

``` js
hexo.theme.removeView(path);
```

## Visualizar

As Views têm dois métodos: `render` e `renderSync`. Esses dois métodos são idênticos, mas o primeiro é assíncrono e o segundo é síncrono. Por uma questão de simplicidade, só discutiremos `render` aqui.

``` js
var view = hexo.theme.getView('layout.swig');

view.render({foo: 1, bar: 2}).then(function(result){
  // ...
});
```

Você pode passar opções para o método `render` e ele tentará processar o template com o renderizador correspondente e carregar os [helpers](helper.html). Quando a renderização estiver completa, ele tentará descobrir se existe um layout. Se `layout` for `false` ou se não existir, o resultado será retornado diretamente.
