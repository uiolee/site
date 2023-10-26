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

O YAML acima é a configuração padrão do Hexo.

## Desabilitado

```yaml
# _config.yml
highlight:
  enable: false
prismjs:
  enable: false
```

Quando ambos `highlight.enable` e `prismjs.` nable are `false`, o HTML de saída do bloco de código é controlado pelo renderizador correspondente. Por exemplo, [`marcada. s`](https://github.com/markedjs/marked) (usado por [`hexo-renderer-marked`](https://github.com/hexojs/hexo-renderer-marked), o renderizador padrão de markdown do Hexo) irá adicionar o código de idioma para a classe `` de `<code>`:

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

Quando nenhum destaque de sintaxe embutido estiver ativado, você pode instalar um plugin de realce de sintaxe de terceiros, ou usar um hileter de sintaxe do lado do navegador (e. . `highlight.js` e `prism.js` ambos suportam rodando no navegador).

## Highlight.js

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

`destaque. s` é habilitado por padrão e usado como realce no lado do servidor em Hexo; precisa ser desativado se você prefere destacar `. s` no lado do navegador.

> Server-side means the syntax highlight is generated during `hexo generate` or `hexo server`.

### Detectar_automaticamente

`auto_detect` é um recurso `highlight.js` que detecta automaticamente o idioma do bloco de código.

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

Somente embrulha com `<pre><code class="lang"></code></pre>` e não irá renderizar todas as tags(`span`, e `br`) no conteúdo se são idiomas iguais a esta opção.

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

Prismjs está desativado por padrão. Você deve definir `highlight.enable` para `false` antes de habilitar o prismjs.

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
- [Plugin de Tag - Bloco de código](https://github.com/hexojs/hexo/blob/master/lib/plugins/tag/code.js)
- [Plugin de Tag - Bloco de Código Backtick](https://github.com/hexojs/hexo/blob/master/lib/plugins/filter/before_post_render/backtick_code_block.js)
