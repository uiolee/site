---
title: GitLab 页面
---

1. 创建一个新的仓库，名称为 <b>*username*.gitlab.io</b>，在该仓库中，用户名是您在 GitLab中的用户名。 如果你已经上传到其他仓库，请重命名仓库.
2. 通过 **设置启用共享运行器** > **CI/CD** > **运行器** > **启用此项目共享运行器**
3. 将你的 Hexo 文件夹的文件推送到资源库。 `公开/` 文件夹不(而且不应该)默认上载，请确认 `。 简体` 文件包含 `public/` 行。 文件夹结构应该大致类似于 [这个repo](https://gitlab.com/pages/hexo)
4. 用 `节点 --version` 检查您在本地机器上使用的Node.js版本。 给主要版本注解(例如， `v16.y.z`
5. 将 `.gitlab-ci.yml` 文件添加到您的 repo 的根目录下(与 _config.yml & 软件包并行)。 请使用以下内容(用你在前面的步骤中注意到的 Node.js 主要版本取代 `16`)：

``` yml
image: node:16-alpine
cache:
  paths:
    - node_modules/

before_script:
  - npm install hexo-cli -g
  - npm install

pages:
  script:
    - npm run build
  artifacts:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

6. *username*.gitlab.io should be up and running, once GitLab CI finishes the deployment job,
7. (Optional) If you wish to inspect the generated site assets (html, css, js, etc), they can be found in the [job artifact](https://docs.gitlab.com/ee/ci/pipelines/job_artifacts.html).

## 项目页面

如果您喜欢在 GitLab上有一个项目页面：

1. 转到 **设置** > **常规** > **高级** > **更改路径** 将值更改为名称，所以网站可在 <b>username.gitlab.io/*repository*</b> 查阅。 It can be any name, like *blog* or *hexo*.
2. Edit **_config.yml**, change the `url:` value to `https://username.gitlab.io/repository`.
3. 提交和推送。

## 有用的链接

- [GitLab 页面](https://docs.gitlab.com/ee/user/project/pages/)
- [GitLab CI Docs](https://docs.gitlab.com/ee/ci/yaml/)
