---
title: Modelos
---

Modelos definem a apresentação do seu site descrevendo como cada página deve parecer. A tabela abaixo mostra o modelo correspondente para cada página disponível. No mínimo, um tema deve conter um template `índice`.

{% youtube mb65bQ4iUc4 %}

| Modelo       | Página                | Fallback  |
| ------------ | --------------------- | --------- |
| `Índice`     | Página principal      |           |
| `publicação` | Postagens             | `Índice`  |
| `Página`     | páginas               | `Índice`  |
| `arquivo`    | Arquivos              | `Índice`  |
| `Categoria`  | Arquivos de categoria | `arquivo` |
| `Etiqueta`   | Arquivos da tag       | `arquivo` |

## Layouts

Quando as páginas compartilham uma estrutura similar - por exemplo, quando dois templates tiverem um cabeçalho e um rodapé - você pode considerar usar um `layout` para declarar essas semelhanças estruturais. Todos os arquivos de layout devem conter uma variável `corpo` para exibir o conteúdo do template em questão. Por exemplo:

``` html index.ejs
Índice
```

``` html layout.ejs
<!DOCTYPE html>
<html>
  <body><%- corpo %></body>
</html>
```

rendimentos:

``` html
<!DOCTYPE html>
<html>
  <body>index</body>
</html>
```

Por padrão, o modelo `layout` é usado por todos os outros templates. Você pode especificar layouts adicionais na front-matter ou configurá-lo como `false` para desativá-lo. É até possível construir uma estrutura aninhada complexa, incluindo mais modelos de layout no seu layout superior.

## Parciais

Parciais são úteis para o compartilhamento de componentes entre seus templates. Exemplos típicos incluem cabeçalhos, rodapés ou barras laterais. Você pode querer colocar seus Parceiros em arquivos separados para tornar a manutenção do seu site significativamente mais conveniente. Por exemplo:

``` html partial/header.ejs
<h1 id="logo"><%= config.title %></h1>
```

``` html index.ejs
<%- partial('partial/header') %>
<div id="content">Página inicial</div>
```

rendimentos:

``` html
<h1 id="logo">Meu Site</h1>
<div id="content">Página Inicial</div>
```

## Variáveis Locais

É possível definir variáveis locais em modelos e usá-las em outros templates.

``` html partial/header.ejs
<h1 id="logo"><%= título %></h1>
```

``` html index.ejs
<%- partial('partial/header', {title: 'Hello World'}) %>
<div id="content">Página Inicial</div>
```

rendimentos:

``` html
<h1 id="logo">Olá Mundo</h1>
<div id="content">Página Inicial</div>
```

## Otimização

Se o seu tema é extremamente complexo ou se o número de arquivos a gerar se tornar muito grande, O desempenho da geração de arquivo de Hexo pode começar a diminuir consideravelmente. Além de simplificar seu tema, você também pode experimentar Cache de Fragmento, que foi introduzido no Hexo 2.7.

Este recurso foi emprestado de [Ruby on Rails](http://guides.rubyonrails.org/caching_with_rails.html#fragment-caching). Faz com que o conteúdo seja salvo como fragmentos e armazenado em cache quando solicitações adicionais são feitas. Isso pode reduzir o número de consultas de banco de dados e também pode acelerar a geração de arquivos.

O cache de fragmento é melhor usado para cabeçalhos, rodapés, barras laterais ou outros conteúdos estáticos que é improvável que mudem de modelo para modelo. Por exemplo:

``` js
<%- fragment_cache('cabeçalho', function(){
  return '<header></header>';
});
```

Embora possa ser mais fácil usar parciais:

``` js
<%- partial('cabeçalho', {}, {cache: true});
```

{% note warn %}
`fragment_cache()` irá armazenar em cache o resultado renderizado e a saída em cache para outras páginas. Isso só deve ser usado em partes que são esperadas **não** para mudar em diferentes páginas. Otherwise, it should **not** be enabled. Por exemplo, ele deve ser desativado quando o `relative_link` é ativado na configuração. Isso porque links relativos podem aparecer de forma diferente nas páginas.
{% endnote %}
