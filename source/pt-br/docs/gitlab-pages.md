---
title: Páginas GitLab
---

1. Crie um novo repositório chamado <b>*username*.gitlab.io</b>, onde o nome de usuário é seu nome de usuário no GitLab. Se você já enviou para outro repositório, renomeie o repositório em vez disso.
2. Enable Shared Runners via `Settings -> CI / CD -> Shared Runners`.
3. Faça push dos arquivos da sua pasta Hexo para o repositório. A pasta `pública/` não é (e não deve ser) enviada por padrão, certifique-se do `. itignore` arquivo contém a linha `pública/` A estrutura da pasta deve ser aproximadamente similar a [este repositório](https://gitlab.com/pages/hexo).
4. Verifique qual versão do Node.js você está usando na sua máquina local com o nó `--version`. Anote a versão principal (por exemplo, `v16.y.z`)
5. Add `.gitlab-ci.yml` file to your repo (alongside _config.yml & package.json) with the following content:

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

6. *nome de usuário*.gitlab.io deve estar ativo e em execução, assim que o GitLab CI terminar o trabalho de implantação
7. (Optional) If you wish to inspect the generated site assets (html, css, js, etc), they can be found in the [job artifact](https://docs.gitlab.com/ee/user/project/pipelines/job_artifacts.html).

## Página do projeto

Se você prefere ter uma página do projeto no GitLab:

1. Go to `Settings -> General -> Advanced -> Change path`. Change the value to a name, so the website is available at <b>username.gitlab.io/*name*</b>. Pode ser qualquer nome, como o *blog* ou *hexo*.
2. Edit **_config.yml**, change the `root:` value from `""` to `"name"`.
3. Commit e push.

## Links úteis

- [Páginas GitLab](https://docs.gitlab.com/ee/user/project/pages/)
- [GitLab CI Docs](https://docs.gitlab.com/ee/ci/yaml/)
