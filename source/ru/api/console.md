---
title: Консоль
---

Консоль служит для взаимодействия пользователей с Hexo. Регистрирует и описывает доступные консольные команды.

## Краткий обзор

``` js
hexo.extend.console.register(name, desc, options, function(args){
  // ...
});
```

| Аргумент | Описание |
| -------- | -------- |
| `имя`    | Имя      |
| `desc`   | Описание |
| `опции`  | Опции    |

Значение из аргумента `args` передаётся в функцию. Свойство описывает вводимые через терминал данные. Анализируется с помощью [Minimist][].

## Опции

### использование

Добавление используемых команд в консоль. Например:

``` js
{usage: '[layout] <title>'}
// hexo new [layout] <title>
```

### аргументы

Описание аргументов в консоли. Например:

``` js
{
  аргументы: [
    {name: 'layout', desc: 'Post layout'},
    {name: 'title', desc: 'Post title'}
  ]
}
```

### опции

Описание опций в консоли. Например:

``` js
{
  options: [
    {name: '-r, --replace', desc: 'Replace existing files'}
  ]
}
```

### desc

Подробная информация о консольной команде.

## Пример

``` js
hexo.extend.console.register('config', 'Display configuration', function(args){
  console.log(hexo.config);
});
```

[Minimist]: https://github.com/minimistjs/minimist
