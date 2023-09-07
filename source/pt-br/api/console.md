---
title: Console
---

O console forma a ponte entre o Hexo e seus usuários. Registra e descreve os comandos disponíveis do console.

## Sinopse

``` js
hexo.extend.console.register(name, desc, opções, function(args){
  // ...
});
```

| Argumento | Descrição: |
| --------- | ---------- |
| `Nome`    | Nome:      |
| `desc`    | Descrição: |
| `Opções`  | Opções     |

Um argumento `args` será passado para a função. Esse é o argumento que os usuários digitam no terminal. É analisado por [Minimist][].

## Opções

### Uso

O uso de um comando de console. Por exemplo:

``` js
{usage: '[layout] <title>'}
// hexo new [layout] <title>
```

### argumentos

A descrição de cada argumento de um comando de console. Por exemplo:

``` js
{
  argumentos: [
    {name: 'layout', desc: 'Post layout'},
    {name: 'title', desc: 'Post title'}
  ]
}
```

### Opções

A descrição de cada opção de um comando do console. Por exemplo:

``` js
{
  options: [
    {name: '-r, --replace', desc: 'Replace existing files'}
  ]
}
```

### desc

Informações mais detalhadas sobre um comando de console.

## Exemplo

``` js
hexo.extend.console.register('config', 'Exibir configuração', function(args){
  console.log(hexo.config);
});
```

[Minimist]: https://github.com/minimistjs/minimist
