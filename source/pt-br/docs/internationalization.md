---
title: Internacionalização (i18n)
---

Você pode usar a internacionalização para apresentar seu site em diferentes idiomas. O idioma padrão é definido modificando a configuração `idioma` em `_config.yml`. Você também pode definir vários idiomas e modificar a ordem dos idiomas padrão.

``` yaml
idioma: zh-tw

idioma:
- zh-tw
- pt
```

### Arquivos de Idioma

Arquivos de linguagem podem ser arquivos YAML ou JSON. Você deve colocá-los na pasta `idiomas` no tema. Existe suporte para o formato [printf](https://github.com/alexei/sprintf.js) em arquivos de idioma.

### Modelos

Use `__` ou `_p` auxiliares em templates para obter as frases traduzidas. O primeiro diz respeito à utilização normal e o segundo à pluralidade das frases. Por exemplo:

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

### Caminho

Você pode definir o idioma das páginas no front-matter, ou modificar a configuração `i18n_dir` em `_config. ml` para habilitar a detecção automática por Hexo.

``` yaml
i18n_dir: :lang
```

O valor padrão da configuração `i18n_dir` é `:lang`, o que significa que o Hexo irá detectar o idioma dentro do primeiro segmento de URL. Por exemplo:

``` plain
/index.html => en
/archives/index.html => en
/zh-tw/index.html => zh-tw
```

O texto só será servido como um idioma quando o arquivo de idioma existir. Então os arquivos `` em `/archives/index.html` (exemplo 2) não serão servidos como uma linguagem.
