---
title: Soluções de Problemas
---

No caso de você ter problemas com o uso do Hexo, aqui está uma lista de soluções para alguns dos problemas mais frequentes. Se esta página não ajudar a resolver seu problema, tente fazer uma pesquisa no nosso [GitHub](https://github.com/hexojs/hexo/issues) ou no nosso [Google Group](https://groups.google.com/group/hexo).

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

Certifique-se de que está usando indentação por espaço (soft tabs) e adicione um espaço após os dois pontos.

Para mais informações, veja [YAML Spec](http://www.yaml.org/spec/1.2/spec.html).

## Erro de EMFILE

``` plain
Erro: EMFILE, muitos arquivos abertos
```

Embora o Node.js tenha I/O não bloqueante, o número máximo de I/O síncronas ainda é limitado pelo sistema. Você pode encontrar um erro EMFILE ao tentar gerar uma grande quantidade de arquivos. Você pode tentar executar o seguinte comando para aumentar o número de operações de I/O síncronas permitidas.

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

## Processos com Pouca Memória

Quando você encontrar esse erro durante a geração:

```
ERRO FATAL: CALL_AND_RETRY_LAST Alocação falhou - processo sem memória
```

Aumente o tamanho da memória heap do Node.js alterando a primeira linha de `hexo-cli` (o comando `which hexo` encontra o arquivo).

```
#!/usr/bin/env node --max_old_space_size=8192
```

[Sem memória ao gerar um enorme blog · Problema #1735 · hexojs/hexo](https://github.com/hexojs/hexo/issues/1735)

## Problemas de Deploy com Git

### RPC falhou

``` plain
erro: RPC falhou; result=22, código HTTP = 403

fatal: 'username.github.io' não parece ser um repositório git
```

Certifique-se de ter [configurado o git](https://help.github.com/articles/set-up-git) corretamente no seu computador ou tente usar a URL HTTPS do repositório ao invés da URL SSH.

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

## Problemas de Servidor

``` plain
Error: listen EADDRINUSE
```

Você pode ter iniciado dois servidores do Hexo ao mesmo tempo ou pode haver outro aplicativo usando a mesma porta. Tente modificar a configuração `port` ou iniciar o servidor do Hexo com o argumento `-p`.

``` bash
$ servidor hexo -p 5000
```

## Problemas na Instalação de Plugins

``` plain
ERRO npm! configurar compilação de node-waf
```

Este erro pode ocorrer ao tentar instalar um plugin escrito em C, C++ ou outra linguagem diferente de JavaScript. Verifique se você instalou o compilador correto em seu computador.

## Error com DTrace (Mac OS X)

```plain
{ [Erro: Não foi possível encontrar o módulo './build/Release/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
{ [Erro: Não foi possível encontrar o módulo '. build/default/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
{ [Erro: Não foi possível encontrar o módulo './build/Debug/DTraceProviderBindings'] código: 'MODULE_NOT_FOUND' }
```

A instalação do DTrace pode ter problemas, use isso:

```sh
$ npm install hexo --no-optional
```

Veja a issue [#1326](https://github.com/hexojs/hexo/issues/1326#issuecomment-113871796) no Github.

## Iterando o Modelo de Dados em Jade ou Swig

A Hexo usa [Warehouse][] para o seu modelo de dados. Ele não é um array, então você pode ter que transformar objetos em iteráveis.

```
{% for post in site.posts.toArray() %}
{% endfor %}
```

## Dados não Atualizados

Alguns dados não podem ser atualizados ou os arquivos recém-gerados são idênticos aos da última versão. Limpe o cache e tente novamente.

``` bash
Limpeza de $ hexos
```

## Nenhum Comando é Executado

Quando você não consegue executar nenhum comando do Hexo, com exceção de `help`, `init` e `version`, isso pode estar acontecendo pela falta do `hexo` no `package.json`:

```json
{
  "hexo": {
    "version": "3.2.2"
  }
}
```

## Conteúdo Escapando

O Hexo usa [Nunjucks][] para renderizar posts ([Swig][] foi usado na versão mais antiga, que compartilha uma sintaxe semelhante). O conteúdo delimitado com `{{ }}` ou `{% %}` será "parseado" e pode causar problemas. Você pode empacotar um conteúdo sensível com a tag plugin [`raw`](/docs/tag-plugins#Raw), single backtick `` `{{ }}` `` or triple backtick. Alternativamente, as tags Nunjucks podem ser desativadas através da opção do renderizador (se suportado), [API](/api/renderer#Disable-Nunjucks-tags) ou [front-matter](/docs/front-matter).

```
{% raw %} Hello {{ world }}
{% endraw %}
```

````
``` Hello {{ world }}
```
````

## ENOSPC Error (Linux)

Às vezes, ao executar o comando `$ hexo server` é retornado o seguinte erro:

```
Erro: watch ENOSPC ...
```

Isto pode ser consertado através do comando `$ npm dedupe` ou, se isso não funcionar, tente o seguinte comando no terminal do Linux:

```
$ echo fs.inotify.max_user_watches=524288 ➲ sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

Isso aumentará o limite do número de arquivos que você pode assistir.

## Erro do EMPERM (Subsistema do Windows para Linux)

Ao executar `$ hexo server` em um ambiente BashOnWindows, ele retorna o seguinte erro:

```
Erro: watch /path/to/hexo/theme/ EMPERM
```

Infelizmente, o WSL (Windows Subsystem for Linux) atualmente não suporta os observadores (watchers) do sistema de arquivos. Portanto, o recurso de atualização em tempo real do servidor do Hexo não está disponível no momento. Contudo, ainda é possível executar o servidor a partir de um ambiente WSL, primeiro gere os arquivos e depois execute servidor em modo estático:

``` sh
$ hexo gera
$ servidor hexo -s
```

Este é [um problema no BashOnWindows conhecido](https://github.com/Microsoft/BashOnWindows/issues/216), e em 15 de agosto de 2016, a equipe do Windows disse que eles trabalhariam nisso. Você pode obter atualizações de progresso e encorajá-los a priorizá-lo na [página UserVoice do problema](https://wpdev.uservoice.com/forums/266908-command-prompt-console-bash-on-ubuntu-on-windo/suggestions/13469097-support-for-filesystem-watchers-like-inotify).

## Erro de Renderização de Template

Às vezes, ao executar o comando `$ hexo generate`, ele retorna um erro:

```
FATAL alguma coisa está errada. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html Template render error: (unknown path)
```

Possível causa:
- One possible reason is that there are some unrecognizable words in your file, e.g. invisible zero width characters.
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



## Delimite a string com aspas duplas se ela contiver dois pontos (:).

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

[Warehouse]: https://github.com/hexojs/warehouse
[Swig]: http://paularmstrong.github.io/swig/
[Nunjucks]: https://mozilla.github.io/nunjucks/
