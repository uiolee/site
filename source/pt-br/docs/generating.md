---
title: Gerando
---

Gerar arquivos estáticos com o Hexo é muito fácil e rápido.

``` bash
Geração de $ hexos
```

{% youtube viEJQPVCoLU %}

### Procurar por alterações nos arquivos

Hexo pode acompanhar alterações de arquivos e regenerar arquivos imediatamente. Hexo irá comparar a soma de verificação SHA1 de seus arquivos e só escreverá se alterações de arquivo forem detectadas.

``` bash
$ hexo generate --watch
```

### Implantar após a geração

Para implantar após a geração, você pode executar um dos seguintes comandos. Não há diferença entre os dois.

``` bash
$ hexo generate --deploy
$ hexo deploy --generate
```
