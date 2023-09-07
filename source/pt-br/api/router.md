---
title: Roteador
---

O roteador salva todos os caminhos usados no site.

## Obter um caminho

O método `recebe` retorna um [Stream][]. Por exemplo, para salvar os dados do caminho para um destino especificado:

``` js
var dados = hexo.route.get('index.html');
var dest = fs.createWriteStream('somewhere');

data.pipe(dest);
```

## Definir um caminho

O método `define` recebe uma string, um [Buffer][] ou uma função.

``` js
// String
hexo.route.set('index.html', 'index')

// Buffer
hexo.route.set('index.html', new Buffer('index'));

// Função (Promise)
hexo.route.set('index. tml', function(){
  return new Promise(function(resolve, reject){
    resolve('index');
  });
});

// Função (Callback)
hexo. oute.set('index.html', function(callback){
  callback(null, 'index');
});
```

Você também pode definir um booleano para se um caminho foi modificado ou não. Isso pode acelerar a geração de arquivo, pois permite ignorar os arquivos não modificados.

``` js
hexo.route.set('index.html', {
    data: 'index',
    modified: false
});

// hexo.route.isModified('index.html') => false
```

## Remover um caminho

``` js
hexo.route.remove('index.html');
```

## Obter a lista de rotas

``` js
hexo.route.list();
```

## Formatar um caminho

O método `formato` transforma uma string em um caminho válido.

``` js
hexo.route.format('archives/');
// archives/index.html
```

[Stream]: http://nodejs.org/api/stream.html
[Buffer]: http://nodejs.org/api/buffer.html
