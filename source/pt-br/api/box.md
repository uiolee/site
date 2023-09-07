---
title: Cx
---

O Box é um container usado para processar arquivos em uma pasta específica. Hexo usa duas caixas diferentes: `hexo.source` e `hexo.theme`. O primeiro é usado para processar a pasta `source` e o segundo para processar a pasta `tema`.

## Carregar Arquivos

Box fornece dois métodos para carregar arquivos: `processo` e `watch`. `process` loads all files in the folder. `watch` faz o mesmo, mas também começa a observar para ver as alterações de arquivos.

``` js
box.process().then(function(){
  // ...
});

box.watch().then(function(){
  // Você pode chamar box.unwatch() mais tarde para parar de assistir.
});
```

## Correspondência de caminho

Caixa fornece muitas maneiras de combinar caminho. Você pode usar uma expressão regular, uma função ou uma string padrão ao estilo Express. Por exemplo:

``` plain
posts/:id => posts/89
posts/*caminho => posts/2015/title
```

Veja [util.Pattern][] para mais informações.

## Processadores

Um processador é um elemento essencial do Box e é usado para processar arquivos. Você pode usar a correspondência de caminhos conforme descrito acima para restringir o que exatamente o processador deve processar. Registre um novo processador com o método `addProcessor`.

``` js
box.addProcessor('posts/:id', function(file){
  //
});
```

O Box passa o conteúdo dos arquivos correspondentes para os processadores. Essa informação pode então ser lida diretamente do argumento do arquivo `` no callback:

| Atributo  | Descrição:                                                                |
| --------- | ------------------------------------------------------------------------- |
| `Fonte`   | Caminho completo do arquivo                                               |
| `caminho` | Caminho relativo para a caixa do arquivo                                  |
| `Tipo`    | Tipo de arquivo. O valor pode ser `create`, `update`, `pular`, `deletar`. |
| `params`  | As informações da correspondência do caminho.                             |

O Box também fornece alguns métodos para que você não tenha que fazer o arquivo IO sozinho.

| Método           | Descrição:                                    |
| ---------------- | --------------------------------------------- |
| `lidos`          | Ler um arquivo                                |
| `readSync`       | Leia um arquivo sincronizadamente             |
| `estatística`    | Ler o estado de um arquivo                    |
| `sincronizaçãod` | Leia o status de um arquivo de forma síncrona |
| `renderizar`     | Renderizar um arquivo                         |
| `renderSync`     | Renderizar um arquivo sincronizadamente       |

[util.Pattern]: https://github.com/hexojs/hexo-util#patternrule
