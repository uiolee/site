---
title: Renderização
---

Existem dois métodos para renderizar arquivos ou strings em Hexo: o método assíncrono `hexo.render.render` e o método síncrono `hexo.render.renderSync`. Não surpreendentemente, os dois métodos são muito semelhantes, então apenas o assíncrono `hexo.render.render` será mais discutido nos parágrafos abaixo.

## Renderizar uma String

Ao renderizar uma string, você deve especificar um mecanismo `` para deixar o Hexo saber qual o mecanismo de renderização ele deve usar.

``` js
hexo.render.render({text: 'example', engine: 'swig'}).then(function(result){
  // ...
});
```

## Renderizar um Arquivo

Ao renderizar um arquivo, Não é necessário especificar um mecanismo `` porque o Hexo detectará o mecanismo de renderização relevante automaticamente com base na extensão do arquivo. Of course, you are also allowed to explicitly define the `engine`.

``` js
hexo.render.render({path: 'path/to/file.swig'}).then(function(result){
  // ...
});
```

## Opções de Renderização

Você pode passar em um objeto de opções como o segundo argumento.

``` js
hexo.render.render({text: ''}, {foo: 'foo'}).then(function(result){
  // ...
});
```

## após_renderizar Filtros

Quando a renderização estiver concluída, o Hexo executará os filtros correspondentes `after_render`. Por exemplo, podemos usar essa funcionalidade para implementar um minifier JavaScript.

``` js
var UglifyJS = require('uglify-js');

hexo.extend.filter.register('after_render:js', function(str, data){
  var result = UglifyJS.minify(str);
  return result.code;
});
```

## Verifique se um arquivo é renderizável

Use o método `isRenderable` ou `isRenderableSync` para verificar se um caminho do arquivo é renderizável. Somente quando um renderizador correspondente tiver sido registrado esse método retornará true.

``` js
hexo.render.isRenderable('layout.swig') // true
hexo.render.isRenderable('image.png') // false
```

## Obter a extensão de saída

Use o método `getOutput` para obter a extensão da saída renderizada. Se um arquivo não for renderizável, o método retornará uma string vazia.

``` js
hexo.render.getOutput('layout.swig') // html
hexo.render.getOutput('image.png') // '''
```

## Desativar Nunjucks tags

Se você não estiver usando um plugin [tag](/docs/tag-plugins) e quer usar `{{ }}` ou `{% %}` na sua publicação sem usar o conteúdo [escapando](/docs/troubleshooting#Escape-Contents), você pode desabilitar o processamento da tag Nunjucks no renderizador existente por:

``` js
// O exemplo a seguir aplica-se apenas à extensão de arquivo '.md'
// você pode precisar cobrir outras extensões, e. . '.markdown', '.mkd', etc
const renderer = hexo. ender.renderer.get('md')
if (renderer) {
  renderer.disableNunjucks = true
  hexo.extend.renderer.register('md', 'html', renderer)
}
```
