---
title: Servidor
---

## [servidor hexo-servidor][]

Com o lançamento do Hexo 3, o servidor foi separado do módulo principal. Para começar a usar o servidor, primeiro você deve instalar o pacote [hexo-server][].

``` bash
$ npm install hexo-server --save
```

Uma vez instalado o servidor, execute o comando a seguir para iniciar o servidor. Seu site será acessível em `http://localhost:4000` por padrão. Quando o servidor estiver sendo executado, o Hexo assistirá por alterações nos arquivos do projeto e atualizará automaticamente a página, por isso não é necessário reiniciar manualmente o servidor.

``` bash
$ servidor hexo
```

Se você quiser mudar a porta ou se estiver encontrando erros `EADDRINUSE`, use a opção `-p` para configurar uma porta diferente.

``` bash
$ servidor hexo -p 5000
```

### Modo Estático

No modo estático, somente arquivos do diretório `public` serão servidos e nenhum arquivo será assistido por mudanças. Você deve executar `hexo generate` antes de iniciar o servidor. Em geral, é desta forma que o site é servido em produção.

``` bash
$ servidor hexo -s
```

### Ip Customizado

O Hexo executa o servidor em `0.0.0.0` por padrão. Você pode substituir a configuração de IP padrão.

``` bash
$ servidor hexo -i 192.168.1.1
```

[servidor hexo-servidor]: https://github.com/hexojs/hexo-server

[hexo-server]: https://github.com/hexojs/hexo-server
