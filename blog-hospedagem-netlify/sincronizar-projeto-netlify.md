## Deploy automatizado com Netlify e GitHub

Neste artigo, vou demonstrar como sincronizar o seu site, onde o código esteja no GitHub com o Netlify.<br>

### Introdução
O Netlify é um serviço de hospedagem para sistemas baseados em tecnologias front-end, que não necessitam de banco de dados ou linguagens back-end para funcionar. O Netlify é gratuito, basta se cadastrar e começar a usar.

O GitHub é uma plataforma gratuita de controle de versões que permite gerenciar projetos e colaborar com uma vasta comunidade de desenvolvedores.

### 1ª Adicionar o seu repositorio GIT no Netlify
A primeira etapa é sincronizar o Git com o Netlify. Na tela principal da sua conta do Netlify, clique no botão "New site from Git". Nesta etapa, autentique-se com sua conta do Git e selecione o repositório ao qual o Netlify terá acesso. Além disso, defina o comando que o Netlify deve executar para fazer o build do projeto. Como estamos usando o Hugo, o comando deve ser hugo -d.

![netlify](/blog-hospedagem-netlify/images/build-netlify.png)

### 2ª Ajustar domain
A conta do Netlify inclui um domínio padrão (xxx.netlify.app). Caso precise de um domínio próprio, você pode adquiri-lo diretamente na plataforma ou configurar um CNAME através de serviços como o Registro.br.

![dns](/blog-hospedagem-netlify/images/dns.png)

### Finalizando
Com esses ajustes, toda vez que houver um deploy na branch, o Netlify fará o build e publicará automaticamente. Este serviço é excelente para divulgar seu trabalho sem a necessidade de pagar por hospedagem.
