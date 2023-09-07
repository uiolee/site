---
title: Temas
---

`hexo.theme` herda de [Box](box.html), e também salva modelos.

## Obtenha uma visualização

``` js
hexo.theme.getView(path);
```

## Definir uma visualização

``` js
hexo.theme.setView(caminho, dados);
```

## Remover uma visualização

``` js
hexo.theme.removeView(path);
```

## Visualizar

Views tem dois métodos: `render` e `renderSync`. Estes dois métodos são idênticos, mas o primeiro é assíncrono e o segundo é síncrono. So for the sake of simplicity, we will only discuss `render` here.

``` js
var view = hexo.theme.getView('layout.swig');

view.render({foo: 1, bar: 2}).then(function(result){
  // ...
});
```

Você pode passar opções para o método `render` e ele tentará processar o template com o renderizador correspondente e carregar os auxiliares [](helper.html). Quando a renderização estiver concluída, ela tentará descobrir se um layout existe. Se `layout` é `false` ou se não existir, o resultado será retornado diretamente.
