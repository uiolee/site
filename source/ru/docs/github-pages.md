---
title: GitHub Pages
---

В этом туториале мы используем [Travis CI](https://travis-ci.com/) для деплоя в Github Pages. [Travis CI](https://travis-ci.com/) бесплатен для репозиториев с открытым исходным кодом, то есть ветка `master` вашего репозитория должна быть публичной. Пожалуйста, перейдите в описание [приватного репозитория](#Private-repository), если вы предпочитаете не открывать свой исходный код, либо откажитесь от загрузки своих файлов на GitHub.

1. Создайте репозиторий с названием <b>*username*.github.io</b>, где `username` — ваше имя пользователя GitHub. Если вы уже загрузили файлы в репозиторий с другим названием, просто переименуйте его.
2. Загрузите `push` файлы вашей папки Hexo в этот репозиторий. The default branch is usually **main**, older repository may use **master** branch.
  - To push `main` branch to GitHub:

    ```
    $ git push -u origin main
    ```
  - Папка `public/` не должна загружаться по умолчанию, проверьте, что файл `.gitignore` содержит строку `public/`. Структура папки должна быть такой же, как в [этом репозитории](https://github.com/hexojs/hexo-starter), без файла `.gitmodules`.

3. Check what version of Node.js you are using on your local machine with `node --version`. Make a note of the major version (e.g., `v16.y.z`)
4. Create `.github/workflows/pages.yml` in your repo with the following contents (substituting `16` to the major version of Node.js that you noted in previous step):

```yml .github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
      - main  # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v3
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          # If your repository depends on submodule, please see: https://github.com/actions/checkout
          submodules: recursive
      - name: Use Node.js 16.x
        uses: actions/setup-node@v2
        with:
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
        run: npm run build
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

5. В настройках своего репозитория GitHub перейдите в раздел "GitHub Pages" и измените `Source` на **ветку gh-pages**.
6. In your GitHub repo's setting, navigate to **Settings** > **Pages** > **Source**. Change the branch to `gh-pages` and save.
7. Проверьте веб-страницу по адресу *username*.github.io.

Note - if you specify a custom domain name with a `CNAME`, you need to add the `CNAME` file to the `source/` folder. [More info](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Страница проекта

Если вы препочитаете страницу проекта на GitHub:

1. Перейдите на страницу своего репо на GitHub. Откройте таб **Settings**. Измените **Repository name**, чтобы ваш блог был доступен на <b>username.github.io/*repository*</b>, **repository** может быть любым словом, как *blog* или *hexo*.
2. Редактируйте файл **_config.yml**, изменив значение `root:` на `/<repository>/` (должно начинаться и заканчиваться косой чертой).
3. Commit and push to the default branch.
4. Как только Travis CI завершит деплой, сгенерированные страницы появятся в ветке `gh-pages` вашего репо.
6. В новой вкладке сгенерируйте [новый токен](https://github.com/settings/tokens) с областью видимости **repo**. Change the branch to `gh-pages` and save.
7. Добавьте файл `.travis.yml` в свой репозиторий (рядом с _config.yml & package.json) со следующим контентом:

## One-command deployment

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
