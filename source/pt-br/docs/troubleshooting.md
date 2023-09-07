---
title: Solução de problemas
---

Caso você esteja enfrentando problemas com o uso do Hexo, veja uma lista de soluções para alguns problemas com frequência. Se esta página não ajudar a resolver seu problema, tente fazer uma pesquisa no [GitHub](https://github.com/hexojs/hexo/issues) ou no nosso [Google Group](https://groups.google.com/group/hexo).

## YAML Parsing Error

``` plain
JS-YAML: um par explícito de mapeamento incompleto; um nó chave é perdido na linha 18, coluna 29:
      last_updated: Última atualização: %s
```

Envolva a linha com aspas se conter dois-pontos.

``` plain
JS-YAML: recuo ruim de uma entrada de mapeamento na linha 18, coluna 31:
      last_updated:"Última atualização: %s"
```

Certifique-se de estar usando guias suaves e adicione um espaço após dois-pontos.

Você pode ver [YAML Spec](http://www.yaml.org/spec/1.2/spec.html) para mais informações.

## Erro de EMFILE

``` plain
Erro: EMFILE, muitos arquivos abertos
```

Embora o Node.js tenha o I/O sem bloqueio, o número máximo de E/S síncrono ainda é limitado pelo sistema. Você pode encontrar um erro EMFILE ao tentar gerar um grande número de arquivos. Você pode tentar executar o seguinte comando para aumentar o número de operações sincronizadas permitidas.

``` bash
$ ulimit -n 10000
```

**Erro: não é possível modificar o limite**

Se você encontrar o seguinte erro:

``` bash
$ ulimit -n 10000
ulimit: arquivos abertos: não é possível modificar o limite: Operação não permitida
```

It means some system-wide configurations are preventing `ulimit` to being increased to a certain limit.

Para substituir o limite:

1. Adicione a seguinte linha a "/etc/security/limits.conf":

  ```
  * - nofile 10000

  # '*' se aplica a todos os usuários e '-' define limites macios e rígidos
  ```

  * A configuração acima pode não se aplicar em alguns casos, garantir que "/etc/pam.d/login" e "/etc/pam.d/lightdm" tenham a seguinte linha. (Ignorar esta etapa se os arquivos não existirem)

  ```
  sessão necessária pam_limits.so
  ```

2. Se você está em uma distribuição [baseada no sistema](https://en.wikipedia.org/wiki/Systemd#Adoption) , o sistema pode substituir "limits.conf". Para definir o limite no sistema, adicione a seguinte linha em "/etc/systemd/system.conf" e "/etc/systemd/user.conf":

  ```
  PadrãoLimitNOFILE=10000
  ```

3. Reboot

## Processo Sem Memória

Quando você encontrar esse erro durante a geração:

```
ERRO FATAL: CALL_AND_RETRY_LAST Alocação falhou - processo sem memória
```

Aumente o tamanho da memória da heap do Node.js alterando a primeira linha de `hexo-cli` (`qual hexo` para procurar o arquivo).

```
#!/usr/bin/env node --max_old_space_size=8192
```

[Sem memória ao gerar um enorme blog · Problema #1735 · hexojs/hexo](https://github.com/hexojs/hexo/issues/1735)

## Problemas de implantação Git

### RPC falhou

``` plain
erro: RPC falhou; result=22, código HTTP = 403

fatal: 'username.github.io' não parece ser um repositório git
```

Certifique-se de que [configurou o git](https://help.github.com/articles/set-up-git) no seu computador corretamente ou tente usar a URL do repositório HTTPS.

### Erro: ENOENT: nenhum arquivo ou diretório desse tipo

Se você receber um erro como `Erro: ENOENT: nenhum arquivo ou diretório` provavelmente é devido a misturar letras maiúsculas e minúsculas nas suas etiquetas, categorias ou nomes de arquivos. O Git não pode fazer o merge dessa alteração automaticamente para que ela quebra o branch automático.

Para corrigir isso, tente

1. Verifique todos os marcadores e categorias e tenha certeza que eles são os mesmos.
1. Comprometa-se
1. Limpar e construir: `./node_modules/.bin/hexo clean && ./node_modules/.bin/hexo generate`
1. Copie manualmente a pasta pública para a área de trabalho
1. Mude de branch do master para o seu ramo de deploy localmente
1. Copie o conteúdo da pasta pública da sua área de trabalho para o branch de implantação
1. Submeter. Você deve ver quaisquer conflitos de mesclagem que você pode resolver manualmente.
1. Volte para o seu branch master e faça deploy normalmente: `./node_modules/.bin/hexo deploy`

## Problemas no servidor

``` plain
Error: listen EADDRINUSE
```

Você pode ter iniciado dois servidores Hexo ao mesmo tempo ou pode haver outro aplicativo usando a mesma porta. Tente modificar a configuração da porta `` ou iniciar o servidor Hexo com a flag `-p`.

``` bash
$ servidor hexo -p 5000
```

## Problemas de instalação de plugin

``` plain
ERRO npm! configurar compilação de node-waf
```

Este erro pode ocorrer ao tentar instalar um plugin escrito em C, C++ ou outros idiomas não-JavaScript. Certifique-se de ter instalado o compilador certo em seu computador.

## Erro com DTrace (Mac OS X)

```plain
{ [Erro: Não foi possível encontrar o módulo './build/Release/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
{ [Erro: Não foi possível encontrar o módulo '. build/default/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
{ [Erro: Não foi possível encontrar o módulo './build/Debug/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
```

A instalação do DTrace pode ter problema, use isto:

```sh
$ npm install hexo --no-optional
```

Veja [#1326](https://github.com/hexojs/hexo/issues/1326#issuecomment-113871796)

## Modelo de Dados Iterados em Jade ou Swig

Hexo usa [Armazém][] para seu modelo de dados. Não é uma matriz, então você pode ter que transformar objetos em iterables.

```
{% for post in site.posts.toArray() %}
{% endfor %}
```

## Dados Não Atualizados

Alguns dados não podem ser atualizados ou os arquivos recém-gerados são idênticos aos da última versão. Limpe o cache e tente novamente.

``` bash
Limpeza de $ hexos
```

## Nenhum comando foi executado

Quando você não puder pegar qualquer comando, exceto `help`, `init` e `versão` para trabalhar e você continua obtendo conteúdo de `hexo help`, pode ser causado por um hexo `ausente` no pacote `. filho`:

```json
{
  "hexo": {
    "version": "3.2.2"
  }
}
```

## Conteúdo de fuga

Hexo usa [Nunjucks][] para renderizar posts ([Swig][] foi usado na versão anterior, que compartilham uma sintaxe similar). Conteúdo encapsulado com `{{ }}` ou `{% %}` será analisado e pode causar problemas. Você pode pular a análise envolvendo-a com o plugin [`raw`](/docs/tag-plugins#Raw) de tag, backtick `` `{{ }}` `` ou backtick triplo. Alternativamente, as tags Nunjucks podem ser desativadas através da opção do renderizador (se suportado), [API](/api/renderer#Disable-Nunjucks-tags) ou [front-matter](/docs/front-matter).

```
{% raw %}
Olá {{ world }}
{% endraw %}
```

````
```
Olá, {{ world }}
```
````

## ENOSPC Error (Linux)

Às vezes, ao executar o comando `$ hexo server` ele retorna um erro:

```
Erro: watch ENOSPC ...
```

Ele pode ser corrigido executando `$ npm dedupe` ou, se isso não ajudar, tente o seguinte no console do Linux:

```
$ echo fs.inotify.max_user_watches=524288 ➲ sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

Isso irá aumentar o limite de arquivos que você pode assistir.

## Erro do EMPERM (Subsistema do Windows para Linux)

Ao executar o servidor `$ hexo` em um ambiente BashOnWindows, ele retorna o seguinte erro:

```
Erro: watch /path/to/hexo/theme/ EMPERM
```

Infelizmente, WSL atualmente não suporta observadores de sistemas de arquivos. Portanto, a funcionalidade de atualização ao vivo do servidor hexo está atualmente indisponível. Você ainda pode executar o servidor a partir de um ambiente WSL gerando primeiro os arquivos e, em seguida, executando-o como um servidor estático:

``` sh
$ hexo gera
$ servidor hexo -s
```

Este é [um problema BashOnWindows](https://github.com/Microsoft/BashOnWindows/issues/216)conhecido e, em 15 de agosto de 2016, a equipe do Windows disse que iria trabalhar nele. You can get progress updates and encourage them to prioritize it on [the issue's UserVoice suggestion page](https://wpdev.uservoice.com/forums/266908-command-prompt-console-bash-on-ubuntu-on-windo/suggestions/13469097-support-for-filesystem-watchers-like-inotify).

## Erro ao renderizar modelo

Às vezes, ao executar o comando `$ hexo gera` ele retorna um erro:

```
FATAL alguma coisa está errada. Talvez você possa encontrar a solução aqui: http://hexo.io/docs/troubleshooting.html
Erro de renderização do template: (caminho desconhecido)
```

Possível causa:
- Há algumas palavras irreconhecíveis em seu arquivo, por exemplo, tamanho zero invisível.
- Uso ou limitação incorreta do plugin [tag](/docs/tag-plugins).
  * Plugin de tag estilo bloco com conteúdo não está entre blocos e `{% endplugin_name %}`
  ```
  #
  {% codeblock %}
  fn()
  {% codeblock %}

  # Incorreta
  {% codeblock %}
  fn()

  # Corrigir
  {% codeblock %}
  fn()
  {% endcodeblock %}
  ```
  * Tendo sintaxe como Nunjucks em um plugin de tags, por exemplo,
[`{#`](https://mozilla.github.io/nunjucks/templating.html#comments). Uma solução alternativa para esse exemplo é usar [triple backtick](/docs/tag-plugins#Backtick-Code-Block). [A seção de conteúdo de escape](/docs/troubleshooting#Escape-Contents) tem mais detalhes. 
    
    
  ```
  {% codeblock lang:bash %}
  Tamanho do array é ${#ARRAY}
  {% endcodeblock %}
  ```
</p></li> </ul></li> </ul> 



## YAMLException (Issue [#4917](https://github.com/hexojs/hexo/issues/4917))

Atualizar para `hexo^6.1.0` a partir de uma versão mais antiga pode causar o seguinte erro ao executar `$ hexo generate`:



```
YAMLException: A lista especificada de tipos YAML (ou um único tipo de objeto) contém um objeto não-tipo.
    às ...
```


Isto pode ser causado por uma dependência incorreta (ex: `js-yaml`) definição que não pode ser resolvida automaticamente pelo gerenciador de pacotes, e você pode ter que atualizá-la manualmente: 



```sh
$ npm install js-yaml@latest
```


ou


```sh
$ yarn add js-yaml@latest
```


se você usa `yarn`.

[Armazém]: https://github.com/hexojs/warehouse
[Swig]: https://node-swig.github.io/swig-templates/
[Nunjucks]: https://mozilla.github.io/nunjucks/
