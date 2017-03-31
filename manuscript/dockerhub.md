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

Antes de enviarmos nossa imagem para a nuvem precisamos taggea-la com o comando `docker tag`. Como vimos acima na coluna **REPOSITORY** a imagem **docker-is-cool** não mostra quem a criou em seu nome. Você precisa do comando [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) para associar a imagem a sua conta Dockerhub incluindo um `namespace` antes do nome da imagem. O comando será semelhante ao abaixo.

![Dockertag](images/Dockerhub-tag.png)

Funciona da seguinte maneira: Usamos o comando `docker tag` e passamos como parâmetros o ID do container que queremos enviar para o repositório que no caso do exemplo é `8d9495d05463` mas o seu será diferente. Depois informamos o namespace que é o nome da conta do Dockerhub que criamos anteriormente e o nome da imagem, seguindo de dois pontos `:` e a versão ou tag de versão, o nosso exemplo ficaria da seguinte maneira.

`docker tag 8d9495d05463 SEU_DOCKER_ID/docker-is-cool:latest`

Vocẽ pode utilizar o comando `docker images` novamente e verá que a imagem que taggeou estará listada na tabela porém com o seu Docker ID no começo, como fizemos no comando acima, se você conseguiu esse resultado podemos enviá-la para a nuvem.

#### Como dar Pull sua imagem

Antes de aprendermos como empurrar nossa imagem para o Dockerhub precisamos fazer login com a conta que nós criamos. Abra o terminal e digite o comando `docker login`, ele não aceita parãmetros mas solicita o seu usuário e senha para realizar o login como no exemplo abaixo.

```
docker login

    Username: *****
    Password: *****
    Login Succeeded
```

Após o login realizado com sucesso podemos enviar nossa imagem utilizando o comando `docker push`, o comando gera diversos outputs, não se assuste, isso acontece porque cada camada é pushada separadamente. Ao utilizar o comando seu retorno será similar ao abaixo.

```
docker push dockerID/docker-is-cool

The push refers to a repository [dockerID/docker-is-cool] (len: 1)
8d9495d05463: Image already exists
...
e9e06b06e14c: Image successfully pushed
Digest: sha256:ad89e88beb7dc73bf55d456e2c600e0a39dd6c9500d7cd8d1025626c4b985011
```
