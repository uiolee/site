---
title: Тег
---

Тег позволяет легко и быстро вставлять фрагменты в свои посты.

## Краткий обзор

``` js
hexo.extend.tag.register(name, function(args, content){
  // ...
}, опции);
```

В функцию тега передаются два аргумента: `args` и `content`. `args` содержит аргументы, передаваемые плагину. `content` оборачивается содержанием с помощью плагина тега.

С момента введения в асинхронное отображение Hexo 3 использует [Nunjucks][] для обработки. Его поведение несколько отличается от применяемого в [Swig][].

## Отменить регистрацию тегов

Используйте `unregister()` для замены существующих плагинов [тегов](/docs/tag-plugins) пользовательскими функциями.

``` js
hexo.extend.tag.unregister(имя);
```

**Пример**

``` js
const tagFn = (args, content) => {
  content = 'something';
  return content;
};

// https://hexo.io/docs/tag-plugins#YouTube
hexo.extend.tag.unregister('youtube');

hexo.extend.tag.register('youtube', tagFn);
```

## Опции

### концы

Использовать закрывающие теги. По умолчанию установлено в `false`.

### асинхр

Включает асинхронный режим. По умолчанию установлено в `false`.

## Примеры

### Без закрывающих тегов

Вставка видео с YouTube.

``` js
hexo.extend.tag.register('youtube', function(args){
  var id = args[0];
  return '<div class="video-container"><iframe width="560" height="315" src="http://www.youtube.com/embed/' + id + '" frameborder="0" allowfullscreen></iframe></div>';
});
```

### С закрывающими тегами

Вставка цитаты.

``` js
hexo.extend.tag.register('pullquote', function(args, content){
  var className = args.join(' );
  return '<blockquote class="pullquote' + className + '">' + content + '</blockquote>';
}, {ends: true});
```

### Асинхронная обработка

Вставка файла.

``` js
var fs = require('hexo-fs');
var pathFn = require('path');

hexo.extend.tag. egister('include_code', function(args){
  var filename = args[0];
  var path = pathFn.join(hexo. ource_dir, имя файла);

  return fs.readFile(path). hen(function(content){
    return '<pre><code>' + content + '</code></pre>';
  });
}, {async: true});
```

## Витрина и конфигурация пользователя

Любой из следующих вариантов является допустимым:

1.

``` js
hexo.extend.tag. egister('foo', function (args) {
  const [firstArg] = args;

  // User config
  const { config } = hexo;
  const editor = config. uthor + firstArg;

  // Конфигурация темы
  const { config: themeCfg } = hexo. heme;
  if (themeCfg.fancybox) // do something...

  // фронт-материя
  const { title } = это; // артикул (post/page) заголовок

  // Содержание статьи
  const { _content } = this; // исходный контент
  const { content } = this; // HTML-отображенное содержимое

  return 'foo';
});
```

2.

``` js index.js
hexo.extend.tag.register('foo', require('./lib/foo')(hexo));
```

``` js lib/foo.js
модуль. xports = hexo => {
  return function fooFn(args) {
    const [firstArg] = args;

    const { config } = шестнадцатерично;
    const редактор = config. uthor + firstArg;

    const { config: themeCfg } = hexo.theme;
    if (themeCfg.fancybox) // do something...

    const { title, _content, content } = this;

    return 'foo';
  };
};
```

[Nunjucks]: https://mozilla.github.io/nunjucks/
[Swig]: https://node-swig.github.io/swig-templates/
