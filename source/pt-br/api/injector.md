---
title: Injetor
---

Um injetor é usado para adicionar trecho de código estático ao `<head>` ou/and `<body>` dos arquivos HTML gerados. Hexo executar injetor **antes do filtro** `after_render:html` ser executado.

## Resumo

```js
hexo.extend.injector.register(entrada, valor, to)
```

### entrada `<string>`

Onde o código será injetado dentro do HTML.

Apoie esses valores:

- `head_start`: Código de injeta logo após `<head>` (Padrão).
- `head_end`: Código de injeta antes de `</head>`.
- `body_begin`: Código de injeta logo após `<body>`.
- `body_end`: Código de injeção antes de `</body>`.

### valor `<string> ├ <Function>`

> Uma função que retorna string é suportada.

O trecho de código a ser injetado.

### para `<string>`

Qual página irá codificar snippets sendo injetados.

- `padrão`: Injetar para cada página (Padrão).
- `home`: Apenas injetar na página inicial (que possui `is_home()` helper sendo `true`)
- `post`: Apenas injetar nas páginas do post (que tem `is_post()` ajudante sendo `true`)
- `página`: Apenas injetar nas páginas (que tem `is_page()` ajudante sendo `true`)
- `archive`: Apenas injeta para as páginas de arquivos (que possuem `is_archive()` helper sendo `true`)
- `Categoria`: Apenas injetar em páginas de categoria (que tem `is_category()` ajudante sendo `verdadeiro`)
- `tag`: Apenas injetar nas páginas de tags (que tem `is_tag()` ajuda sendo `true`)
- Custom layout name could be used as well, see [Writing - Layout](writing#Layout).

----

Existem outras funções internas, consulte [hexojs/hexo#4049](https://github.com/hexojs/hexo/pull/4049) para obter mais detalhes.

## Exemplo

```js
const css = hexo.extend.helper.get('css').bind(hexo);
const js = hexo.extend.helper.get('js').bind(hexo);

hexo.extend.injector.register('head_end', () => {
  return css('https://cdn.jsdelivr.net/npm/aplayer@1.10. /dist/APlayer.min.css');
}, 'music');

hexo.extend.injector.register('body_end', '<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js">', 'music');

hexo.extend.injector.register('body_end', () => {
  return js('/js/jquery.js');
});
```

Acima da configuração injetará `APlayer.min. ss` (`<link>` tag) para o `</head>` de qualquer página que o layout seja `música`, e `APlayer. in.js` (`<script>` tag) ao `</body>` dessas páginas. Além disso, o `jquery.js` (`<script>` tag) será injetado para `</body>` de cada página gerada.

## Acessando configuração do usuário

Use qualquer uma das seguintes opções:

1.

``` js
const css = hexo.extend.helper.get('css').bind(hexo);

hexo.extend.injector.register('head_end', () => {
  const { cssPath } = hexo.config.fooPlugin;
  return css(cssPath);
});
```

2.

``` js index.js
/* hexo global */

hexo.extend.injector.register('head_end', require('./lib/inject').bind(hexo))
```

``` js lib/inject.js
module.exports = function () {
  const css = this.extend.helper.get('css');
  const { cssPath } = this.config.fooPlugin;
  return css(cssPath);
}
```

``` js lib/inject.js
function injectFn() {
  const css = this.extend.helper.get('css');
  const { cssPath } = this.config.fooPlugin;
  return css(cssPath);
}

module.exports = injectFn;
```

3.

``` js index.js
/* hexo global */

hexo.extend.injector.register('head_end', require('./lib/inject')(hexo))
```

``` js lib/inject.js
module.exports = (hexo) => () => {
  const css = hexo.extend.helper.get('css').bind(hexo);
  const { cssPath } = hexo.config.fooPlugin;
  return css(cssPath);
};
```

``` js lib/inject.js
const injectFn = (hexo) => {
  const css = hexo.extend.helper.get('css').bind(hexo);
  const { cssPath } = hexo. onfig.fooPlugin;
  return css(cssPath);
};

module.exports = (hexo) => injectFn(hexo);
```
