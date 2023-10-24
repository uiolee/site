---
title: Миграция
---

## RSS-лента

Прежде нужно установить плагин `hexo-migrator-rss`.

``` bash
$ npm установить hexo-migrator-rss --save
```

После установки плагина запустите следующую команду для миграции всех постов в RSS. `source` может быть путём к файлу или URL ссылкой.

``` bash
$ шестнадцать rss <source>
```

## Чекилль

Переместите все файлы из папки Jekyll `_posts` в папку `source/_posts`.

Измените переменную `new_post_name` в `_config.yml`:

``` yaml
new_post_name: :year :month-:day-:title.md
```

## Осьминог

Переместите все файлы из папки Octopress `source/_posts` в папку `source/_posts`.

Измените переменную `new_post_name` в `_config.yml`:

``` yaml
new_post_name: :year :month-:day-:title.md
```

## WordPress

Сначала установите плагин `hexo-migrator-wordpress`.

``` bash
$ npm установить hexo-migrator-wordpress --save
```

Экспортируйте WordPress сайт, зайдя в “Инструменты” → “Экспорт” → “Wordpress” в панели WordPress (см. страницу [поддержки WordPress](https://wordpress.com/ru/support/export/) для более подробной информации.

Выполнить:

``` bash
$ hexo мигрировать wordpress <source>
```

Где `source` — это путь или URL файла экспортированного из WordPress.

## Joomla

Во-первых, нужно установить плагин `hexo-migrator-joomla`.

```bash
$ npm установить hexo-migrator-joomla --save
```

Экспортируйте статьи Joomla с помощью компонента [J2XML](http://extensions.joomla.org/extensions/migration-a-conversion/data-import-a-export/12816?qh=YToxOntpOjA7czo1OiJqMnhtbCI7fQ%3D%3D)

Выполнить:

```bash
$ hexo migrate joomla <source>
```

Где `source` — это путь или URL файла экспортированного из Joomla.
