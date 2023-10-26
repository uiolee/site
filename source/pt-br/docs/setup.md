---
title: Configuração
---

{% youtube 0m2HnATkHOk %}

Uma vez instalado o Hexo, execute os seguintes comandos para inicializar um site com Hexo em um diretório `<folder>`.

``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

Após inicializado, o diretório do seu projeto ficará com a seguinte estrutura:

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

Arquivo de [configuração](configuration.html) do site. Você pode definir a maioria das configurações aqui.

### package.json

Arquivo de dados da aplicação. Os renderizadores [Markdown](http://daringfireball.net/projects/markdown/), [EJS](https://ejs.co/) e [Stylus](http://learnboost.github.io/stylus/) são instalados por padrão. Se desejar, você pode desinstalá-los posteriormente.

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

Diretório de [Scaffold](writing.html#Scaffolds). Quando você cria uma nova postagem, o Hexo cria um arquivo baseado no scaffold.

### Fonte

Diretório de conteúdo. É aqui que você coloca o conteúdo do seu site. O Hexo ignora arquivos ocultos e arquivos ou diretórios cujos nomes são prefixados com `_` (sublinhado) - exceto o diretório `_posts`. Os arquivos renderizáveis (arquivos Markdown e HTML por exemplo) serão processados e colocados no diretório `public`, enquanto outros arquivos serão simplesmente copiados.

### temas

Diretório de [Temas](themes.html). O Hexo gera um site estático combinando o conteúdo do site com o tema.
