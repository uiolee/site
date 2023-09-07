---
title: Gerador
---

Um gerador constrói rotas com base em arquivos processados.

## Sinopse

``` js
hexo.extend.generator.register(name, function(locals){
  // ...
});
```

Um argumento `locais` será passado para a função, contendo as variáveis [do site](../docs/variables.html#Site-Variables). Você deve usar esse argumento para obter os dados do site, evitando ter que acessar o banco de dados diretamente.

## Atualizar rotas

``` js
hexo.extend.generator.register('test', function(locals){
  // Object
  return {
    path: 'foo',
    data: 'foo'
  };

  // Array
  return [
    {path: 'foo', data: 'foo'},
    {path: 'bar', data: 'bar'}
  ];
});
```

| Atributo  | Descrição:                                                                                                                                             |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `caminho` | Caminho não incluindo o prefixo `/`.                                                                                                                   |
| `Dados`   | Dado                                                                                                                                                   |
| `layout`  | Leiaute Especifique os layouts para renderização. O valor pode ser uma string ou uma matriz. Se é ignorado então a rota retornará `dados` diretamente. |

Quando os arquivos de origem são atualizados, o Hexo executará todos os geradores e reconstruirá as rotas. **Please return the data and do not access the router directly.**

## Exemplo

### Página de arquivo

Criar uma página de arquivos em `archives/index.html`. Nós passamos todas as postagens como dados para os modelos. Esses dados são equivalentes à variável `página` nos templates.

Em seguida, defina o atributo `layout` para renderizar com os templates do tema. Estamos definindo dois layouts nesse exemplo: se o layout `archive` não existir, o layout `índice` será usado.

``` js
hexo.extend.generator.register('archive', function(locals){
  return {
    path: 'archives/index.html',
    data: locais,
    layout: ['archive', 'index']
  }
});
```

### Página de arquivo com paginação

Você pode usar a conveniente ferramenta oficial [hexo-paginação][] para facilmente construir páginas de arquivos com paginação.

``` js
var pagination = require('hexo-pagination');

hexo.extend.generator.register('archive', function(locals){
  // hexo-paginação faz um índice. tml para a rota /archives
  return pagination('archives', locais. ostos, {
    perpágina: 10,
    layout: ['archive', 'index'],
    data: {}
  });
});
```

### Gerar todas as postagens

Iterar sobre todos os posts em `locals.posts` e criar rotas para todos os posts.

``` js
hexo.extend.generator.register('post', function(locals){
  return locals.posts.map(function(post){
    return {
      path: post.path,
      data: post,
      layout: 'post'
    };
  });
});
```

### Copiar Arquivos

Desta vez nós não retornamos os dados explicitamente, mas, em vez disso, definimos `dados` para uma função para que a rota construa `fs. eadStream` apenas quando necessário.

``` js
var fs = require('hexo-fs');

hexo.extend.generator.register('asset', function(locals){
  return {
    path: 'file.txt',
    data: function(){
      return fs.createReadStream('path/to/file.txt')
    }
  };
});
```

[hexo-paginação]: https://github.com/hexojs/hexo-pagination
