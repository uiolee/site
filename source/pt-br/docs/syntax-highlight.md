---
title: Realce de sintaxe
---

Hexo tem duas bibliotecas de destaque de sintaxe integradas, [highlight.js](https://github.com/highlightjs/highlight.js) e [prismjs](https://github.com/PrismJS/prism). Este tutorial mostra como integrar o destaque de sintaxe integrado ao Hexo no seu modelo.

## Como usar o bloco de código nas postagens

Hexo suporta duas maneiras de escrever bloco de código: [Plugin de Tag - Code Block](tag-plugins#Code-Block) e [Plugin de Tag - Backtick Code Block](https://hexo.io/docs/tag-plugins#Backtick-Code-Block):

````markdown
{% codeblock [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcodeblock %}

{% code [title] [lang:language] [url] [link text] [additional options] %}
code snippet
{% endcode %}

``` [language] [title] [url] [link text] [additional options]
code snippet
```
````
A terceira sintaxe é a sintaxe de um bloco de código de Markdown e o Hexo a estende para suportar mais recursos. Confira a [Documentação do Plugin Tag](tag-plugins#Code-Block) para descobrir as opções disponíveis.
> Dica: as postagens de suporte ao Hexo escritas em qualquer formato, por isso a extensão de renderização correspondente está instalada. It can be in markdown, ejs, swig, nunjucks, pug, asciidoc, etc. Regardless of the format used, those three code block syntax will always be available. Independentemente do formato usado, aquela sintaxe de três blocos de código estará sempre disponível.
## Configuração
below v7.0.0:

```yaml
# _configuração. ml
highlight:
  enable: true
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: ''
  exclude_languages:
    - exemplo
  wrap: true
  hljs: false
prismjs:
  enable: false
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

v7.0.0+:

```yaml
# _config.yml
syntax_highlighter: highlight.js
highlight:
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: ''
  exclude_languages:
    - example
  wrap: true
  hljs: false
prismjs:
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

O YAML acima é a configuração padrão do Hexo.

## Desabilitado

below v7.0.0:

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  enable: false
```

`auto_detect` é um recurso `highlight.js` que detecta automaticamente o idioma do bloco de código.

```yaml
# _config.yml
syntax_highlighter:  # empty
```

When both `highlight.enable` and `prismjs.enable` are `false` (below v7.0.0) or `syntax_highlighter` is empty (v7.0.0+), the output HTML of the code block is controlled by the corresponding renderer. Por exemplo, [`marcada. s`](https://github.com/markedjs/marked) (usado por [`hexo-renderer-marked`](https://github.com/hexojs/hexo-renderer-marked), o renderizador padrão de markdown do Hexo) irá adicionar o código de idioma para a classe `` de `<code>`:

````markdown
```yaml
olá: hexo
```
````

```html
<pre>
  <code class="yaml">olá: hexo</code>
</pre>
```

When no built-in syntax highlight is enabled, you can either install third-party syntax-highlight plugin, or use a browser-side syntax highlighter (e.g. `highlight.js` and `prism.js` both support running in browser).

## Highlight.js

below v7.0.0:

```yaml
# _configuração. ml
highlight:
  enable: true
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: ' '
  exclude_languages:
    - exemplo
  wrap: true
  hljs: false
prismjs:
  enable: false false
```

v7.0.0+:

```yaml
# _config.yml
syntax_highlighter: highlight.js
highlight:
  auto_detect: false
  line_number: true
  line_threshold: 0
  tab_replace: '  '
  exclude_languages:
    - example
  wrap: true
  hljs: false
```

`destaque. s` é habilitado por padrão e usado como realce no lado do servidor em Hexo; precisa ser desativado se você prefere destacar `. s` no lado do navegador.

> Server-side means the syntax highlight is generated during `hexo generate` or `hexo server`.

### Detectar_automaticamente

`auto_detect` is a `highlight.js` feature that detects language of the code block automatically.

> Dica: Quando você quiser usar "destaque da sublinguagem", habilite `auto_detect` e não marque a linguagem ao escrever um bloco de código.

{% note avise "Aviso!" %}
`auto_detect` é muito exigente em recursos. Não habilite a menos que você realmente precise do "destaque da sublinguagem" ou prefira não marcar linguagem ao escrever um bloco de código.
{% endnote %}

### número_linha

`highlight.js` [does not](https://highlightjs.readthedocs.io/en/latest/line-numbers.html) support line number.

Hexo adiciona um número de linha ao envolver a saída dentro do `<figure>` e `<table>`:

```html
<figure class="highlight yaml">
<table>
<tbody>
<tr>
  <td class="gutter">
    <pre><span class="line">1</span><br></pre>
  </td>
  <td class="code">
    <pre><span class="line"><span class="attr">hello:</span><span class="string">hexo</span></span><br></pre>
  </td>
</tr>
</tbody>
</table>
</figure>
```

Não é o comportamento do `realçado. s` e requer CSS personalizado para `<figure>` e `<table>` ; alguns temas possuem suporte embutido.

You might also notice that all `class` has no `hljs-` prefixed, we will revisit it [later part](#hljs).

### line_threshold (+6.1.0)

Aceita um limite opcional para mostrar apenas números de linha, contanto que os números de linhas do bloco de código excedam esse limite. O padrão é `0`.

### substituir_aba

Substituir guias dentro de bloco de código por uma string determinada. Por padrão são 2 espaços.

### excluir_linguagens (+6.1.0)

Only wrap with `<pre><code class="lang"></code></pre>` and will not render all tags(`span`, and `br`) in content if are languages match this option.

### embrulhar

Hexo _encapsula_ a saída dentro de `<figure>` e `<table>` para suportar o número da linha. Você precisa desativar **ambos,** `line_number` e `wrap` para reverter para o comportamento do `highlight.js`:

```html
<pre><code class="yaml">
<span class="comment"># _config.yml</span>
<span class="attr">hexo:</span> <span class="string">hexo</span>
</code></pre>
```

{% note avise "Aviso!" %}
Porque `line_number` recurso depende do `wrap`, você não pode desabilitar `wrap` com `line_number` habilitado: se você definir `line_number` para `true`, , `embrulho` será ativado automaticamente.
{% endnote %}

### hljs

Quando `hljs` estiver definido como `verdadeiro`, toda a saída HTML terá `classe` com o prefixo `hlj -` (independente de `o embrulho` está habilitado ou não):

```html
<pre><code class="yaml hljs">
<span class="hljs-comment"># _config.yml</span>
<span class="hljs-attr">hexo:</span> <span class="hljs-string">hexo</span>
</code></pre>
```

> Dica: Quando `line_number` está definido como `false`, `wrap` está definido como falso e `hljs` está definido como `verdadeiro`, você pode usar `destaque. s` [tema](https://github.com/highlightjs/highlight.js/tree/master/src/styles) diretamente no seu site.

## PrismJS

below v7.0.0:

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  enable: true
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

v7.0.0+:

```yaml
# _config.yml
syntax_highlighter: prismjs
prismjs:
  preprocess: true
  line_number: true
  line_threshold: 0
  tab_replace: ''
```

Prismjs está desativado por padrão. You should set `highlight.enable` to `false` (below v7.0.0) or set `syntax_highlighter` to `prismjs` (v7.0.0+) before enabling prismjs.

### pré-processamento

O prismjs embutido do Hexo suporta ambos browser-side (`preprocess` set to `false`) e server-side (`preprocess` set to `true`).

Quando usar o modo server-side (defina `pré-processar` para `true`), você só precisa incluir o tema prismjs (css stylesheet) em seu site. Quando usar o lado do navegador (defina `pré-processar` para `false`), você precisa incluir a biblioteca javascript também.

Prismjs é projetado para ser usado no navegador, portanto, no modo `pré-processamento` apenas o plugin prismjs limitado é suportado:

- [Números de linha](https://prismjs.com/plugins/line-numbers/): Somente `prism-linha-números.css` é necessário, não é necessário incluir `números-linha-prisma. js` no seu site. Hexo irá gerar a marcação HTML necessária para você.
- [Mostrar Idiomas](https://prismjs.com/plugins/show-language/): Hexo sempre terá atributo `idioma de dados` desde que o idioma seja dado para o bloco de código.
- Quaisquer outros plugins de prisma que não precisam de uma marcação HTML especial também são suportados, mas você terá que incluir JavaScript exigido por esses plugins.

Todos os plugins prism são suportados se `preprocess` está definido como `false`. Aqui estão algumas coisas para as quais você ainda precisa prestar atenção:

- [Números de linha](https://prismjs.com/plugins/line-numbers/): Hexo não gerará a marcação HTML necessária quando o `pré-processo` estiver definido como `false`. Requer ambos `prism-line-numbers.css` e `prism-line-numbers.js`.
- [Mostrar Idiomas](https://prismjs.com/plugins/show-language/): Hexo sempre terá atributo `idioma de dados` desde que o idioma seja dado para o bloco de código.
- [realce de linha](https://prismjs.com/plugins/line-highlight/): Tanto Hexo [Plugin de Tag - Code Block](tag-plugins#Code-Block) e [Plugin de Tag - Backtick Code Block](https://hexo.io/docs/tag-plugins#Backtick-Code-Block) suporta sintaxe de realce de linha (`mark` opção). Quando a opção `marcar` for dada, o Hexo irá gerar a marcação HTML correspondente.

### número_linha

Com ambos `pré-processamento` e `line_number` definido como `verdadeiro`, você só precisa incluir números `de linha de prisma. ss` para fazer a numeração de linha. Se você definir ambos `pré-processamento` e `line_number` para falso, você precisará ambos `prism-line-numbers.css` e `prism-line-numbers.js`.

### line_threshold (+6.1.0)

Aceita um limite opcional para mostrar apenas números de linha, contanto que os números de linhas do bloco de código excedam esse limite. O padrão é `0`.

### substituir_aba

Substituir `\t` dentro de bloco de código por uma string fornecida. Por padrão são 2 espaços.

## Outras informações úteis

- [Highlight.js](https://highlightjs.readthedocs.io/en/latest/)
- [PrismJS](https://prismjs.com/)

Os códigos de origem por trás do destaque de sintaxe do Hexo estão disponíveis em:

- [Funções de Utilitário Highlight.js](https://github.com/hexojs/hexo-util/blob/master/lib/highlight.ts)
- [Funções Utilitárias PrismJS](https://github.com/hexojs/hexo-util/blob/master/lib/prism.ts)
- [Plugin de Tag - Bloco de código](https://github.com/hexojs/hexo/blob/master/lib/plugins/tag/code.ts)
- [Plugin de Tag - Bloco de Código Backtick](https://github.com/hexojs/hexo/blob/master/lib/plugins/filter/before_post_render/backtick_code_block.ts)
