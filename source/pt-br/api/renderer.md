---
title: Renderizador
---

Um renderizador é usado para processar o conteúdo.

## Sinopse

``` js
hexo.extend.renderer.register(name, output, function(data, options){
  // ...
}, sincronizar);
```

| Argumento     | Descrição:                                                     |
| ------------- | -------------------------------------------------------------- |
| `Nome`        | A extensão do arquivo de entrada (minúsculas, sem liderar `.`) |
| `saída`       | A extensão do arquivo de saída (minúsculas, sem liderar `.`)   |
| `sincronizar` | Modo de sincronização                                          |

Três argumentos serão passados para a função render:

| Argumento  | Descrição:                                                                                                         |
| ---------- | ------------------------------------------------------------------------------------------------------------------ |
| `Dados`    | Inclua dois atributos: caminho `caminho` e conteúdo do arquivo `texto`. `caminho` não vai necessariamente existir. |
| `opção`    | Opções                                                                                                             |
| `callback` | Função de retorno de chamada de dois parâmetros `err`, `valor`.                                                    |

## Exemplo

### Modo assíncrono

``` js
var stylus = require('stylus');

// Callback
hexo.extend.renderer.register('styl', 'css', function(dados, opções, callback){
  stylus(data.text).set('filename', data.path). ender(callback);
});

// Promessa
hexo.extend.renderer. egister('styl', 'css', function(data, options){
  return new Promise(function(resolve, reject){
    resolve('test');
  });
});
```

### Modo de Sincronização

``` js
var ejs = require('ejs');

hexo.extend.renderer.register('ejs', 'html', function(data, options){
  options.filename = data.path;
  return ejs.render(data.text, options);
}, true);
```

### Desativar Nunjucks tags

Nunjucks tags `{{ }}` ou `{% %}` (utilizado por [tag plugin](/docs/tag-plugins)) são processados por padrão, para desativar:

``` js
function lessFn(data, options) {
  // faz algo
}

lessFn.disableNunjucks = true

hexo.extend.renderer.register('less', 'css', lessFn);
```
