---
title: Implantador
---

Um deployer ajuda os usuários a publicarem rapidamente seu site em um servidor remoto sem comandos complicados.

## Sinopse

``` js
hexo.extend.deployer.register(name, function(args){
  // ...
});
```

Um argumento `args` será passado para a função. Contém o valor `deploy` definido em `_config.yml`, bem como os usuários de entrada exatos digitados em seu terminal.
