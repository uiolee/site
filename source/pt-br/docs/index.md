---
title: Documentação
---

Bem-vindo à documentação Hexo. If you encounter any problems when using Hexo, have a look at the  [troubleshooting guide](troubleshooting.html), raise an issue on [GitHub](https://github.com/hexojs/hexo/issues) or start a topic on the [Google Group](https://groups.google.com/group/hexo).

## O que é Hexo?

Hexo é um framework de blog rápido, simples e poderoso. Você escreve posts no [Markdown](http://daringfireball.net/projects/markdown/) (ou outros idiomas de marcação) e no Hexo gera arquivos estáticos com um tema bonito em segundos.

## Instalação

Demora apenas alguns minutos para montar o Hexo. Se você encontrar um problema e não encontrar a solução aqui, por favor [envie um problema do GitHub](https://github.com/hexojs/hexo/issues) e nós ajudaremos.

{% youtube ARted4RniaU %}

### Requisitos

Instalar o Hexo é muito fácil e requer apenas o seguinte antes:

- [Node.js](http://nodejs.org/) (Deve ser pelo menos Node.js 10.13 recomenda 12.0 ou superior)
- [Git](http://git-scm.com/)

Se o seu computador já tem isso, parabéns! You can skip to the [Hexo installation](#Install-Hexo) step.

Se não, siga as seguintes instruções para instalar todos os requisitos.

### Install Git

- Windows: Baixe & instale [git](https://git-scm.com/download/win).
- Mac: Instale-o com [Homebrew](https://brew.sh/), [MacPorts](http://www.macports.org/) ou [Instalador](http://sourceforge.net/projects/git-osx-installer/).
- Linux (Ubuntu, Debian): `sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS): `sudo yum install git-core`

{% note warn For Mac users %}
Você pode encontrar alguns problemas ao compilar. Primeiro instale o Xcode na App Store Depois que o Xcode for instalado, abra o Xcode e vá para **Preferências -> Download -> Ferramentas de linha de comando -> Instale** para instalar as ferramentas de linha de comando.
{% endnote %}

### Instalar Node.js

Node.js fornece [instalador oficial](https://nodejs.org/en/download/) para a maioria das plataformas.

Métodos de instalação alternativos:

- Windows: Instale-o com [nvs](https://github.com/jasongin/nvs/) (recomendado) ou [nvm](https://github.com/nvm-sh/nvm).
- Mac: Instale-o com [Homebrew](https://brew.sh/) ou [MacPorts](http://www.macports.org/).
- Linux (DEB/RPM-based): Instale com [NodeSource](https://github.com/nodesource/distributions).
- Outros: instale-o através do respectivo gerenciador de pacotes. Consulte [o guia](https://nodejs.org/en/download/package-manager/) fornecido pelo Node.js.

nvs também é recomendado para Mac e Linux para evitar possíveis problemas de permissão.

{% note info Windows %}
Se você usar o instalador oficial, certifique-se que **Adicionar ao PATH** está verificado (é marcado por padrão).
{% endnote %}

{% note warn Mac / Linux %}
Se você encontrar o erro de permissão `EACCES` ao tentar instalar o Hexo, por favor, siga [a solução alternativa](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) fornecida pelo npmjs; Sobrescrever com root/sudo é altamente desencorajado.
{% endnote %}

{% note info Linux %}
If you installed Node.js using Snap, you may need to manually run `npm install` in the target folder when [initializing](/docs/commands#init) a blog.
{% endnote %}

### Instalar Hexo

Assim que todos os requisitos estiverem instalados, você pode instalar o Hexo com npm:

``` bash
$ npm install -g hexo-cli
```

### Instalação avançada e uso

Usuários avançados podem preferir instalar e usar o pacote `hexo`.

``` bash
$ npm install hexo
```

Uma vez instalado, você pode executar o Hexo de duas maneiras:

1. `npx hexo <command>`
2. Usuários de Linux podem definir o caminho relativo da pasta `node_modules/`:

  ``` bash
  echo 'PATH="$PATH:./node_modules/.bin"' >> ~/.profile
  ```

  então execute o Hexo usando `hexo <command>`

### Versão necessária do Node.js

Se você estiver preso com o Node.js mais antigo, você pode considerar instalar uma versão anterior do Hexo.

Por favor, note que não fornecemos correções de bugs para versões anteriores do Hexo.

Recomendamos sempre instalar a versão [mais recente](https://www.npmjs.com/package/hexo?activeTab=versions) do Hexo e a versão [recomendada](#Requirements) do Node.js, sempre que possível.

| Versão do Hexo | Mínimo (versão do Node.js) | Menos de (versão do Node.js) |
| -------------- | -------------------------- | ---------------------------- |
| 6.2+           | 12.13.0                    | último                       |
| 6.0+           | 12.13.0                    | 18.5.0                       |
| 5.0+           | 10.13.0                    | 12.0.0                       |
| 4.1 - 4.2      | 8.10                       | 10.0.0                       |
| 4.0            | 8.6                        | 8.10.0                       |
| 3.3 - 3.9      | 6.9                        | 8.0.0                        |
| 3.2 - 3.3      | 0.12                       | desconhecido                 |
| 3.0 - 3.1      | 0.10 ou iojs               | desconhecido                 |
| 0.0.1 - 2.8    | 0.10                       | desconhecido                 |
