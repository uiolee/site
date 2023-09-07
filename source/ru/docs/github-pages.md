---
title: GitHub Pages
---

В этом туториале мы используем [Travis CI](https://travis-ci.com/) для деплоя в Github Pages. [Travis CI](https://travis-ci.com/) бесплатен для репозиториев с открытым исходным кодом, то есть ветка `master` вашего репозитория должна быть публичной. Пожалуйста, перейдите в описание [приватного репозитория](#Private-repository), если вы предпочитаете не открывать свой исходный код, либо откажитесь от загрузки своих файлов на GitHub.

1. Создайте репозиторий с названием <b>*username*.github.io</b>, где `username` — ваше имя пользователя GitHub. Если вы уже загрузили файлы в репозиторий с другим названием, просто переименуйте его.
2. Загрузите `push` файлы вашей папки Hexo в этот репозиторий. Ветка по умолчанию, как правило, **основная**, старый репозиторий может использовать ветку **master**.
  - To push `main` branch to GitHub:

    ```
    $ git push -u основной
    ```
  - Папка `public/` не должна загружаться по умолчанию, проверьте, что файл `.gitignore` содержит строку `public/`. Структура папки должна быть такой же, как в [этом репозитории](https://github.com/hexojs/hexo-starter), без файла `.gitmodules`.

3. Проверьте, какая версия Node.js используется на локальной машине с `узлом --version`. Запомните основную версию (например, `v16.y.z`)
4. Создать `.github/workflows/pages. ml` в вашем репозитории со следующим содержанием (замена `16` основной версии узла. , что вы отметили в предыдущем шаге):

```yml .github/workflows/pages.yml
имя: Страницы

на:
  push:
    ветвей:
      - основная # ветка по умолчанию

задания:
  страницы:
    запуска-on: ubuntu-latest
    разрешения:
      содержимое: написать
    шагов:
      - использование: actions/checkout@v3
        с помощью:
          токен: ${{ secrets.GITHUB_TOKEN }}
          # Если ваше хранилище зависит от субмодуля, пожалуйста, см. https://github. om/actions/checkout
          submodules: recursive
      - name: Use Node. s 16.
        использований: actions/setup-node@v2
        с:
          node-version: '16'
      - Название: кэширование зависимостей NPM
        использование: actions/cache@v2
        с:
          пути: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - Название: Установить зависимости
        выполнен: npm install
      - Название: сборка
        Выполнить: npm запустить сборку
      - название: Deploy
        использования: peaceiris/actions-gh-pages@v3
        с:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir публичный
```

5. В настройках своего репозитория GitHub перейдите в раздел "GitHub Pages" и измените `Source` на **ветку gh-pages**.
6. В настройках вашего репозитория перейдите к **Настройкам** > **страницам** > **Источник**. Изменить ветку на `г страницы` и сохранить.
7. Проверьте веб-страницу по адресу *username*.github.io.

Note - if you specify a custom domain name with a `CNAME`, you need to add the `CNAME` file to the `source/` folder. [More info](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Страница проекта

Если вы препочитаете страницу проекта на GitHub:

1. Перейдите на страницу своего репо на GitHub. Откройте таб **Settings**. Измените **Repository name**, чтобы ваш блог был доступен на <b>username.github.io/*repository*</b>, **repository** может быть любым словом, как *blog* или *hexo*.
2. Редактируйте файл **_config.yml**, изменив значение `root:` на `/<repository>/` (должно начинаться и заканчиваться косой чертой).
3. Зафиксировать и нажать на ветку по умолчанию.
4. Как только Travis CI завершит деплой, сгенерированные страницы появятся в ветке `gh-pages` вашего репо.
6. В новой вкладке сгенерируйте [новый токен](https://github.com/settings/tokens) с областью видимости **repo**. Изменить ветку на `г страницы` и сохранить.
7. Добавьте файл `.travis.yml` в свой репозиторий (рядом с _config.yml & package.json) со следующим контентом:

## Развертывание в одну команду

Следующая инструкция адаптирована со страницы [развёртывание одной командой](/docs/one-command-deployment) page.

1. Установите [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git).
2. Добавьте следующую конфигурацию в **_config.yml**, (удалите существующие строки, если таковые имеются)

  ``` yml
  deploy:
    type: git
    repo: https://github.com/<username>/<project>
    # example, https://github.com/hexojs/hexojs.github.io
    branch: gh-pages
  ```

3. Запустите `hexo clean && hexo deploy`.
4. Проверьте страницу на *username*.github.io.

## Полезные ссылки

- [GitHub Pages](https://docs.github.com/en/pages)
- [peaceiris/actions-gh-pages](https://github.com/marketplace/actions/github-pages-action)
