---
title: GitHub Pages
---

In this tutorial, we use [GitHub Actions](https://docs.github.com/en/actions) to deploy GitHub Pages. 它在公共和私人仓库中工作。 如果您不愿意上传源文件夹到 GitHub ，请跳至 [单命令部署](#One-command-deployment) 部分。

1. Create a repo named <b>*username*.github.io</b>, where username is your username on GitHub. 如果你已经上传到其他仓库，请重命名仓库.
2. 将您的 Hexo 文件夹的文件推送到仓库的默认分支。 默认分支通常是 **主**，旧版本库可能使用 **主** 分支。
  - 将 `主` 分支推送到 GitHub：

    ```
    $git 推送-u 来源
    ```
  - `公开/` 文件夹不(而且不应该)默认上载，请确认 `。 简体` 文件包含 `public/` 行。 文件夹结构应该大致类似于 [这个repo](https://github.com/hexojs/hexo-starter), 没有 `.gitmodules` 文件。

3. 用 `节点 --version` 检查您在本地机器上使用的Node.js版本。 给主要版本注解(例如， `v16.y.z`
4. 创建 `.github/workflows/页面。 ml` 在您的仓库中包含以下内容(替换为主版本节点的 `16` s 你在前一步骤中注意到：

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

5. 部署完成后，生成的页面可以在您的资源库的 `gh-pages` 分支中找到。
6. In your GitHub repo's setting, navigate to **Settings** > **Pages** > **Source**. 将分支更改为 `gh-pages` 并保存。
7. Check the webpage at *username*.github.io.

注意：如果您指定了一个带有 `CNAME`的自定义域名。 您需要将 `CNAME` 文件添加到 `源/` 文件夹。 [更多信息](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

## 项目页面

如果您喜欢在 GitHub 上有一个项目页面：

1. 在 GitHub 上导航到你的仓库. 转到 **设置** 标签页。 更改 **仓库名称** ，所以你的博客可以在 <b>username.github上使用。 o/*仓库*</b>、  **仓库** 可以是任何名称，例如 *博客* 或 *hexo*
2. 编辑您的 **_config.yml**, 更改 `网址:` 值为 <b>https://*username*.github.io/*repository*</b>
3. 提交并推送到默认分支。
4. 部署完成后，生成的页面可以在您的资源库的 `gh-pages` 分支中找到。
6. In your GitHub repo's setting, navigate to **Settings** > **Pages** > **Source**. 将分支更改为 `gh-pages` 并保存。
7. 请在 *用户名为*.github.io/*资源库* 中查看网页。

## 一次指挥部署

以下指令是从 [单命令部署](/docs/one-command-deployment) 页面修改的。

1. 安装 [十六进制部署器](https://github.com/hexojs/hexo-deployer-git)
2. 将以下配置添加到 **_config.yml**(如果有的话，请删除现有的行)。

  ``` yml
  deploy:
    type: git
    repo: https://github.com/<username>/<project>
    # example, https://github.com/hexojs/hexojs.github.io
    branch: gh-pages
  ```

3. Run `hexo clean && hexo deploy`.
4. Check the webpage at *username*.github.io.

## 有用的链接

- [GitHub Pages](https://docs.github.com/en/pages)
- [Peaceiris/actions-gh-pages](https://github.com/marketplace/actions/github-pages-action)
