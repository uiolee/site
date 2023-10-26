---
title: Ajudante
---

Um helper facilita a adição de snippets (trechos de código) aos seus templates. Recomendamos usar helpers em vez de templates quando estiver lidando com código mais complicado.

Os Helpers não podem ser acessados nos arquivos de `source`.

## Resumo

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

### Onde pôr um helper personalizado?

Coloque-o na pasta `scripts/` ou `temas/<yourtheme>/scripts/`.

### Como faço para usar outro auxiliar registrado no meu ajudante personalizado?

Todos os auxiliares são executados no mesmo contexto. Por exemplo, para usar [`url_for()`](/docs/helpers#url-for) dentro de um auxiliar personalizado:

``` js
hexo.extend.helper.register('lorem', function(path) {
  return '<script src="' + this.url_for(path) + '"></script>';
});
```

### Como usar um auxiliar registrado em outra extensão (por exemplo, Filtro, Injetor)?

`hexo.extend.helper.get` retornará a função auxiliar, mas ela precisa ter o hexo como seu contexto, a:

``` js
const url_for = hexo.extend.helper.get('url_for').bind(hexo);
```
