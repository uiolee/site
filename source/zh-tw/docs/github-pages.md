---
title: 在 GitHub Pages 上部署 Hexo
---

本文將使用 [GitHub Actions](https://docs.github.com/en/actions) 部屬至 GitHub Pages，此方法適用於公開或私人儲存庫。 It works in both public and private repositories. 若你不希望將整個資料夾推上 GitHub，請參閱 [一鍵部屬](#一鍵部屬)。

1. 建立名為 <b>*username*.github.io</b> 的儲存庫，username 是你在 GitHub 上的使用者名稱，若之前已將 Hexo 上傳至其他儲存庫，將該儲存庫重命名即可。 如果你之前上載了 Hexo 到其他資料庫，那麼只需將該資料庫重新命名為 `<GitLab 用戶名>.gitlab.io` 。
2. Push the files of your Hexo folder to the default branch of your repository. 在儲存庫中前往 **Settings** > **Pages** > **Source**，並將 branch 改為 `gh-pages`。
  - 將 `main` 分支 push 到 GitHub：

    ```
    $ git push -u origin main
    ```
  - 預設情況下 `public/` 不會被上傳(也不該被上傳)，確認 `.gitignore` 檔案中包含一行 `public/`。 整體資料夾結構應會與[範例儲存庫](https://github.com/hexojs/hexo-starter)極為相似。

3. 使用 `node --version` 指令檢查你電腦上的 Node.js 版本，並記下該版本 (例如：`v16.y.z`) Make a note of the major version (e.g., `v16.y.z`)
4. 開啟你在 GitHub 的儲存庫，並前往 **Settings** 頁面。 Change the source to **GitHub Actions** and save.
5. 在儲存庫中建立 `.github/workflows/pages.yml`，並填入以下內容 (將 `16` 替換為上個步驟中記下的版本)：

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

6. Once the deployment is finished, check the webpage at *username*.github.io.

若你使用 `CNAME` 自訂域名，你需要在 `source/` 資料夾中新增 `CNAME` 檔案。 [更多資訊](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

## Project page

如果你希望網站部署在 `<你的 GitHub 用戶名>.github.io` 的子目錄中：

1. Navigate to your repo on GitHub. Go to the **Settings** tab. Change the **Repository name** so your blog is available at <b>username.github.io/*repository*</b>,  **repository** can be any name, like *blog* or *hexo*.
2. 編輯你的 **_config.yml**，將 `url:` 更改為 <b>https://*username*.github.io/*repository*</b>。
3. 在 GitHub 儲存庫中，前往 **Settings** > **Pages** > **Source**，並將 branch 改為 `gh-pages` 後儲存。 Change the source to **GitHub Actions** and save.
4. Commit and push to the default branch.
4. Once the deployment is finished, check the webpage at *username*.github.io/*repository*.

## One-command deployment

以下教學改編自 [一鍵部署](/docs/one-command-deployment) .

1. 安裝 [hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git).
2. Add the following configurations to **_config.yml**, (remove existing lines if any).

  ``` yml
  deploy:
    type: git
    repo: https://github.com/<username>/<project>
    # example, https://github.com/hexojs/hexojs.github.io
    branch: gh-pages
  ```

3. 執行 `hexo clean && hexo deploy` 。
4. 前往 *username*.github.io 查看網站。

## Useful links

- [GitHub Pages 使用文檔](https://docs.github.com/en/pages)
- [Publishing with a custom GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow)
- [actions/deploy-github-pages-site](https://github.com/marketplace/actions/deploy-github-pages-site)
