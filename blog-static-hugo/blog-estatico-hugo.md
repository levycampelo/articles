---
title: "Blog estático com Hugo"
weight: 1
date: 2024-07-23T08:48:36-03:00
authors:
  - levy
tags:
  - Blog Hugo
draft: true
---
HUGO é um gerador de sites estáticos escrito em Golang que tem ganhado muita visibilidade devido à sua rapidez na geração e compilação de conteúdos. Juntamente com o Jekyll, escrito em Ruby, ambos os geradores oferecem uma ampla gama de recursos, permitindo que você crie um site ou blog em minutos.

### Como instalar Hugo no Linux
O Hugo é distribuído como um executável compilado, o que significa que você não precisa baixar e gerenciar várias dependências para começar a usá-lo. Ele está disponível para macOS, Windows e Linux.
```
# apt install hugo
```

### Instalar o pacote webpack:
```
# apt install nodejs
```

### Instalar o curl:
```
# apt install curl
```

### Criar seu primeiro blog:
```
hugo new site <name of site>
cd <name of site>
```

### Instalado o tema HugoBlog:
```
cd themes
curl -L https://github.com/thegeeklab/hugo-geekblog/releases/latest/download/hugo-geekblog.tar.gz | 
tar -xz -C themes/hugo-geekblog/ --strip-components=1
```

### Configure o arquivo config.toml
```
baseURL = "http://localhost"
title = "Geekblog"
theme = "hugo-geekblog"

pluralizeListTitles = false

# Geekblog required configuration
pygmentsUseClasses = true
pygmentsCodeFences = true
disablePathToLower = true

# Needed for mermaid shortcodes
[markup]
  [markup.goldmark.renderer]
    unsafe = true
  [markup.tableOfContents]
    startLevel = 1
    endLevel = 9

[taxonomies]
  author = "authors"
  tag = "tags"

[mediaTypes]
  [mediaTypes."application/atom+xml"]
    suffixes = ["xml"]

[outputFormats]
  [outputFormats.Atom]
    name = "Atom"
    mediaType = "application/atom+xml"
    baseName = "feed"
    isPlainText = false
    rel = "alternate"
    isHTML = false
    noUgly = true
    permalinkable = false

[outputs]
  home = ["HTML", "ATOM"]
  page = ["HTML"]
  section = ["HTML"]
  taxonomy = ["HTML"]
  term = ["HTML", "ATOM"]
```

### Iniciar o serviço: 
```hugo server -D```

### Este comando executara seu projeto no localhost utilizando a porta 1313:
```http://localhost:1313``` 
