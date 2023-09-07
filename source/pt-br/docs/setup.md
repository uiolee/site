---
title: Configuração
---

{% youtube 0m2HnATkHOk %}

Uma vez que o Hexo estiver instalado, execute os seguintes comandos para inicializar o Hexo no alvo `<folder>`.

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

Uma vez inicializado, aqui está a aparência da pasta do seu projeto:

``` plain
.
── _config.yml
── package.json
─── scaffolds
── fonte
├── _drafts
─── _drafts 
 ── _posts
── temas
```

### _config.yml

Arquivo [configuração](configuration.html) do site. Você pode definir a maioria das configurações aqui.

### package.json

Dados do aplicativo. Os renderizadores [EJS](https://ejs.co/), [Stylus](http://learnboost.github.io/stylus/) e [Markdown](http://daringfireball.net/projects/markdown/) estão instalados por padrão. Se você quiser, você pode desinstalá-los mais tarde.

``` json package.json
{
  "name": "hexo-site",
  "version": "0.0. ",
  "private": true,
  "hexo": {
    "version": ""
  },
  "dependências": {
    "hexo": "^3. .0",
    "hexo-generator-archive": "^0.1.5",
    "hexo-gerador-categoria": "^0. .3",
    "hexo-gerator-index": "^0.2.1",
    "hexo-gerador-tag": "^0.2.0",
    "hexo-renderer-ejs": "^0.3. ",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-renderer-marked": "^0. .2",
    "servidor hexo": "^0.3.3"
  }
}
```

### andaimes

[Pasta Scaffold](writing.html#Scaffolds). Quando você cria um novo post, o Hexo base o novo arquivo no andaime.

### Fonte

Pasta de origem. É aqui que você coloca o conteúdo do seu site. Hexo ignora arquivos e pastas ocultos ou cujos nomes são prefixados com `_` (underscore) - exceto a pasta `_posts`. Arquivos renderizáveis (por exemplo, Markdown, HTML) serão processados e colocados na pasta `pública` , enquanto outros arquivos serão simplesmente copiados.

### temas

Pasta [Tema](themes.html). O Hexo gera um site estático combinando o conteúdo do site com o tema.
