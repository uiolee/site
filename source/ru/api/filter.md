---
title: Фильтры
---

Фильтры используются для изменения указанных данных. Hexo передает данные для фильтров в определенной последовательности и фильтров изменения данных один за другим. Эта концепция была заимствована из [WordPress](http://codex.wordpress.org/Plugin_API#Filters)

## Краткий обзор

``` js
hexo.extend.filter.register(type, function() {
  // User configuration
  const { config } = this;
  if (config.external_link.enable) // do something...

  // Конфигурация темы
  const { config: themeCfg } = this.theme;
  if (themeCfg.fancybox) // do something...

}, приоритет);
```

Вы можете определить приоритет. Низкий приоритет означает, что он будет выполняться в первую очередь. Приоритет по умолчанию равен 10. Рекомендуется использовать настраиваемое пользователем значение приоритета, которое возможно указать в конфигурации, например `hexo.config.your_plugin.priority`.

## Использование фильтров

``` js
hexo.extend.filter.exec(тип, данные, параметры);
hexo.extend.filter.execSync(тип, данные, параметры);
```

| Опция      | Описание                               |
| ---------- | -------------------------------------- |
| `контекст` | Контекст                               |
| `args`     | Аргументы. Должны быть в виде массива. |

Первый аргумент, передаваемый в каждый фильтр, это `data`. Данные `data`, передаваемые в следующий фильтр, могут быть изменены путем возврата нового значения. Если же ничего не возвращается, данные остаются без изменений. Вы даже можете использовать аргументы, чтобы указать другие аргументы в фильтрах. Например:

``` js
hexo.extend.filter. egister('test', функция(данные, arg1, arg2){
  // данные === 'some data'
  // arg1 === 'foo'
  // arg2 === 'bar'

  return 'something';
});

шестнадцатерично. xtend.filter.register('test', function(data, arg1, arg2){
  // data === 'something'
});

hexo. xtend.filter.exec('test', 'some data', {
  args: ['foo', 'bar']
});
```

Также можно использовать следующие методы для выполнения фильтров:

``` js
hexo.execFilter(тип, данные, параметры);
hexo.execFilterSync(тип, данные, параметры);
```

## Отмена фильтров

``` js
hexo.extend.filter.unregister(type, filter);
```

**Пример**

``` js
// Отменить фильтр, зарегистрированный с именованной функцией

const filterFn = (data) => {
  data = 'something';
  возврат данных;
};
шестнадцатерично. xtend.filter.register('example', filterFn);

hexo.extend.filter.unregister('example', filterFn);
```

``` js
// Убрать фильтр, зарегистрированный с помощью модуля

hexo.extend.filter.register('example', require('path/to/filter'));

hexo.extend.filter.unregister('example', require('path/to/filter'));
```

## Список фильтров

Здесь находится список фильтров, используемых в Hexo.

### before_post_render

Выполняется перед началом обработки поста. См. [post rendering](posts.html#Render) для изучения этапов обработки.

Например, перевести название в нижний регистр:

``` js
hexo.extend.filter.register('before_post_render', function(data){
  data.title = data.title.toLowerCase();
  return data;
});
```

### после-пост-рендер

Выполняется после завершения обработки поста. См. [post rendering](posts.html#Обработка) для изучения этапов выполнения.

Например, чтобы заменить `@username` ссылкой на профиль в Twitter:

``` js
hexo.extend.filter.register('after_post_render', function(data){
  data.content = data.content.replace(/@(\d+)/, '<a href="http://twitter.com/$1">#$1</a>');
  return data;
});
```

### перейти_выход

Выполняется перед выходом из Hexo. Срабатывает сразу после выполнения `hexo.exit`.

``` js
hexo.extend.filter.register('before_exit', function(){
  // ...
});
```

### пересгенерировать

Выполнится перед началом генерации.

``` js
hexo.extend.filter.register('before_generate', function(){
  // ...
});
```

### после генерации

Выполнится после окончания генерации.

``` js
hexo.extend.filter.register('after_generate', function(){
  // ...
});
```

### template_locals

Позволяет изменять [локальные переменные](../docs/variables.html) в шаблонах.

Например, чтобы добавить переменную текущего времени в шаблон:

``` js
hexo.extend.filter.register('template_locals', function(locals){
  locals.now = Date.now();
  return locals;
});
```

### _после инициализации

Выполнится после начала инициализации Hexo - запустится только после того, как полностью отработает команда `hexo.init`.

``` js
hexo.extend.filter.register('after_init', function(){
  // ...
});
```

### новый пост_путь

Выполняется при создании поста для определения пути постоянной ссылки.

``` js
hexo.extend.filter.register('new_post_path', function(data, replace){
  // ...
});
```

### Постоянная ссылка

Используется при создании поста для определения пути постоянной ссылки.

``` js
hexo.extend.filter.register('post_permalink', function(data){
  // ...
});
```

### после рендеринга

Выполнится после завершения обработки. См. [рендеринг](rendering.html#after_render_Filters) для подробностей.

### очистить

Выполняется после того, как создаваемые файлы и кэш удаляются с помощью команды `hexo clean`.

``` js
hexo.extend.filter.register('after_clean', function(){
  // удаляем некоторые другие временные файлы
});
```

### server_middleware

Добавляет промежуточные задачи для сервера. `app` является экземпляром [Connect][].

Например, чтобы добавить `X-Powered-By: Hexo` в заголовке ответа:

``` js
hexo.extend.filter.register('server_middleware', function(app){
  app.use(function(req, res, next){
    res.setHeader('X-Powered-By', 'Hexo');
    next();
  });
});
```

[Connect]: https://github.com/senchalabs/connect
