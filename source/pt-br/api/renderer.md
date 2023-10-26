---
title: Renderizador
---

Um `renderer` é utilizado para renderizar conteúdos.

## Resumo

``` js
hexo.extend.renderer.register(name, output, function(data, options){
  // ...
}, sincronizar);
```

| Argumento     | Descrição                                                       |
| ------------- | --------------------------------------------------------------- |
| `Nome`        | Extensão do arquivo de entrada (caixa baixa, sem o `.` inicial) |
| `saída`       | Extensão do arquivo de saída (caixa baixa, sem o `.` inicial)   |
| `sincronizar` | Modo de sincronização                                           |

Dois argumentos devem ser passados para a função renderer:

| Argumento  | Descrição                                                                                                                |
| ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| `Dados`    | Inclui dois atributos: Caminho do arquivo (`path`) e o conteúdo do arquivo (`text`). Não é necessário que `path` exista. |
| `opção`    | Opções                                                                                                                   |
| `callback` | Função de retorno de chamada de dois parâmetros `err`, `valor`.                                                          |

## Exemplo

### Modo Assíncrono

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

### Modo Síncrono

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
