---
title: Etiqueta
---

Uma tag permite que os usuários insiram, de forma rápida e fácil, snippets (trechos de código) dentro de suas postagens.

## Resumo

``` js
hexo.extend.tag.register(name, function(args, content){
  // ...
}, opções);
```

Dois argumentos serão passados para dentro da função: `args` e `content`. `args` contém os argumentos passados para o tag plugin e `content` é o conteúdo envolvido do tag plugin.

Desde a introdução da renderização assíncrona, na versão 3 do Hexo, estamos usando o [Nunjucks][] para renderização. O comportamento pode ser um pouco diferente do [Swig][].

## Desregistrar tags

Use `unregister()` para substituir plugins de tags [existentes](/docs/tag-plugins) por funções personalizadas.

``` js
hexo.extend.tag.unregister(nome);
```

**Exemplo**

``` js
const tagFn = (args, content) => {
  content = 'algo';
  return content;
};

// https://hexo.io/docs/tag-plugins#YouTube
hexo.extend.tag.unregister('youtube');

hexo.extend.tag.register('youtube', tagFn);
```

## Opções

### Termina

Use as tags end. Esta opção é `false` por padrão.

### assíncrono

Habilite o modo assíncrono. Esta opção é `false` por padrão.

## Exemplos

### Sem a Tag End

Insira um vídeo do Youtube.

``` js
hexo.extend.tag.register('youtube', function(args){
  var id = args[0];
  return '<div class="video-container"><iframe width="560" height="315" src="http://www.youtube.com/embed/' + id + '" frameborder="0" allowfullscreen></iframe></div>';
});
```

### Com a Tag End

Insira uma citação.

``` js
hexo.extend.tag.register('pullquote', function(args, content){
  var className = args.join(' ');
  return '<blockquote class="pullquote' + className + '">' + content + '</blockquote>';
}, {ends: true});
```

### Renderização Assíncrona

Insira um arquivo.

``` js
var fs = require('hexo-fs');
var pathFn = require('path');

hexo.extend.tag. egister('include_code', function(args){
  var filename = args[0];
  var path = pathFn.join(hexo. ource_dir, filename);

  return fs.readFile(path). hen(function(content){
    return '<pre><code>' + content + '</code></pre>';
  });
}, {async: true});
```

## Configuração Front-matter e do usuário

Qualquer uma das seguintes opções é válida:

1.

``` js
tag.hex.extend. egister('foo', function (args) {
  const [firstArg] = args;

  // Configuração do usuário
  const { config } = hexo;
  const editor = config. uthor + firstArg;

  // Configuração do tema
  const { config: themeCfg } = hexo. hemo;
  if (themeCfg.fancybox) // fazer algo...

  // Front-matter
  const { title } = this; // article's (post/page) title

  // Article's content
  const { _content } = this; // original content
  const { content } = this; // HTML-rendered content

  return 'foo';
});
```

2.

``` js index.js
hexo.extend.tag.register('foo', require('./lib/foo')(hexo));
```

``` js lib/foo.js
Módulo xports = hexo => {
  retorna a função fooFn(args) {
    const [firstArg] = args;

    const { config } = hexo;
    const editor = config. uthor + primeiro;

    const { config: themeCfg } = hexo.theme;
    if (themeCfg.fancybox) // fazer algo...

    const { title, _content, content } = this;

    return 'foo';
  };
};
```

[Nunjucks]: https://mozilla.github.io/nunjucks/
[Swig]: http://paularmstrong.github.io/swig/
