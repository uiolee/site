---
title: Temas
---

{% youtube 5ROIU_9dYe4 %}

É fácil construir um tema Hexo - você só tem que criar uma nova pasta. Para começar a usar o seu tema, modifique a configuração `tema` no `_config.yml` do seu site. Um tema deve ter a seguinte estrutura:

```plain
.
── _config.yml
── linguagens
── layout
── scripts
── fonte
```

### \_config.yml

Arquivo de configuração do tema. Ao contrário do arquivo de configuração principal do site, modificar isto não requer uma reinicialização do servidor.

### Idiomas

Pasta do idioma. Consulte [internacionalização (i18n)](internationalization.html) para mais informações.

### layout

Pasta de layout. Esta pasta contém arquivos de template do tema, que definem a aparência do site. Hexo fornece o mecanismo de template [Nunjucks][] por padrão mas você pode facilmente instalar plugins adicionais para suportar motores alternativos como [EJS][], [Haml][], [Jade][], ou [Pug][]. Hexo escolhe o motor de modelos com base na extensão do arquivo do template (como os posts). Por exemplo:

```plain
layout.ejs - usa o layout EJS
layout.njk - usa Nunjucks
```

Veja [templates](templates.html) para mais informações.

### scripts

Pasta de script. Hexo carregará automaticamente todos os arquivos JavaScript nesta pasta durante a inicialização. Para obter mais informações, consulte [plugins](plugins.html).

### Fonte

Pasta de origem. Coloque seus ativos (por exemplo, arquivos CSS e JavaScript) aqui. Hexo ignora arquivos e pastas ocultos precedidos por `_` (sublinhado).

Hexo processará e salvará todos os arquivos de renderização na pasta `pública`. Arquivos não renderizáveis serão copiados para a pasta `pública` diretamente.

### Publicando

Quando terminar de construir o seu tema, você pode publicá-lo na lista [do tema](/themes). Antes de fazer isso, você deve executar o [teste de unidade de tema](https://github.com/hexojs/hexo-theme-unit-test) para garantir que tudo funcione. The steps for publishing a theme are very similar to those for [updating documentation](contributing.html#Updating_Documentation).

1. Fork [hexojs/site][]
2. Clone o repositório para o seu computador e instale dependências.

   ```shell
   $ git clone https://github.com/<username>/site.git
   $ cd site
   $ npm install
   ```

3. Crie um novo arquivo yaml em `source/_data/themes/`, use o nome do seu tema como o nome do arquivo

4. Edite `source/_data/themes/<your-theme-name>.yml` e adicione o seu tema. Por exemplo:

   ```yaml
   descrição: Um novo tema padrão para o Hexo.
   link: https://github.com/hexojs/hexo-theme-landscape
   preview: http://hexo.io/hexo-theme-landscape
   tags:
     - oficial
     - responsive
     - widget
     - two_column
     - one_column
   ```

5. Adicione uma captura de tela (com o mesmo nome do tema) a `fonte/temas/capturas de tela`. Deve ser um PNG de 800\*500px.
6. Empurre o branch.
7. Crie um pull request e descreva a mudança.

[EJS]: https://github.com/hexojs/hexo-renderer-ejs
[Haml]: https://github.com/hexojs/hexo-renderer-haml
[Jade]: https://github.com/hexojs/hexo-renderer-jade
[Pug]: https://github.com/maxknee/hexo-render-pug
[hexojs/site]: https://github.com/hexojs/site
[Nunjucks]: https://mozilla.github.io/nunjucks/
