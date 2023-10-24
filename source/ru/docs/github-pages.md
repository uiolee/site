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
4. В настройках вашего репозитория перейдите к **Настройкам** > **страницам** > **Источник**. Измените источник на **GitHub Actions** и сохраните.
5. Создать `.github/workflows/pages. ml` в вашем репозитории со следующим содержанием (замена `16` основной версии узла. , что вы отметили в предыдущем шаге):

```yml .github/workflows/pages.yml
имя: Страницы

в:
  push:
    ветвей:
      - основная # ветка

по умолчанию:
  создать:
    запуска-на: Ubuntu-latest
    шаги:
      - использование: actions/checkout@v3
        с:
          токен: ${{ secrets.GITHUB_TOKEN }}
          # Если хранилище зависит от подмодуля, пожалуйста, см. https://github. om/actions/checkout
          подмодули: рекурсивный
      - имя: Использовать узел. s 16.
        использований: actions/setup-node@v2
        с:
          node-version: '16'
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v2
        с:
          path: . public
  deployment :
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: ploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

6. Once the deployment is finished, check the webpage at *username*.github.io.

Note - if you specify a custom domain name with a `CNAME`, you need to add the `CNAME` file to the `source/` folder. [More info](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Страница проекта

Если вы препочитаете страницу проекта на GitHub:

1. Перейдите на страницу своего репо на GitHub. Откройте таб **Settings**. Измените **Repository name**, чтобы ваш блог был доступен на <b>username.github.io/*repository*</b>, **repository** может быть любым словом, как *blog* или *hexo*.
2. Редактируйте файл **_config.yml**, изменив значение `root:` на `/<repository>/` (должно начинаться и заканчиваться косой чертой).
3. В новой вкладке сгенерируйте [новый токен](https://github.com/settings/tokens) с областью видимости **repo**. Измените источник на **GitHub Actions** и сохраните.
4. Зафиксировать и нажать на ветку по умолчанию.
4. Once the deployment is finished, check the webpage at *username*.github.io/*repository*.

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
4. Проверьте веб-страницу по адресу *username*.github.io.

## Полезные ссылки

- [GitHub Pages](https://docs.github.com/en/pages)
- [Публикация с пользовательскими действиями GitHub](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)
- [actions/deploy-github-pages-site](https://github.com/marketplace/actions/deploy-github-pages-site)
