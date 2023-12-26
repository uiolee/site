---
title: 将 Hexo 部署到 GitLab Pages
---

1. 如果你更希望你的站点部署在 `<你的 GitLab 用户名>.gitlab.io` 的子目录中，你的 repository 需要直接命名为子目录的名字，这样你的站点可以通过 `https://<你的 GitLab 用户名>.gitlab.io/<repository 的名字>` 访问。 你需要检查你的 Hexo 配置文件，将 `url` 的值修改为 `https://<你的 GitLab 用户名>.gitlab.io/<repository 的名字>`、将 `root` 的值修改为 `/<repository 的名字>/`
2. 通过 **设置启用共享运行器** > **CI/CD** > **运行器** > **启用此项目共享运行器**
3. 将你的 Hexo 站点文件夹推送到 repository 中。 默认情况下 `public` 目录将不会（并且不应该）被推送到 repository 中，建议你检查 `.gitignore` 文件中是否包含 `public` 一行，如果没有请加上。 文件夹结构应该大致类似于 [这个repo](https://gitlab.com/pages/hexo)
4. 用 `节点 --version` 检查您在本地机器上使用的Node.js版本。 给主要版本注解(例如， `v16.y.z`
5. 将 `.gitlab-ci.yml` 文件添加到您的 repo 的根目录下(与 _config.yml & 软件包并行)。 请使用以下内容(用你在前面的步骤中注意到的 Node.js 主要版本取代 `16`)：

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

6. GitLab CI 应该会自动开始运行，构建成功以后你应该可以在 `https://<你的 GitLab 用户名>.gitlab.io` 查看你的网站。
7. (可选) 如果你需要查看生成的文件，可以在 [job artifact](https://docs.gitlab.com/ee/ci/pipelines/job_artifacts.html) 中找到。

## 项目页面

如果您喜欢在 GitLab上有一个项目页面：

1. 转到 **设置** > **常规** > **高级** > **更改路径** 将值更改为名称，所以网站可在 <b>username.gitlab.io/*repository*</b> 查阅。 It can be any name, like *blog* or *hexo*.
2. Edit **_config.yml**, change the `url:` value to `https://username.gitlab.io/repository`.
3. 提交和推送。

## 参考链接

- [GitLab Pages 相关文档](https://docs.gitlab.com/ee/user/project/pages/index.html)
- [GitLab CI 相关文档](https://docs.gitlab.com/ee/ci/yaml/)
- [在百度上搜索 "Hexo GitLab"](https://www.baidu.com/s?wd=Hexo%20GitLab)
