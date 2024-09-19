---
title: "Usando o Git"
date: 2024-07-26T18:21:13-03:00
draft: true
authors:
  - levy
tags:
  - GIT
---

Para subir o seu projeto que está localizado no seu computador (por exemplo no diretório /home/seu_usuario) para o GitHub, você pode seguir os passos básicos abaixo:

### Passo 1: Criar um repositório no GitHub
1.	Faça login na sua conta do GitHub.
2.	No canto superior direito, clique no sinal de + e selecione Novo repositório.
3.	Escolha um nome para o seu repositório, defina se será público ou privado, e clique em Criar repositório.

### Passo 2: Preparar seu repositório local
1.	Abra um terminal no seu computador.
2.	Navegue até o diretório onde seu projeto está localizado usando o comando cd (por exemplo, cd /home/levy/rota).
3.	Verifique se o Git já está inicializado no seu projeto usando git status. Se o Git não estiver inicializado, use git init para iniciar o controle de versão Git no diretório.

### Passo 3: Adicionar e confirmar os arquivos
1.	Para adicionar todos os arquivos ao controle de versão do Git, use o comando:
```
git add .
```
Isso adicionará todos os arquivos no diretório atual para serem monitorados pelo Git.
2.	Em seguida, confirme as mudanças usando o comando git commit:
```
git commit -m "Descreve as alterações"
```
### Passo 4: Conectar seu repositório local ao GitHub

1.	No GitHub, copie o URL do seu repositório (você pode encontrá-lo na página do seu repositório, geralmente começa com https://github.com/seu-usuario/nome-do-repositorio.git).
2.	De volta ao terminal, adicione o URL remoto ao seu repositório Git local usando o comando:
```
git remote add origin https://github.com/seu-usuario/nome-do-repositorio.git
```
3.	Finalmente, envie seu código para o GitHub usando o comando git push:
```
git push -u origin master
```

Isso empurra suas alterações locais para o branch principal (master) do seu repositório remoto no GitHub.
Depois de completar esses passos, seu projeto estará disponível no GitHub. Você pode continuar a trabalhar no seu projeto localmente, e sempre que quiser enviar novas alterações para o GitHub, basta usar git add, git commit e git push novamente.


