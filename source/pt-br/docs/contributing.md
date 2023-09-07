---
title: Contribuições
---

Seja bem-vinda a sua participação no desenvolvimento de Hexo. 🤗

## Desenvolvimento

Seja bem-vinda a sua participação no desenvolvimento de Hexo. Este documento irá ajudá-lo durante o processo.

### Antes de começar

Por favor leia [Código de Conduta do Contribuidor](https://github.com/hexojs/hexo/blob/master/CODE_OF_CONDUCT.md) primeiro.

Siga o estilo de codificação:

- Siga [Guia de estilo do Google JavaScript](https://google.github.io/styleguide/jsguide.html).
- Use soft-tabs com dois espaços dentro.
- Não coloque vírgulas primeiro.

Além disso, Hexo tem sua própria configuração [ESLint](https://github.com/hexojs/eslint-config-hexo), então por favor, certifique-se de que sua contribuição fará ESLint feliz.

### Workflow

1. Fork [hexojs/hexo][].
2. Clone o repositório para o seu computador e instale dependências.

``` bash
$ git clone https://github.com/<username>/hexo.git
$ cd hexo
$ npm install
$ git submodule update --init
```

3. Criar um ramo de recurso.

``` bash
$ git check-b new_feature
```

4. Comece a hacking.
5. Empurre o branch:

```
$ git push origin new_feature
```

6. Crie um pull request e descreva a mudança.

### Observação

- Por favor, não modifique o número da versão em `package.json`.
- Seu pull request só será mesclado quando os testes forem concluídos. Não esqueça de executar testes antes do envio.

``` bash
$ teste npm
```

## Atualizando oficial-plugins

Also, we welcome PR or issue to [official-plugins](https://github.com/hexojs). 🤗

## Atualizando Documentação

A documentação do Hexo é de código aberto e você pode encontrar o código-fonte em [hexojs/site][].

### Workflow

1. Fork [hexojs/site][]
2. Clone o repositório para o seu computador e instale dependências.

``` bash
$ npm install hexo-cli -g # Se você não tem hexo-cli instalado
$ git clone https://github. om/<username>/site.git
$ cd site
$ npm install
```

3. Comece a editar a documentação. Você pode iniciar o servidor para pré-visualização ao vivo.

``` bash
$ servidor hexo
```

4. Empurre o branch.
5. Crie um pull request e descreva a mudança.

### Traduzindo

1. Adicione uma nova pasta de idioma na pasta `fonte`. (Todos os casos mais baixos)
2. Copie arquivos de Markdown e modelo na pasta `fonte` para a nova pasta de idioma.
3. Adicione o novo idioma à `source/_data/language.yml`.
4. Copie o `en.yml` em `temas/navy/languages` e renomeie para o nome do idioma (todos casos menores).

## Reportando problemas

Quando você encontrar alguns problemas ao usar o Hexo, você pode encontrar as soluções no [Solução de problemas](troubleshooting.html) ou me perguntar no [GitHub](https://github.com/hexojs/hexo/issues) ou [Google Group](https://groups.google.com/group/hexo). Se você não encontrar a resposta, por favor, reporte no GitHub.

1. Representa o problema no modo [de depuração](commands.html#Debug_mode).
2. Siga as etapas do modelo de problema para fornecer a mensagem e versão de depuração ao enviar um novo problema no GitHub.

[hexojs/hexo]: https://github.com/hexojs/hexo
[hexojs/site]: https://github.com/hexojs/site
