---
title: Modelos
---

Os templates definem a apresentação do seu site, descrevendo o que cada página deve ter de semelhante. A tabela abaixo mostra o modelo correspondente para cada página disponível. No mínimo, um tema deve conter um template de `index`.

{% youtube mb65bQ4iUc4 %}

| Modelo       | Página              | Fallback  |
| ------------ | ------------------- | --------- |
| `Índice`     | Página Home         |           |
| `publicação` | Postagens           | `Índice`  |
| `Página`     | Páginas             | `Índice`  |
| `arquivo`    | Arquivos (archives) | `Índice`  |
| `Categoria`  | Categorias          | `arquivo` |
| `Etiqueta`   | Tags                | `arquivo` |

## Layouts

Quando as páginas compartilham uma estrutura semelhante - por exemplo, quando dois templates possuem um cabeçalho e um rodapé - você pode considerar usar um `layout` para declarar essas semelhanças estruturais. Todo arquivo de layout deve conter uma variável `body` para exibir o conteúdo do template em questão. Por exemplo:

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

Por padrão, o template de `layout` é usado por todos os outros templates. Você pode especificar layouts adicionais no [front-matter](front-matter.html) ou configurá-lo como `false` para desativá-lo. É até possível criar uma estrutura aninhada complexa ao incluir mais templates de layout no seu layout principal.

## Parciais

Os partials são úteis para compartilhar componentes entre seus templates. Um exemplo típico inclui cabeçalhos (header), rodapés (footer) ou barras laterais (sidebar). Você pode querer colocar seus partials em arquivos separados para tornar a manutenção do seu site significativamente mais conveniente. Por exemplo:

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

Você pode definir variáveis locais em um template e usá-las em outros templates.

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

Se o seu tema for extremamente complexo ou se o número de arquivos a serem gerados for muito grande, o desempenho da geração de arquivos do Hexo pode começar a diminuir consideravelmente. Além de simplificar o seu tema, você também pode tentar usar o `Fragment Caching`, que foi introduzido no Hexo 2.7.

Este recurso foi emprestado do [Ruby on Rails](http://guides.rubyonrails.org/caching_with_rails.html#fragment-caching). Isso faz com que o conteúdo seja salvo de forma fragmentada e cacheado para quando requisições adicionais forem feitas. Isso pode reduzir o número de consultas no banco de dados e também pode acelerar a geração de arquivos.

O recurso de `Fragment Caching` é melhor aproveitado em cabeçalhos, rodapés, barras laterais e outros conteúdos estáticos, onde sejam feitas pouquíssimas mudanças de um template para outro. Por exemplo:

``` js
<%- fragment_cache('cabeçalho', function(){
  return '<header></header>';
});
```

Embora seja mais fácil usar partials:

``` js
<%- partial('cabeçalho', {}, {cache: true});
```

{% note warn %}
`fragment_cache()` irá armazenar em cache o resultado renderizado e a saída em cache para outras páginas. Isso só deve ser usado em partes que são esperadas **não** para mudar em diferentes páginas. Otherwise, it should **not** be enabled. Por exemplo, ele deve ser desativado quando o `relative_link` é ativado na configuração. Isso porque links relativos podem aparecer de forma diferente nas páginas.
{% endnote %}
