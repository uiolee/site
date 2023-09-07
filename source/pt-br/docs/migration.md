---
title: Migração
---

## Resposta

Primeiro, instale o plugin `hexo-migrator-rss`.

``` bash
$ npm install hexo-migrator-rss --save
```

Uma vez que o plugin estiver instalado, execute o seguinte comando para migrar todos os posts do RSS. `fonte` pode ser um caminho ou uma URL.

``` bash
$ hexo migrar rss <source>
```

## Jekyll

Mover todos os arquivos na pasta do Jekyll `_posts` para a pasta `fonte/_posts`.

Modificar a configuração `new_post_name` em `_config.yml`:

``` yaml
novo_nome_post: :year-:day-:title.md
```

## Polvo

Mova todos os arquivos no Octopress `source/_posts` pasta para `source/_posts`

Modificar a configuração `new_post_name` em `_config.yml`:

``` yaml
novo_nome_post: :year-:day-:title.md
```

## WordPress

Primeiro, instale o plugin `hexo-migrator-wordpress`.

``` bash
$ npm install hexo-migrator-wordpress --save
```

Exporte o seu site WordPress indo para "Ferramentas" → "Exportar" → "WordPress" no painel WordPress (veja a página de suporte [WordPress](http://en.support.wordpress.com/export/) para mais detalhes).

Agora executar:

``` bash
$ hexo migrar wordpress <source>
```

Onde `fonte` é o caminho do arquivo ou URL para o arquivo de exportação WordPress.

## Joomla

Primeiro, instale o plugin `hexo-migrator-joomla`.

```bash
$ npm install hexo-migror-joomla --save
```

Exporte os seus artigos do Joomla usando o componente [J2XML](http://extensions.joomla.org/extensions/migration-a-conversion/data-import-a-export/12816?qh=YToxOntpOjA7czo1OiJqMnhtbCI7fQ%3D%3D).

Agora executar:

```bash
$ hexo migrate joomla <source>
```

Onde `fonte` é o caminho do arquivo ou URL para o arquivo de exportação do Joomla.
