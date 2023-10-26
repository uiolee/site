---
title: Implantação de um Comando
---

O Hexo fornece uma estratégia de implantação (deployment) rápida e fácil. Você só precisa de um único comando para implantar seu site no servidor.

```bash
Campo hexo de $
```

Instale os plugins necessários que são compatíveis com o método de implantação fornecido pelo seu servidor/repositório.

Antes da sua primeira implantação, você terá que modificar algumas configurações em `_config.yml`. Uma configuração de implantação válida deve ter um campo `type`. Por exemplo:

```yaml
implantação:
  tipo: git
```

Você pode implantar o site em mais de um servidor. O Hexo executará cada implantação na ordem da declaração.

```yaml
deploy:
- tipo: git
  repo:
- tipo: heroku
:
```

Consulte a lista [Plugins](https://hexo.io/plugins/) para mais plugins de implantação.

## Git

1. Instale o [hexo-deployer-git][].

```bash
$ npm install hexo-deployer-git --save
```

2. Editar **\_config.yml** (com exemplos de valores mostrados abaixo como comentários):

```yaml
deploy:
  type: git
  repo: <repository url> #https://bitbucket.org/JohnSmith/johnsmith.bitbucket.io
  branch: [branch]
  message: [message]
```

| Opção         | Descrição                                                                                                           | Padrão                                                                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `repositório` | URL do repositório de destino                                                                                       |                                                                                     |
| `branch`      | Nome da filial.                                                                                                     | `gh-pages` (GitHub)<br>`coding-pages` (Coding.net)<br>`master` (outros) |
| `Mensagem`    | Personalizar mensagem de commit.                                                                                    | `Site atualizado: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`            |
| `token`       | Valor do token opcional para autenticação com o repositório. Prefixo com `$` para ler token da variável de ambiente |                                                                                     |

3. Implante seu site `hexo limpe && hexo deploy`.

  - Você será solicitado com o nome de usuário e senha do repositório de destino, a menos que você autentique com um token ou chave ssh.
  - hexo-deployer-git não armazena seu nome de usuário e senha. Use [git-credential-cache](https://git-scm.com/docs/git-credential-cache) para armazená-los temporariamente.

4. Navegue até as configurações do repositório e altere o ramo "Páginas" para `gh-pages` (ou o ramo especificado na sua configuração). O site implantado deve estar ao vivo na configuração de "Páginas".

## Heroku

Instale o pacote [hexo-deployer-heroku][].

```bash
$ npm install hexo-deployer-heroku --save
```

Editando as configurações.

```yaml
deploy:
  tipo: heroku
  repo: <repository url>
  message: [message]
```

| Opção                 | Descrição                                                                                                         |
| --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `repo`, `repositório` | URL do repositório no Heroku                                                                                      |
| `Mensagem`            | Customiza a mensagem de commit (O padão é: `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`) |

## Netlify

[Netlify](https://www.netlify.com/) fornece deploy contínuo (compilações acionadas pelo Git), um CDN, DNS global inteligente, completo (incluindo domínios personalizados), HTTP automatizado, aceleração de ativos e muito mais. É uma plataforma unificada que automatiza seu código para criar sites de alto desempenho e facilmente sustentável e aplicativos web.

Existem duas maneiras diferentes de implantar seus sites no Netlify. O jeito mais comum é usar a interface da web. Vá para [criar uma nova página do site](https://app.netlify.com/start), selecione seu repositório de projeto no GitHub, GitLab ou Bitbucket, e siga os prompts.

Como alternativa, você pode usar a ferramenta CLI [da Netlify, baseada em CLI](https://www.netlify.com/docs/cli/) para gerenciar e implantar sites no Netlify sem sair do seu terminal.

Você também pode adicionar um [Implantar no Netlify Button](https://www.netlify.com/docs/deploy-button/) no seu README. ile to allow other to create a copy of your repository and be deployed to Netlify via um clique.

## Rsync

Instale o pacote [hexo-deployer-rsync][].

```bash
$ npm install hexo-deployer-rsync --save
```

Editando as configurações.

```yaml
deploy:
  type: rsync
  host: <host>
  user: <user>
  root: <root>
  porta: [port]
  deleta: [trueřfalse]
  verbose: [trueý false]
  ignore_errors: [trueg_false]
```

| Opção           | Descrição                              | Padrão     |
| --------------- | -------------------------------------- | ---------- |
| `hospedeiro`    | Endereço do host remoto                |            |
| `usuário`       | Nome de usuário                        |            |
| `raiz`          | Diretório raiz do host remoto          |            |
| `Porta`         | Porta                                  | 22         |
| `Excluir`       | Exclui arquivos antigos no host remoto | verdadeiro |
| `verbose`       | Exibi mensagens detalhadas             | verdadeiro |
| `ignorar_erros` | Ignora erros                           | Falso      |

## OpenShift

Instale o pacote [hexo-deployer-openshift][].

```bash
$ npm install hexo-deployer-openshift --save
```

Editando as configurações.

```yaml
deploy:
  tipo: openshift
  repo: <repository url>
  message: [message]
```

| Opção         | Descrição                                                                                                         |
| ------------- | ----------------------------------------------------------------------------------------------------------------- |
| `repositório` | URL do repositório no OpenShift                                                                                   |
| `Mensagem`    | Customiza a mensagem de commit (O padrão é `Site updated: {% raw %}{{ now('YYYY-MM-DD HH:mm:ss') }}{% endraw %}`) |

## FTPSync

Instale o pacote [hexo-deployer-ftpsync][].

```bash
$ npm install hexo-deployer-ftpsync --save
```

Editando as configurações.

```yaml
deploy:
  tipo: ftpsync
  host: <host>
  usuário: <user>
  pass: <password>
  remota: [remote]
  porta: [port]
  ignore: [ignore]
  conexões: [connections]
  versículo: [truewilling false]
```

| Alternativa  | Descrição                         | Padrão |
| ------------ | --------------------------------- | ------ |
| `hospedeiro` | Endereço do host remoto           |        |
| `usuário`    | Nome de usuário                   |        |
| `aprovação`  | Senha                             |        |
| `remota`     | Diretório raiz do host remoto     | `/`    |
| `Porta`      | Porta                             | 21     |
| `ignorar`    | Ignora os arquivos no host remoto |        |
| `conexões`   | Número de conexões                | 1      |
| `verbose`    | Exibi mensagens detalhadas        | Falso  |

## SFTP

Instale o pacote [hexo-deployer-sftp][]. Implantação do site via SFTP, permitindo conexões sem senhas usando "ssh-agent".

```bash
$ npm install hexo-deployer-sftp --save
```

Editando as configurações.

```yaml
deploy:
  type: sftp
  host: <host>
  user: <user>
  pass: <password>
  remotePath: [remote path]
  port: [port]
  privateKey: [path/to/privateKey]
  passphrase: [passphrase]
  agent: [path/to/agent/socket]
```

| Alternativa          | Descrição                                                 | Padrão           |
| -------------------- | --------------------------------------------------------- | ---------------- |
| `hospedeiro`         | Endereço do host remoto                                   |                  |
| `Porta`              | Porta                                                     | 22               |
| `usuário`            | Nome de usuário                                           |                  |
| `aprovação`          | Senha                                                     |                  |
| `privateChave`       | Caminho para uma chave ssh privada                        |                  |
| `frase-chave`        | Frase secreta opcional para a chave privada               |                  |
| `agente`             | Caminho para o socket do agente ssh                       | `$SSH_AUTH_SOCK` |
| `caminhoRemoto`      | Diretório raiz do host remoto                             | `/`              |
| `forçCarregarUpload` | Sobrescrever arquivos existentes                          | Falso            |
| `concorrência`       | Número máximo de tarefas SFTP processadas simultaneamente | 100              |

## Transportadora

[Vercel](https://vercel.com) é uma plataforma em nuvem que permite aos desenvolvedores hospedar sites e serviços web Jamstack que são lançados instantaneamente, escala automática e não requer nenhuma supervisão, tudo com configuração zero. Eles fornecem uma rede de arestas global, criptografia SSL, compressão de ativos, invalidez de cache e muito mais.

Passo 1: Adicione um script de compilação ao seu arquivo `package.json`:

```json
{
  "scripts": {
    "build": "hexo gerate"
  }
}
```

Passo 2: Implantar seu site Hexo para Vercel

Para fazer deploy do seu aplicativo Hexo com um [Vercel para Integração Git](https://vercel.com/docs/git-integrations), certifique-se de que ele tenha sido enviado para um repositório Git.

Importe o projeto para Vercel utilizando o [Importar Flow](https://vercel.com/import/git). Durante a importação, você encontrará todas as opções relevantes pré-configuradas para você; no entanto, você pode optar por alterar qualquer uma destas opções, uma lista das quais pode ser encontrada [aqui](https://vercel.com/docs/build-step#build-&-development-settings).

Depois que o seu projeto for importado, todos os pushes subsequentes em branches gerarão [Pré-visualizar Deployments](https://vercel.com/docs/platform/deployments#preview), , e todas as alterações feitas no ramo de produção [](https://vercel.com/docs/git-integrations#production-branch) (comumente "principal") resultarão em [Implantação de Produção](https://vercel.com/docs/platform/deployments#production).

Como alternativa, você pode clicar no botão de implantação abaixo para criar um novo projeto:

[![Implantar Vercel](https://vercel.com/button)](https://vercel.com/new/hexo)

## Bênção

[Bip](https://bip.sh) é um serviço de hospedagem comercial que fornece implantação de zero downtime, uma CDN, SSL, largura de banda ilimitada e muito mais para sites estáticos. Planos estão disponíveis para pagamento conforme você está, por domínio.

Começar é rápido e fácil, já que Bip fornece o suporte absoluto para o Hexo. Este guia assume que você já tem [domínio de Bip e Bip CLI instalado](https://bip.sh/getstarted).

1: Inicialize o diretório do seu projeto

```bash
$ bip init
```

Siga as instruções para onde você será solicitado a qual domínio você gostaria de implantar. A Bíblia detectará que você está usando o Hexo, e definirá automaticamente as configurações do projeto, como o diretório do arquivo de origem.

2: Implante seu site

```bash
$ hexo gera — implantar && implantação de bip
```

Depois de alguns momentos, seu site será publicado.

## RSS3

\[RSS3\] (https://rss3.io) é um protocolo aberto projetado para conteúdo e redes sociais na era da Web 3.0.

1. Instale [hexo-deployer-rss3][]

2. Modifique a configuração.

  ``` yaml
  deploy:
  - type: rss3
    endpoint: https://hub.rss3.io
    privateKey: 47e18d6c386898b424025cd9db446f779ef24ad33a26c499c87bb3d9372540ba
    ipfs:
      deploy: true
      gateway: pinata
      api:
        key: d693df715d3631e489d6
        secret: ee8b74626f12b61c1a4bde3b8c331ad390567c86ba779c9b18561ee92c1cbff0
  ```

| Parâmetros        | Descrição                                           |
| ----------------- | --------------------------------------------------- |
| `endpoint`        | Um link para o hub RSS3                             |
| `privateChave`    | Sua chave privada, 64 bytes                         |
| `ipfs/deploy`     | Se deve implantar no IPFS                           |
| `ipfs/gateway`    | Gateway de API IPFS                                 |
| `ipfs/api/key`    | Conteúdo de verificação relacionado ao gateway IPFS |
| `ipfs/api/secret` | Conteúdo de verificação relacionado ao gateway IPFS |

3. Gere arquivos estáticos

4. implantar

Para precauções relacionadas à implantação específica, você pode consultar \[nossa documentação\] (https://github.com/NaturalSelectionLabs/hexo-deployer-rss3/tree/develop/docs/zh_CN/start.md).

## Edgio (antiga camada)

[Edgio (anteriormente Layer0)](https://docs.edg.io) é uma plataforma de escala da Internet que torna fácil a construção de equipes, libere, proteja e acelere seus aplicativos da web e APIs.

1. No diretório do seu projeto hexo, instale o Edgio CLI:

```bash
npm i -g @edgio/cli
```

2. Instalar o conector Hexo por Edgio:

```bash
edit --connector=@edgio/hexo
```

3. Implantar

```bash
edgio de deploy
```

Como alternativa, você pode clicar no botão de implantação abaixo para criar um novo projeto:

[![Implementar para Edgio](https://docs.edg.io/button.svg)](https://app.layer0.co/deploy?repo=https%3A%2F%2Fgithub.com%2Fedgio-docs%2Fedgio-hexo-example)

## Outros Métodos

Todos os arquivos gerados são salvos no diretório `public`. Você pode copiá-los para onde quiser.

[hexo-deployer-git]: https://github.com/hexojs/hexo-deployer-git
[hexo-deployer-heroku]: https://github.com/hexojs/hexo-deployer-heroku
[hexo-deployer-rsync]: https://github.com/hexojs/hexo-deployer-rsync
[hexo-deployer-openshift]: https://github.com/hexojs/hexo-deployer-openshift
[hexo-deployer-ftpsync]: https://github.com/hexojs/hexo-deployer-ftpsync
[hexo-deployer-sftp]: https://github.com/lucascaro/hexo-deployer-sftp
[hexo-deployer-rss3]: https://github.com/NaturalSelectionLabs/hexo-deployer-rss3
