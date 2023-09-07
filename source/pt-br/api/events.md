---
title: Eventos
---

Hexo herda de [EventEmitter][]. Use o método `no` para ouvir eventos emitidos pelo Hexo e use o método `emite` para emitir eventos. Para obter mais informações, consulte a documentação da API do Node.js.

### implantaçãoAntes

Emitido antes que a implantação comece.

### implantaçãoApós

Emitido após conclusão da implantação.

### saindo

Emitido antes da saída Hexo.

### gerarAntes

Emitido antes do início da geração.

### gerarDepois

Emitido após término da geração.

### Novo

Emitido após uma nova postagem ter sido criada. Este evento retorna os dados da postagem:

``` js
hexo.on('new', function(post){
  //
});
```

| Dado                  | Descrição:                       |
| --------------------- | -------------------------------- |
| `caminho.post`        | Caminho completo do arquivo post |
| `publicação.conteúdo` | Conteúdo do arquivo post         |

### processarAntes

Emitido antes que o processamento comece. Este evento retorna um caminho que representa o diretório raiz da caixa.

### processAfter

Emitido após término do processamento. Este evento retorna um caminho que representa o diretório raiz da caixa.

### Pronto

Emitido após a conclusão da inicialização.

[EventEmitter]: https://nodejs.org/dist/latest/docs/api/events.html
