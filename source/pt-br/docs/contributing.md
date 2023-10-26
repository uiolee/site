---
title: Contribuindo
---

Seja bem-vinda a sua participação no desenvolvimento de Hexo. 🤗

## Desenvolvimento

Nós damos o parabéns a você por se juntar ao desenvolvimento do Hexo. Este documento irá ajudá-lo através do processo.

### Antes de Você Começar

Por favor leia [Código de Conduta do Contribuidor](https://github.com/hexojs/hexo/blob/master/CODE_OF_CONDUCT.md) primeiro.

Por favor, siga o estilo de codificação:

- Siga o [Guia de Estilo de Código JavaScript do Google](https://google.github.io/styleguide/jsguide.html).
- Use soft-tabs com um recuo de dois espaços.
- Não coloque vírgulas primeiro.

Além disso, Hexo tem sua própria configuração [ESLint](https://github.com/hexojs/eslint-config-hexo), então por favor, certifique-se de que sua contribuição fará ESLint feliz.

### Fluxo de Trabalho

1. Faça um fork [hexojs/hexo][].
2. Clone o repositório no seu computador e instale as dependências.

``` bash
$ git clone https://github.com/<username>/hexo.git
$ cd hexo
$ npm install
$ git submodule update --init
```

3. Crie um branch para a feature a ser desenvolvida.

``` bash
$ git check-b new_feature
```

4. Comece a hacking.
5. Empurre o branch:

```
$ git push origin new_feature
```

6. Crie um pull request e descreva as mudanças.

### Observação

- Não modifique o número da versão no arquivo `package.json`.
- Seu pedido de pull request só será aceito quando os testes tiverem passado. Não se esqueça de executar testes antes da submissão.

``` bash
$ teste npm
```

## Atualizando oficial-plugins

Also, we welcome PR or issue to [official-plugins](https://github.com/hexojs). 🤗

## Atualizando a Documentação

A documentação do Hexo é de código aberto e você pode encontrar o código-fonte em [hexojs/site][].

### Fluxo de trabalho

1. Faça um fork [hexojs/site][]
2. Clone o repositório no seu computador e instale as dependências.

``` bash
$ npm install hexo-cli -g # Se você não tem hexo-cli instalado
$ git clone https://github. om/<username>/site.git
$ cd site
$ npm install
```

3. Comece a editar a documentação. Você pode iniciar o servidor para a visualização das mudanças em tempo real.

``` bash
$ servidor hexo
```

4. Empurre o branch.
5. Crie um pull request e descreva as mudanças.

### Traduzindo

1. Adicione um diretório para o novo idioma dentro do repositório `source`. (Todas as letras minúsculas)
2. Copie os arquivos de template e Markdown que estão no `source` para o diretório do novo idioma.
3. Adicione o novo idioma a `source/_data/language.yml`.
4. Copie o arquivo `en.yml` em `themes/navy/languages` e o renomeie para o nome do novo idioma (todas as minúsculas).

## Reportando Issues

Quando você encontra alguns problemas ao usar o Hexo, você pode encontrar as soluções em [Solução de problemas](troubleshooting.html) ou nos perguntar no [GitHub](https://github.com/hexojs/hexo/issues) ou [Google Group](https://groups.google.com/group/hexo). Se você não conseguir encontrar a resposta, abra uma nova issue no GitHub.

1. Reproduza o problema em [modo de depuração](commands.html#Debug_mode).
2. Siga as etapas do modelo de problema para fornecer a mensagem e versão de depuração ao enviar um novo problema no GitHub.

[hexojs/hexo]: https://github.com/hexojs/hexo
[hexojs/site]: https://github.com/hexojs/site
