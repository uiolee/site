---
title: Internacionalização (i18n)
---

Você pode usar a internacionalização para apresentar seu site em diferentes idiomas. O idioma padrão é definido modificando a configuração `language` em `_config.yml`. Você também pode definir vários idiomas e modificar a ordem dos idiomas padrão.

``` yaml
idioma: zh-tw

idioma:
- zh-tw
- pt
```

### Arquivo de Idiomas

Os arquivos de idioma podem ser arquivos YAML ou JSON. Você deve inseri-los no diretório `languages` de `theme`. Há suporte para o [printf format](https://github.com/alexei/sprintf.js) nos arquivos de idioma.

### Modelos

Use os helpers `__` ou `_p` nos templates para traduzir as strings. O primeiro é para uso normal e o segundo é para strings no plural. Por exemplo:

``` yaml en.yml
índice:
  title: Casa
  adicionar: Adicionar
  vídeo:
    zero: Sem vídeos
    um: Um vídeo
    outro: vídeos %d
```

``` js
<%= __('index.title') %>
// Home

<%= _p('index.video', 3) %>
// 3 vídeos
```

### Caminhos

Você pode definir o idioma das páginas no front-matter ou modificar a configuração `i18n_dir` no arquivo `_config.yml` para habilitar a detecção automática pelo Hexo.

``` yaml
i18n_dir: :lang
```

O valor padrão da configuração `i18n_dir` é `:lang`, o que significa que o Hexo detectará o idioma dentro do primeiro segmento de URL. Por exemplo:

``` plain
/index.html => en
/archives/index.html => en
/zh-tw/index.html => zh-tw
```

A string só será servida como um idioma quando o arquivo de idioma existir. Então, `archives` em `/archives/index.html` (exemplo 2) não será servida como um idioma.
