---
title: Рендер
---

Рендер используется для создания содержимого.

## Краткий обзор

``` js
hexo.extend.renderer.register(name, output, function(data, options){
  // ...
}, синхронизация);
```

| Аргумент        | Описание                                                              |
| --------------- | --------------------------------------------------------------------- |
| `имя`           | Вводится расширение входного файла (нижний регистр, без ведущей `.`)  |
| `вывод`         | Выводится расширение входного файла (нижний регистр, без ведущей `.`) |
| `синхронизация` | Режим синхронизации                                                   |

В функцию рендера передаются два аргумента:

| Аргумент   | Описание                                                                                                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------ |
| `данные`   | Включает два атрибута: путь к файлу `path` и содержимое файла  `text`. Переменная `path` не является обязательной. |
| `опция`    | Опции                                                                                                              |
| `callback` | Функция обратного вызова двух параметров `err`, `value`.                                                           |

## Пример

### Асинхронный режим

``` js
var stylus = require('stylus');

// Обратный вызов
hexo.extend.renderer.register('styl', 'css', function(data, options, callback){
  stylus(data.text).set('filename', data.path).render(callback);
});

// Запрос
hexo.extend.renderer.register('styl', 'css', function(data, options){
  return new Promise(function(resolve, reject){
    resolve('test');
  });
});
```

### Синхронный режим

``` js
var ejs = require('ejs');

hexo.extend.renderer.register('ejs', 'html', function(data, options){
  options.filename = data.path;
  return ejs.render(data.text, options);
}, true);
```

### Отключить теги Nunjucks

Nunjucks теги `{{ }}` или `{% %}` (используемые [плагином тегов](/docs/tag-plugins)) обрабатываются по умолчанию, для отключения:

``` js
function lessFn(data, options) {
  // do something
}

lessFn.disableNunjucks = true

hexo.extend.renderer.register('less', 'css', lessFn);
```
