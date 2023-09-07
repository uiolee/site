---
title: GitHub Pages
---

Neste tutorial, usamos [GitHub Actions](https://docs.github.com/en/actions) para o deploy de Páginas do GitHub. Funciona tanto em repositório público quanto privado. Pule para a seção [Um comando de deploy](#One-command-deployment) se você preferir não enviar sua pasta de origem para o GitHub.

1. Crie um repositório chamado <b>*username*.github.io</b>, onde o nome de usuário é seu nome de usuário no GitHub. Se você já enviou para outro repositório, renomeie o repositório em vez disso.
2. Faça push dos arquivos da sua pasta Hexo para o branch padrão do seu repositório. O branch padrão é geralmente o **principal**, o repositório mais antigo pode usar o branch **master**.
  - Para enviar `principal` branch para o GitHub:

    ```
    $ git push -u origem principal
    ```
  - A pasta `pública/` não é (e não deve ser) enviada por padrão, certifique-se do `. itignore` arquivo contém a linha `pública/` A estrutura da pasta deve ser aproximadamente similar a [este repositório](https://github.com/hexojs/hexo-starter), sem o arquivo `.gitmodules`.

3. Verifique qual versão do Node.js você está usando na sua máquina local com o nó `--version`. Anote a versão principal (por exemplo, `v16.y.z`)
4. Criar `.github/workflows/páginas. ml` em seu repositório com o seguinte conteúdo (substituição de `16` para a versão principal do nó. s que você notou na etapa anterior):

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

5. Depois que o deploy estiver concluído, as páginas geradas podem ser encontradas na branch `gh-pages` do repositório.
6. Na configuração do seu repositório do GitHub, navegue para **Configurações** > **Pages** > **Source**. Altere o branch para `gh-pages` e salve.
7. Verifique a página da Web no nome *nome de usuário*.github.io.

Nota - se você especificar um nome de domínio personalizado com `CNAME`, você precisa adicionar o arquivo `CNAME` à pasta `fonte/`. [Mais informações](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site).

## Página do projeto

Se você prefere ter uma página do projeto no GitHub:

1. Navegue até seu repositório no GitHub. Vá para aba **Configurações**. Altere o nome **do repositório** para que o seu blog esteja disponível em <b>username.github. o/*repositório*</b>,  **repositório** pode ser qualquer nome, como o *blog* ou *hexo*.
2. Editar o seu **_config.yml**, altere o valor do `url:` para <b>https://*username*.github.io/*repository*</b>.
3. Enviar e fazer push no branch padrão.
4. Depois que o deploy estiver concluído, as páginas geradas podem ser encontradas na branch `gh-pages` do repositório.
6. Na configuração do seu repositório do GitHub, navegue para **Configurações** > **Pages** > **Source**. Altere o branch para `gh-pages` e salve.
7. Verifique a página da Web no nome *username*.github.io/*repositório*.

## Implementação de um comando

A seguinte instrução é adaptada da página [implantação de um comando](/docs/one-command-deployment).

1. Instale o [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git).
2. Adicione as seguintes configurações ao **_config.yml**, (remova as linhas existentes se houver).

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
- [peaceiris/actions-gh-pages](https://github.com/marketplace/actions/github-pages-action)
