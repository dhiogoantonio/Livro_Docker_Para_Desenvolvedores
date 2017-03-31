# Dockerhub

Você está aprendendo a fazer algo muito legal ao criar a sua própria imagem, que tal compartilhar com as outras pessoas o que você está fazendo? Isso pode ser bem útil para você no futuro e é assim que comunidades fortes são estabelecidas. É pra isso que existe o **Dockerhub**.

#### O que é Dockerhub?

Dockerhub é um Serviço de Web Hosting compartilhado para imagens Docker. No capítulo anterior você leu um pouco sobre imagens oficiais e não-oficiais, é no Dockerhub que os **Dockerfiles** são disponibilizadas para a comunidade. **imagens oficiais** são disponibilizadas por grandes grupos para facilitar o seu trabalho na hora de criar uma infraestrutura Docker. Por exemplo: Ao necessitar de um container com um sistema de gerenciamento de Banco de Dados e montar você uma imagem, o que demandaria certo tempo, você pode usar a [imagem oficial do MySQL](https://hub.docker.com/_/mysql/), que é mantido pelos próprio time interno da empresa.

Diversas outras empresas também possuem imagens oficiais disponveis na plataforma, como:

+ [Nginx](https://hub.docker.com/_/nginx/)
+ [Python](https://hub.docker.com/_/python/)
+ [Node](https://hub.docker.com/_/node/)
+ [WordPress](https://hub.docker.com/_/wordpress/)

Você pode explorar a [lista completa](https://hub.docker.com/explore/) por sua conta.

#### Criando sua conta e um repositório

Agora que você está interessado, vamos criar uma conta na plataforma. Esse processso só pode ser feito através do navegador na [página de inscrição](https://hub.docker.com/register/?utm_source=getting_started_guide&utm_medium=embedded_MacOSX&utm_campaign=create_docker_hub_account) do Dockerhub, ou seja, ainda não é possível criar uma conta pelo terminal.

![Dockerhub](images/Dockerhub.png)

Ao acessar o endereço você deve inserir um novo ID do Docker (nome de usuário), um endereço de e-mail e uma senha. O navegador irá mostrar uma tela de `Welcome to Docker Hub`. Após o cadastro entre no e-mail informado e procure um e-mail entitulado `Please confirm email for your Docker ID`, caso não encontre, não esqueça de checar a sua caixa de spam.

Abra o e-mail e clique em `Confirm Your Email`, o nevagador irá abrir o Dockerhub e redirecionar você para o seu perfil. Nessa página clique em `Create Repository` e preencha um pequeno formulário com o nome do repositório e uma breve descrição, certifique-se de que o repositório esteja como público para que outras pessoas possam visualizar a sua imagem.

A conta gratuita possui direto a um repositório privado. Há [planos](https://hub.docker.com/account/billing-plans/) para que mais repositórios privados fiquem disponveis, geralmente voltado para empresas que usam Docker em sua infraestrutura. 

### Como enviar sua imagem para o Dockerhub

Agora que você já tem a sua conta e criou um repositório vamos enviar a sua imagem para o repositório. Se esse conceito ainda não está claro para você, tente fazer um paralelo com enviar um projeto para o Github utilizando o Git, pois é isso que vamos fazer agora. Ao utilizar o comando `docker images` você verá todas as imagens armazenadas localmente na sua máquina. Vamos imaginar que queremos subir a nossa imagem **docker-is-cool** para o repositório que acabamos de criar pelo navegador.

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker-is-cool      latest              8d9495d05463        38 minutes ago      193.4 MB
ambientum/node      6                   cee61c8e3d01        2 weeks ago         346 MB
nginx               stable-alpine       f94d6dd9b576        3 weeks ago         54 MB
```

Ao utilizar o comando `docker images` seu resultado será similar ao acima.

#### Taggeando a sua imagem



#### Como dar Pull e Push na sua imagem
