---
title: filtro
---

Um `filter` (filtro) pode ser utilizado para modificar alguns dados. O Hexo passa os dados para filtros em sequência e os filtros, então, modificam esses dados um após o outro. Este é o mesmo conceito utilizado pelo [WordPress](http://codex.wordpress.org/Plugin_API#Filters).

## Resumo

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

Você pode definir uma prioridade específica para cada filtro (parâmetro `priority` no exemplo acima). Baixa `prioridade` significa que ela será executada primeiro. A prioridade padrão é 10. Recomendamos usar um valor de prioridade de usuário configurável que o usuário pode especificar na configuração, por exemplo, `hexo.config.your_plugin.priority`.

## Executar Filtros

``` js
hexo.extend.filter.exec(type, data, opções);
hexo.extend.filter.execSync(type, data, opções);
```

| Opção      | Descrição                      |
| ---------- | ------------------------------ |
| `contexto` | Contexto                       |
| `args`     | Argumentos. Deve ser um array. |

O primeiro argumento passado para cada filtro é `data`. O próximo filtro da sequência pode receber o argumento `data` modificado ao se retornar um novo valor. Se nada for retornado, `data` continua intacto. Você ainda pode utilizar `args` para especificar outros argumentos dentro dos filtros. Por exemplo:

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

Você também pode utilizar os seguintes métodos para executar filtros:

``` js
hexo.execFilter(type, data, options);
hexo.execFilterSync(type, data, options);
```

## Remover Filtros

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

## Lista de Filtros

Abaixo são listados os filtros utilizados pelo Hexo.

### renderização_de_postagem_anterior

Executado antes de uma postagem ser renderizada. Verificar a seção [Renderizar](posts.html#Renderizar) para saber mais sobre as etapas de execução.

Por exemplo, para se transformar um título em _caixa baixa_:

``` js
hexo.extend.filter.register('before_post_render', function(data){
  data.title = data.title.toLowerCase();
  return data;
});
```

### renderizar_post_depois

Executado após a postagem ser renderizado. Verificar a seção [Renderizar](posts.html#Renderizar) para saber mais sobre as etapas de execução.

Por exemplo, para substituir `@username` por um link para o perfil do Twitter:

``` js
hexo.extend.filter.register('after_post_render', function(data){
  data.content = data.content.replace(/@(\d+)/, '<a href="http://twitter.com/$1">#$1</a>');
  return data;
});
```

### saída_anterior

Executado quando o Hexo está prestes a ser terminado -- isso será executado logo após `hexo.exit` ser chamado.

``` js
hexo.extend.filter.register('before_exit', function(){
  // ...
});
```

### gerar_antes

Executado antes do processo de geração ser iniciado.

``` js
hexo.extend.filter.register('before_generate', function(){
  // ...
});
```

### gerar_depois

Executado após o processo de geração ser concluído.

``` js
hexo.extend.filter.register('after_generate', function(){
  // ...
});
```

### template_locals

Modifica as [variáveis locais](../docs/variables.html) nos templates.

Por exemplo, para adicionar a hora atual às variáveis locais dos templates:

``` js
hexo.extend.filter.register('template_locals', function(locals){
  locals.now = Date.now();
  return locals;
});
```

### Entrar_depois

Executado após a inicialização do Hexo -- este será executado logo após `hexo.init` ser concluído.

``` js
hexo.extend.filter.register('after_init', function(){
  // ...
});
```

### novo_caminho_post

Executado ao criar uma postagem para determinar o caminho das novas postagens.

``` js
hexo.extend.filter.register('new_post_path', function(data, replace){
  // ...
});
```

### post_permalink

Usado para determinar os links permanentes das postagens.

``` js
hexo.extend.filter.register('post_permalink', function(data){
  // ...
});
```

### depois_renderização

Executado após a renderização ser terminada. Mais informações podem ser encontradas na seção de [renderização](rendering.html#Filtros-after-render).

### após_limpeza

Executados após os arquivos serem gerados e o cache ser removido com o comando `hexo clean`.

``` js
hexo.extend.filter.register('after_clean', function(){
  // remove alguns outros arquivos temporários
});
```

### middleware

Adiciona um middleware ao servidor. `app` é uma instância de [Connect][].

Por exemplo, para adicionar `X-Powered-By: Hexo` ao cabeçalho de resposta:

``` js
hexo.extend.filter.register('server_middleware', function(app){
  app.use(function(req, res, next){
    res.setHeader('X-Powered-By', 'Hexo');
    next();
  });
});
```

[Connect]: https://github.com/senchalabs/connect
