---
title: Comandos
---

## iniciar

``` bash
$ hexo init [folder]
```

Inicializa um site. Se nenhuma pasta `` for fornecida, o Hexo vai configurar um site no diretório atual.

Este comando é um atalho que executa as seguintes etapas:

1. O Git clone [hexo-starter](https://github.com/hexojs/hexo-starter) incluindo [hexo-theme-landscape](https://github.com/hexojs/hexo-theme-landscape) no diretório atual ou uma pasta de destino, se especificado.
2. Instale dependências usando um gerenciador de pacotes: [Yarn 1](https://classic.yarnpkg.com/lang/en/), [pnpm](https://pnpm.js.org) ou [npm](https://docs.npmjs.com/cli/install), o que for instalado; se houver mais de um instalado, a prioridade é como listada. npm é empacotado com [Node.js](/docs/#Install-Node-js) por padrão.

## Novo

``` bash
$ hexo novo [layout] <title>
```

Cria um novo artigo. Se nenhum `layout` for fornecido, Hexo usará o `default_layout` de [_config.yml](configuration.html). Use o layout `rascunho` para criar um rascunho. Se o `título` contém espaços, cerque-o com aspas.

| Alternativa       | Descrição:                                                 |
| ----------------- | ---------------------------------------------------------- |
| `-p`, `--path`    | Caminho de postagem. Personalizar o caminho da publicação. |
| `-r`, `--replace` | Substituir a publicação atual se existir.                  |
| `-s`, `--slug`    | Postar slug. Personalizar a URL do post.                   |

Por padrão, o Hexo usará o título para definir o caminho do arquivo. Para páginas, irá criar um diretório com esse nome e um arquivo `index.md` nele. Use a opção `--path` para substituir esse comportamento e definir o caminho do arquivo:

```bash
hexo nova página --path sobre/me "Sobre mim"
```

irá criar o arquivo `source/about/me.md` com o título "Sobre mim" definido no front matter.

Por favor, note que o título é obrigatório. Por exemplo, isso não resultará no comportamento que você pode esperar:

```bash
nova página hexo --path sobre/me
```

irá criar o post `source/_posts/about/me.md` com o título "page" no front. Isso porque há apenas um argumento (`página`) e o layout padrão é `post`.

## gerar

``` bash
Geração de $ hexos
```

Gera arquivos estáticos.

| Alternativa           | Descrição:                                                                 |
| --------------------- | -------------------------------------------------------------------------- |
| `-d`, `--deploy`      | Implementar após a finalização da geração                                  |
| `-w`, `--watch`       | Ver alterações de arquivos                                                 |
| `-b`, `--bail`        | Gera um erro se qualquer exceção não tratada for lançada durante a geração |
| `-f`, `--force`       | Forçar regeneração                                                         |
| `-c`, `--concurrency` | Número máximo de arquivos a serem gerados em paralelo. Padrão é infinito   |

## publicar

``` bash
$ hexo publish [layout] <filename>
```

Publica um rascunho.

## Servidor

``` bash
$ servidor hexo
```

Inicia um servidor local. Por padrão, isso está em `http://localhost:4000/`.

| Alternativa      | Descrição:                                |
| ---------------- | ----------------------------------------- |
| `-p`, `--port`   | Substituir a porta padrão                 |
| `-s`, `--static` | Usar apenas arquivos estáticos            |
| `-l`, `--log`    | Habilitar logger. Override logger format. |

## implantar

``` bash
Campo hexo de $
```

Imprime o seu site.

| Alternativa        | Descrição:                 |
| ------------------ | -------------------------- |
| `-g`, `--generate` | Gerar antes da implantação |

## renderizar

``` bash
$ hexo de renderização <file1> [file2]...
```

Renderiza arquivos.

| Alternativa      | Descrição:       |
| ---------------- | ---------------- |
| `-o`, `--output` | Destino de saída |

## migrar

``` bash
$ hexo migrar <type>
```

[Migrates](migration.html) conteúdo de outros sistemas de blog.

## limpar

``` bash
Limpeza de $ hexos
```

Limpa o arquivo de cache (`db.json`) e os arquivos gerados (`public`).

## lista

``` bash
$ lista hexo <type>
```

Lista de todas as rotas.

## Versão

``` bash
Versão de $ hexo
```

Exibe informações da versão

## Opções

### Modo de segurança

``` bash
$ hexo --safe
```

Desativa o carregamento de plugins e scripts. Tente isto se você encontrar problemas depois de instalar um novo plugin.

### Modo de depuração

``` bash
$ hexo --debug
```

Registra mensagens detalhadas no terminal e para `debug.log`. Tente isso se você encontrar qualquer problema com o Hexo. If you see errors, please [raise a GitHub issue](https://github.com/hexojs/hexo/issues/new).

### Modo silencioso

``` bash
$ hexo --silent
```

Silencia a saída para o terminal.

### Personalizar caminho do arquivo de configuração

``` bash
$ hexo --config custom.yml
```

Usa um arquivo de configuração personalizado (em vez de `_config.yml`). Também aceita uma lista separada por vírgulas (sem espaços) de arquivos de configuração JSON ou YAML que combinarão os arquivos em um único `_multiconfig.yml`.

``` bash
$ hexo --config custom.yml,custom2.json
```

### Exibir rascunhos

``` bash
$ hexo --draft
```

Exibe postagens de rascunho (armazenadas na pasta `source/_drafts`).

### Personalizar CWD

``` bash
$ hexo --cwd /path/to/cwd
```

Personaliza o caminho do diretório de trabalho atual.
