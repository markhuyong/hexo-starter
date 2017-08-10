---
title: hexo cheatsheet 
categories:
  - Hexo
tags:
  - hexo
  - cheatsheet
---
Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

## Cheatsheet

### Installation

```bash
npm install hexo -g #install
npm update hexo -g #update
hexo init #initialize
```

### Shorthands

```bash
 hexo n #hexo new
 hexo p #hexo publish
 hexo g #hexo generate
 hexo s #hexo server
 hexo d #hexo deploy

 hexo s -g #hexo server with generator
 hexo s -g --draft #hexo server with generator and show drafts

```

### Server

```bash
hexo server #Hexo will watch files, don't need to restart server 
hexo server -s #Static mode, serve public folder and disable file watching.
hexo server -p 5000 #change port
hexo server -i 192.168.1.1 #custom ip
hexo clean #Cleans the cache file (db.json) and generated files (public).
hexo g #Generates static files.
hexo d #Deploys your website.
```

### Watching

```bash
hexo generate
hexo generate --watch #Watch file changes
```

### Deploy

```bash
hexo generate --deploy
hexo deploy --generate

hexo deploy -g
hexo server -g
```

### Posts

```bash
hexo new "postName" # new post _posts/postName.md
hexo new page "pageName" 
hexo generate 
hexo server 
hexo deploy #.deploy deploy to GitHub repo
hexo new [layout] <title>
hexo new photo "My Gallery"
hexo new "Hello World" --lang tw

hexo new draft "New Draft" # New-Draft.md
hexo publish "New Draft" # copy New-Draft.md from _drafts to _posts
```
## Quick Start

Command line reference: [Commands | Hexo](https://hexo.io/docs/commands.html)

Installation with github: [How to use Hexo and deploy to GitHub Pages](https://gist.github.com/btfak/18938572f5df000ebe06fbd1872e4e39)

Next theme: [Hexo搭建GitHub博客（三）- NexT主题配置使用 | Zhiho's Blog](http://zhiho.github.io/2015/09/29/hexo-next/)



### Create a new post

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### Run server

``` bash
$ hexo server
```

More info: [Server](https://hexo.io/docs/server.html)

### Generate static files

``` bash
$ hexo generate
```

More info: [Generating](https://hexo.io/docs/generating.html)

### Deploy to remote sites

``` bash
$ hexo deploy
```

More info: [Deployment](https://hexo.io/docs/deployment.html)
