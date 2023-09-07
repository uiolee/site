---
title: Migrator
---

Um migrador ajuda usuários a migrar de outros sistemas para o Hexo.

## Sinopse

``` js
hexo.extend.migrator.register(name, function(args){
  // ...
});
```

Um argumento `args` será passado para a função. Esse argumento conterá a entrada do usuário no terminal.
