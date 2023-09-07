---
title: Variáveis Locais
---

Variáveis locais são usadas para a renderização de templates, que é a variável `site` nos templates.

## Variáveis padrão

| Variável      | Descrição:          |
| ------------- | ------------------- |
| `publicações` | Todas as postagens  |
| `páginas`     | Todas as páginas    |
| `Categorias`  | Todas as categorias |
| `Etiquetas`   | Todas as tags       |

## Obter uma Variável

``` js
hexo.locals.get('posts')
```

## Definir uma variável

``` js
hexo.locals.set('posts', function(){
  return ...
});
```

## Remover uma variável

``` js
hexo.locals.remove('posts');
```

## Obter todas as variáveis

``` js
hexo.locals.toObject();
```

## Invalidar o cache

``` js
hexo.locals.invalidate();
```
