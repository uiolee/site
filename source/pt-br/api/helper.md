---
title: Ajudante
---

Um ajudante facilita a adição rápida de trechos nos seus modelos. Recomendamos usar ajudantes em vez de templates quando você está lidando com código mais complicado.

Helpers can not be accessed from `source` files.

## Sinopse

``` js
hexo.extend.helper.register(name, function(){
  // ...
});
```

## Exemplo

``` js
hexo.extend.helper.register('js', function(path){
  return '<script src="' + path + '"></script>';
});
```

``` js
<%- js('script.js') %>
// <script src="script.js"></script>
```

## Perguntas Frequentes

### Onde colocar o helper personalizado?

Coloque-o na pasta `scripts/` ou `temas/<yourtheme>/scripts/`.

### Como faço para usar outro auxiliar registrado no meu ajudante personalizado?

Todos os auxiliares são executados no mesmo contexto. Por exemplo, para usar [`url_for()`](/docs/helpers#url-for) dentro de um auxiliar personalizado:

``` js
hexo.extend.helper.register('lorem', function(path) {
  return '<script src="' + this.url_for(path) + '"></script>';
});
```

### Como usar um auxiliar registrado em outra extensão (por exemplo, Filtro, Injetor, etc)?

`hexo.extend.helper.get` retornará a função auxiliar, mas ela precisa ter o hexo como seu contexto, a:

``` js
const url_for = hexo.extend.helper.get('url_for').bind(hexo);
```
