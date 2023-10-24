---
title: Eventos
---

O Hexo herda de [EventEmitter][]. Use o método `on` para ouvir os eventos emitidos pelo Hexo, e use o método `emit` para emitir eventos. Para obter mais informações, consulte a documentação da API do Node.js.

### implantaçãoAntes

Emitido antes do deployment começar.

### implantaçãoApós

Emitido depois do deployment finalizado.

### saindo

Emitido antes de Hexo sair.

### gerarAntes

Emitido antes da geração começar.

### gerarDepois

Emitido depois da geração finalizada.

### Novo

Emitido depois de uma nova postagem ter sido criada. Este evento retorna os dados da postagem:

``` js
hexo.on('new', function(post){
  //
});
```

| Dados                 | Descrição                               |
| --------------------- | --------------------------------------- |
| `caminho.post`        | Caminho completo do arquivo da postagem |
| `publicação.conteúdo` | Conteúdo do arquivo da postagem         |

### processarAntes

Emitido antes do início do processamento. Este evento retorna um caminho que representa o diretório raiz do box.

### processAfter

Emitido depois do processamento finalizado. Este evento retorna um caminho que representa o diretório raiz do `box`.

### Pronto

Emitido depois da inicialização terminar.

[EventEmitter]: https://nodejs.org/dist/latest/docs/api/events.html
