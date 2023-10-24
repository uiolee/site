---
title: Страницы GitLab
---

1. Создайте новый репозиторий под названием <b>*username*.gitlab.io</b>, где `username` — ваше имя пользователя GitLab. Если вы уже загрузили файлы в репозиторий с другим названием, просто переименуйте его.
2. Включите возможность Shared Runners через настройки `Settings -> CI / CD -> Shared Runners`.
3. Запушьте файлы вашей папки Hexo в этот репозиторий. Папка `public/` не должна загружаться по умолчанию, проверьте, что файл `.gitignore` содержит строку `public/`. Структура папки должна быть такой же, как в [этом репозитории](https://gitlab.com/pages/hexo).
4. Проверьте, какая версия Node.js используется на локальной машине с `узлом --version`. Запомните основную версию (например, `v16.y.z`)
5. Добавьте файл `.gitlab-ci.yml` в ваш репозиторий (рядом с _config.yml & package.json) со следующий контентом:

``` yml
image: node:10-alpine # use nodejs v10 LTS
cache:
  paths:
    - node_modules/

before_script:
  - npm install hexo-cli -g
  - npm install

pages:
  script:
    - hexo generate
  artifacts:
    paths:
      - public
  only:
    - master
```

6. *username*.gitlab.io должен заработать, как только GitLab CI закончит деплой.
7. (Опционально) Если вы хотите проверить содержимое папок с материалами (html, css, js и т.д.), они могут быть найдены в разделе [job artifact](https://docs.gitlab.com/ee/user/project/pipelines/job_artifacts.html).

## Страница проекта

Если вы препочитаете страницу проекта на GitLab:

1. Перейдите в настройки `Settings -> General -> Advanced -> Change path`. Измените значение на имя так, чтобы сайт был доступен по адресу <b>username.gitlab.io/*name*</b>. Это может быть любое слово, как *blog* или *hexo*.
2. Редактируйте **_config.yml**, изменив значение `root:` с `""` на `"name"`.
3. Закоммитьте и запушьте.

## Полезные ссылки

- [Страницы GitLab](https://docs.gitlab.com/ee/user/project/pages/)
- [Документация GitLab CI](https://docs.gitlab.com/ee/ci/yaml/)
