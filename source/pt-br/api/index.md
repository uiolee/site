---
title: API
---

Esta documentação fornece informações mais detalhadas sobre a API e será particularmente útil para pessoas que querem modificar o código-fonte Hexo ou escrever novos plugins. Se você estiver interessado no uso mais básico do Hexo, consulte em vez disso a documentação [](../docs).

Por favor, note que esta documentação só é válida para Hexo 3 ou superior.

## Inicializar

Primeiro, temos de criar uma instância Hexo. Uma nova instância tem dois argumentos: o diretório raiz do site, `base_dir`, e um objeto que contém as opções de inicialização. Em seguida, vamos inicializar esta instância chamando o método `init` nela, o que então fará com que o Hexo carregue suas configurações e plugins.

``` js
var Hexo = require('hexo');
var hexo = new Hexo(process.cwd(), {});

hexo.init().then(function(){
  // ...
});
```

| Alternativa              | Descrição:                                                                                                         | Padrão                         |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------ | ------------------------------ |
| `debug`                  | Ativar modo de depuração. Exibir mensagens de depuração no terminal e salvar o `debug.log` no diretório raiz.      | `Falso`                        |
| `seguro`                 | Ativar modo de segurança. Não carregue nenhum plug-in.                                                             | `Falso`                        |
| `silencioso`             | Ativar modo silencioso. Não exiba nenhuma mensagem no terminal.                                                    | `Falso`                        |
| `configuração`           | Especifique o caminho do arquivo de configuração.                                                                  | `_config.yml`                  |
| `rascunho` / `rascunhos` | Habilitar para adicionar rascunhos à lista de postagens.<br> exemplo: quando usar `hexo.locals.get('posts')` | `render_drafts` of _config.yml |

## Carregar Arquivos

Hexo fornece dois métodos para carregar arquivos: `carregar` e `watch`. `load` is used for loading all files in the `source` folder as well as the theme data. `Assistir` faz as mesmas coisas que o `carregar` faz, mas também começará a observar por mudanças contínuas nos arquivos.

Ambos os métodos irão carregar a lista de arquivos e passá-los para os processadores correspondentes. Depois de todos os arquivos terem sido processados, eles vão pedir aos geradores que criem as rotas.

``` js
hexo.load().then(function(){
  // ...
});

hexo.watch().then(function(){
  // Depois você pode chamar hexo.unwatch() para parar de assistir.
});
```

## Executar comandos

Qualquer comando do console pode ser chamado explicitamente usando o `chama` método na instância Hexo. Tal chamada recebe dois argumentos: o nome do comando do console e um argumento de opções. Diferentes opções estão disponíveis para os diferentes comandos do console.

``` js
hexo.call('gerar', {}).then(function(){
  // ...
});
```

``` js
hexo.call('list', { _: ['post'] }).then(function() {
  // ...
})
```

## Sair

Você deve chamar o método `exit` após a conclusão bem sucedida de um comando do console. Isso permite ao Hexo sair graciosamente e terminar coisas importantes, como salvar o banco de dados.

``` js
hexo.call('generate').then(function(){
  return hexo.exit();
}).catch(function(err){
  return hexo.exit(err);
});
```
