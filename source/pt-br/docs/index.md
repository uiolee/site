---
title: Documentação
---

Bem-vindo à documentação do Hexo. Se você encontrar algum problema ao usar o Hexo, dê uma olhada no  [guia de solução de problemas](troubleshooting.html), abra uma issue no [GitHub](https://github.com/hexojs/hexo/issues) ou inicie um tópico no [Google Group](https://groups.google.com/group/hexo).

## O que é o Hexo?

O Hexo é uma ferramenta simples, rápida e poderosa para criação blog. Você escreve postagens em [Markdown](http://daringfireball.net/projects/markdown/) (ou outras linguagens) e o Hexo gera arquivos estáticos com um lindo tema em segundos.

## Instalação

Demora apenas alguns minutos para configurar o Hexo. Se você encontrar um problema e não conseguir encontrar a solução aqui, por favor [abra uma issue no GitHub](https://github.com/hexojs/hexo/issues) e vamos tentar resolvê-lo.

{% youtube ARted4RniaU %}

### Requisitos

Instalar o Hexo é bastante fácil. No entanto, você precisa ter algumas outras coisas instaladas primeiro:

- [Node.js](http://nodejs.org/) (Deve ser pelo menos Node.js 10.13 recomenda 12.0 ou superior)
- [Git](http://git-scm.com/)

Se o seu computador já possui estes, parabéns! Basta instalar o Hexo com o npm:

Caso contrário, siga as instruções a seguir para instalar todos os requisitos.

### Instalando o Git

- Windows: Download e instalação do [Git](https://git-scm.com/download/win).
- Mac: Intalação com o [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) ou [installer](http://sourceforge.net/projects/git-osx-installer/).
- Linux (Ubuntu, Debian): `sudo apt-get install git-core`
- Linux (Fedora, Red Hat, CentOS): `sudo yum install git-core`

{% note warn Para usuários Mac %}
Você pode encontrar alguns problemas ao compilar. Instale o Xcode da App Store primeiro. Depois que o Xcode estiver instalado, abra o Xcode e vá para **Preferences -> Download -> Command Line Tools -> Install** para instalar as ferramentas de linhas de comandos.
{% endnote %}

### Instalando o Node.js

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

### Instalando Hexo

Uma vez que todos os requisitos estão instalados, você pode instalar o Hexo com npm:

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
| 7.0+           | 14.0.0                     | último                       |
| 6.2+           | 12.13.0                    | latest                       |
| 6.0+           | 12.13.0                    | 18.5.0                       |
| 5.0+           | 10.13.0                    | 12.0.0                       |
| 4.1 - 4.2      | 8.10                       | 10.0.0                       |
| 4.0            | 8.6                        | 8.10.0                       |
| 3.3 - 3.9      | 6.9                        | 8.0.0                        |
| 3.2 - 3.3      | 0.12                       | desconhecido                 |
| 3.0 - 3.1      | 0.10 ou iojs               | desconhecido                 |
| 0.0.1 - 2.8    | 0.10                       | desconhecido                 |
