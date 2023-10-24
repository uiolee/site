---
title: GitHub Pages
---

In this tutorial, we use [Travis CI](https://travis-ci.com/) to deploy Github Pages. It is free for open source repository, meaning your repository's `master` branch has to be public. Please skip to the [Private repository](#Private-repository) section if you prefer to keep the repo private, or prefer not to upload your source folder to GitHub.

1. Crie um repositório chamado <b>*username*.github.io</b>, onde o nome de usuário é seu nome de usuário no GitHub. Se você já enviou para outro repositório, renomeie o repositório em vez disso.
2. Push the files of your Hexo folder to the repository. O branch padrão é geralmente o **principal**, o repositório mais antigo pode usar o branch **master**.
  - Para enviar `principal` branch para o GitHub:

    ```
    $ git push -u origem principal
    ```
  - A pasta `pública/` não é (e não deve ser) enviada por padrão, certifique-se do `. itignore` arquivo contém a linha `pública/` A estrutura da pasta deve ser aproximadamente similar a [este repositório](https://github.com/hexojs/hexo-starter).

3. Verifique qual versão do Node.js você está usando na sua máquina local com o nó `--version`. Anote a versão principal (por exemplo, `v16.y.z`)
4. Na configuração do seu repositório do GitHub, navegue para **Configurações** > **Pages** > **Source**. Mude o código fonte para **GitHub Actions** e salve.
5. Criar `.github/workflows/páginas. ml` em seu repositório com o seguinte conteúdo (substituição de `16` para a versão principal do nó. s que você notou na etapa anterior):

```yml .github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
      - main  # default branch

jobs:
  build:
    runs-on: ubuntu-latest
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
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public
  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

6. Uma vez que o deploy terminar, verifique a página da Web no nome **.github.io.

Nota - se você especificar um nome de domínio personalizado com `CNAME`, você precisa adicionar o arquivo `CNAME` à pasta `fonte/`. [Mais informações](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Página do projeto

Se você prefere ter uma página do projeto no GitHub:

1. Navegue até seu repositório no GitHub. Vá para aba **Configurações**. Altere o nome **do repositório** para que o seu blog esteja disponível em <b>username.github. o/*repositório*</b>,  **repositório** pode ser qualquer nome, como o *blog* ou *hexo*.
2. Edit your **_config.yml**, change the `root:` value to the `/<repository>/` (must starts and ends with a slash, without the brackets).
3. On the Travis page, go to your repo's setting. Under **Environment Variables**, put **GH_TOKEN** as name and paste the token onto value. Mude o código fonte para **GitHub Actions** e salve.
4. Enviar e fazer push no branch padrão.
4. Uma vez que o deploy terminar, verifique a página da Web no nome *username*.github.io/*repository*.

## Implementação de um comando

A seguinte instrução é adaptada da página [implantação de um comando](/docs/one-command-deployment).

1. Instale o [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git).
2. Add the following configurations to **_config.yml**, (remove existing lines if any)

  ``` yml
  deploy:
    type: git
    repo: https://github.com/<username>/<project>
    # example, https://github.com/hexojs/hexojs.github.io
    branch: gh-pages
  ```

3. Run `hexo clean && hexo deploy`.
4. Verifique a página da Web no nome *nome de usuário*.github.io.

## Links úteis

- [GitHub Pages](https://docs.github.com/en/pages)
- [Publicação com um fluxo de trabalho personalizado do GitHub Actions](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)
- [ações/deploy-github-pages-site](https://github.com/marketplace/actions/deploy-github-pages-site)
