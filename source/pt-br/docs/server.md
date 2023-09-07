---
title: Servidor
---

## [servidor hexo-servidor][]

Com o lançamento do Hexo 3, o servidor foi separado do módulo principal. Para começar a usar o servidor, você primeiro terá que instalar [hexo-server][].

``` bash
$ npm install hexo-server --save
```

Uma vez que o servidor for instalado, execute o seguinte comando para iniciar o servidor. Seu site será executado em `http://localhost:4000` por padrão. Quando o servidor estiver em execução, o Hexo irá observar as alterações de arquivo e atualizará automaticamente para que não seja necessário reiniciar o servidor manualmente.

``` bash
$ servidor hexo
```

Se você quer mudar a porta ou se estiver encontrando erros `EADDRINUSE` , use a opção `-p` para definir uma porta diferente.

``` bash
$ servidor hexo -p 5000
```

### Modo Estático

No modo estático, apenas arquivos na pasta `pública` serão servidos e o relógio de arquivos está desativado. Você precisa executar `hexo generate` antes de iniciar o servidor. Geralmente utilizado na produção.

``` bash
$ servidor hexo -s
```

### IP personalizado

Hexo executa o servidor em `0.0.0.0` por padrão. Você pode substituir a configuração de IP padrão.

``` bash
$ servidor hexo -i 192.168.1.1
```

[servidor hexo-servidor]: https://github.com/hexojs/hexo-server

[hexo-server]: https://github.com/hexojs/hexo-server
