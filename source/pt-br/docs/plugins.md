---
title: Complementos
---

Hexo tem um poderoso sistema de plugins, que torna fácil estender funções sem modificar o código-fonte do módulo do núcleo. Existem dois tipos de plugins no Hexo:

### Roteiro

Se o seu plugin é relativamente simples, é recomendado usar um script. Tudo o que você precisa fazer é colocar seus arquivos JavaScript na pasta `scripts` e Hexo irá carregá-los durante a inicialização.

### Plugin

Se o seu código é complicado ou se quiser publicá-lo no registro NPM, recomendamos o uso de um plugin. Primeiro, crie uma pasta na pasta `node_modules`. O nome desta pasta deve começar com `hexo-` ou Hexo irá ignorá-la.

Sua nova pasta deve conter pelo menos dois arquivos: um contendo o código JavaScript real e um pacote `. arquivo son` que descreve o propósito do plugin e define suas dependências.

```plain
.
── index.js
── package.json
```

No mínimo, você deve definir o nome ``, `versão` e `main` entries no arquivo `package.json`. Por exemplo:

```json package.json
{
  "name": "hexo-meu-plugin",
  "version": "0.0.1",
  "main": "index"
}
```

Você também precisará listar o seu plugin como uma dependência no pacote `raiz. son` da sua instância de hexo em ordem para que Hexo detecte e carregue-o.

### Ferramentas

Você pode fazer uso das ferramentas oficiais fornecidas pelo Hexo para acelerar o desenvolvimento:

- [hexo-fs][]：Arquivo IO
- [util][]：Utilidades
- [hexo-i18n][]：Localização (i18n)
- [hexo-paginação][]：Gerar dados de paginação

### Publicando

Quando seu plugin estiver pronto, você pode considerar publicá-lo na lista [do plugin](/plugins) para convidar outras pessoas para começar a usá-lo. Publishing your own plugins is very similar to [updating documentation](contributing.html#Updating_Documentation).

1. Fork [hexojs/site][]
2. Clone o repositório para o seu computador e instale dependências.

   ```shell
   $ git clone https://github.com/<username>/site.git
   $ cd site
   $ npm install
   ```

3. Crie um novo arquivo yaml em `source/_data/plugins/`, use o nome do seu plugin como o nome do arquivo

4. Edite `source/_data/plugins/<your-plugin-name>.yml` e adicione o seu plugin. Por exemplo:

   ```yaml
   descrição: Módulo do servidor para o Hexo.
   link: https://github.com/hexojs/hexo-server
   tags:
     - oficial
     - servidor
     - console
   ```

5. Empurre o branch.
6. Crie um pull request e descreva a mudança.

[hexo-fs]: https://github.com/hexojs/hexo-fs
[util]: https://github.com/hexojs/hexo-util
[hexo-i18n]: https://github.com/hexojs/hexo-i18n
[hexo-paginação]: https://github.com/hexojs/hexo-pagination
[hexojs/site]: https://github.com/hexojs/site
