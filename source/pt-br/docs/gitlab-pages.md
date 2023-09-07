---
title: Páginas GitLab
---

1. Crie um novo repositório chamado <b>*username*.gitlab.io</b>, onde o nome de usuário é seu nome de usuário no GitLab. Se você já enviou para outro repositório, renomeie o repositório em vez disso.
2. Habilitar Runners Compartilhados via **Settings** > **CI/CD** > **Runners** > **Habilitar runners compartilhados para este projeto**.
3. Faça push dos arquivos da sua pasta Hexo para o repositório. A pasta `pública/` não é (e não deve ser) enviada por padrão, certifique-se do `. itignore` arquivo contém a linha `pública/` A estrutura da pasta deve ser aproximadamente similar a [este repositório](https://gitlab.com/pages/hexo).
4. Verifique qual versão do Node.js você está usando na sua máquina local com o nó `--version`. Anote a versão principal (por exemplo, `v16.y.z`)
5. Adicionar o arquivo `.gitlab-ci.yml` à pasta raiz do seu repositório (junto com o pacote _config.yml & . son) com o seguinte conteúdo (substituindo `16` pela versão principal do Node.js que você notou na etapa anterior):

``` yml
imagem: node:16-alpine
cache:
  paths:
    - node_modules/

before_script:
  - npm install hexo-cli -g
  - npm install

pages:
  script:
    - npm run build
  artefatos:
    paths:
      - public
  rules:
    - if: $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH
```

6. *nome de usuário*.gitlab.io deve estar ativo e em execução, assim que o GitLab CI terminar o trabalho de implantação
7. (Opcional) Se você deseja inspecionar os assets do site gerados (html, css, js, etc), eles podem ser encontrados no artefato [job](https://docs.gitlab.com/ee/ci/pipelines/job_artifacts.html).

## Página do projeto

Se você prefere ter uma página do projeto no GitLab:

1. Vá para **Configurações** > **General** > **Avançado** > **Mudar o caminho**. Altere o valor para um nome, então o site está disponível em <b>username.gitlab.io/*repository*</b>. Pode ser qualquer nome, como o *blog* ou *hexo*.
2. Editar **_config.yml**, alterar o valor da `url:` para `https://username.gitlab.io/repository`.
3. Commit e push.

## Links úteis

- [Páginas GitLab](https://docs.gitlab.com/ee/user/project/pages/)
- [GitLab CI Docs](https://docs.gitlab.com/ee/ci/yaml/)
