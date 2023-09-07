---
title: filtro
---

Um filtro é usado para modificar alguns dados especificados. Hexo passa os dados para os filtros em sequência e os filtros então modifica os dados um após o outro. Este conceito foi emprestado do WordPress [WordPress](http://codex.wordpress.org/Plugin_API#Filters).

## Sinopse

``` js
hexo.extend.filter.register(type, function() {
  // Configuração do usuário
  const { config } = this;
  if (config.external_link.enable) // fazer algo...

  // Configuração do tema
  const { config: themeCfg } = this.theme;
  if (themeCfg.fancybox) // fazer algo...

}, prioridade);
```

You can define the `priority`. Baixa `prioridade` significa que ela será executada primeiro. A prioridade `padrão` é 10. Recomendamos usar um valor de prioridade de usuário configurável que o usuário pode especificar na configuração, por exemplo, `hexo.config.your_plugin.priority`.

## Executar Filtros

``` js
hexo.extend.filter.exec(type, data, opções);
hexo.extend.filter.execSync(type, data, opções);
```

| Alternativa | Descrição:                            |
| ----------- | ------------------------------------- |
| `contexto`  | Contexto                              |
| `args`      | Argumentos. Isto deve ser uma matriz. |

O primeiro argumento passado para cada filtro é `dados`. O `dado` passado para o próximo filtro pode ser modificado retornando um novo valor. Se nada for retornado, os dados não serão modificados. Você pode até usar `args` para especificar outros argumentos em filtros. Por exemplo:

``` js
filtro hexo.extend.filter. egister('teste', função(dado, arg1, arg2){
  // dados === 'alguns dados'
  // arg1 === 'foo'
  // arg2 === 'bar'

  return 'algo';
});

hexo. xtend.filter.register('test', function(data, arg1, arg2){
  // dados === 'algo'
});

hexo. xtend.filter.exec('test', 'alguns dados', {
  arges: ['foo', 'bar']
});
```

Você também pode usar os seguintes métodos para executar os filtros:

``` js
hexo.execFilter(type, data, options);
hexo.execFilterSync(type, data, options);
```

## Desregistrar Filtros

``` js
hexo.extend.filter.unregister(tipo, filtro);
```

**Exemplo**

``` js
// Desregistra um filtro que é registrado com a função nomeada

const filterFn = (data) => {
  data = 'algo';
  retorna dados;
};
hexo. xtend.filter.register('exemplo', filterFn);

hexo.extend.filter.unregister('exemplo', filterFn);
```

``` js
// Desregistra um filtro registrado com o módulo commonjs

hexo.extend.filter.register('example', require('path/to/filter'));

hexo.extend.filter.unregister('example', require('path/to/filter'));
```

## Lista de filtros

Aqui está uma lista de filtros usados por Hexo.

### renderização_de_postagem_anterior

Executado antes de um post ser renderizado. Consulte a renderização [post](posts.html#Render) para aprender as etapas de execução.

Por exemplo, para transformar o título em maiúsculas e minúsculas:

``` js
hexo.extend.filter.register('before_post_render', function(data){
  data.title = data.title.toLowerCase();
  return data;
});
```

### renderizar_post_depois

Executado depois que um post é renderizado. Consulte a renderização [post](posts.html#Render) para aprender as etapas de execução.

Por exemplo, para substituir `@username` por um link para um perfil do Twitter:

``` js
hexo.extend.filter.register('after_post_render', function(data){
  data.content = data.content.replace(/@(\d+)/, '<a href="http://twitter.com/$1">#$1</a>');
  return data;
});
```

### saída_anterior

Executado antes que Hexo esteja prestes a sair -- isto será executado logo após a chamada `hexo.exit`.

``` js
hexo.extend.filter.register('before_exit', function(){
  // ...
});
```

### gerar_antes

Executado antes do início da geração.

``` js
hexo.extend.filter.register('before_generate', function(){
  // ...
});
```

### gerar_depois

Executado depois que a geração termina.

``` js
hexo.extend.filter.register('after_generate', function(){
  // ...
});
```

### template_locals

Modifique [variáveis locais](../docs/variables.html) nos templates.

Por exemplo, para adicionar o tempo atual às variáveis locais de templates:

``` js
hexo.extend.filter.register('template_locals', function(locals){
  locals.now = Date.now();
  return locals;
});
```

### Entrar_depois

Executado após a inicialização do Hexo -- isto será executado logo após a conclusão de `hexo.init`.

``` js
hexo.extend.filter.register('after_init', function(){
  // ...
});
```

### novo_caminho_post

Executado ao criar um post para determinar o caminho de novas postagens.

``` js
hexo.extend.filter.register('new_post_path', function(data, replace){
  // ...
});
```

### post_permalink

Usado para determinar a permalink de postagens.

``` js
hexo.extend.filter.register('post_permalink', function(data){
  // ...
});
```

### depois_renderização

Executado após a conclusão da renderização. You can see [rendering](rendering.html#after_render_Filters) for more info.

### após_limpeza

Executado após arquivos e cache gerados são removidos com o comando `hexo clean`.

``` js
hexo.extend.filter.register('after_clean', function(){
  // remove alguns outros arquivos temporários
});
```

### middleware

Adicionar middleware ao servidor. `app` é uma instância [Conectar][].

Por exemplo, para adicionar `X-Powered-By: Hexo` ao cabeçalho da resposta:

``` js
hexo.extend.filter.register('server_middleware', function(app){
  app.use(function(req, res, next){
    res.setHeader('X-Powered-By', 'Hexo');
    next();
  });
});
```

[Conectar]: https://github.com/senchalabs/connect
