##  Base de código

Com o objetivo de facilitar o controle das mudanças de código, viabilizando a rastreabilidade das alterações, essa boa prática indica que cada aplicação deve ter apenas uma base de código e, a partir do mesmo, uma aplicação pode ser implantada em distintos ambientes, mas a base precisa ser a mesma. Vale salientar que essa boa prática é necessária caso pretenda praticar o Continuous Integration ([CI](https://www.thoughtworks.com/continuous-integration)), ou seja, o mesmo código deverá ser consumido pelo processo de integração contínua e posteriormente implantado em desenvolvimento, teste e produção, mudando apenas parâmetros específicos ao ambiente em questão.

Para essa explicação, criei um [repositório](https://github.com/gomex/exemplo-12factor-docker.git) de exemplo.

Perceba que todo nosso código está dentro desse repositório, organizado por prática em cada pasta, para facilitar a reprodução. Lembre de entrar na pasta correspondente a cada boa prática apresentada.

O Docker tem uma infraestrutura que permite a utilização de variável de ambiente para parametrização da infraestrutura, sendo assim o mesmo código terá um comportamento distinto com base no valor das variáveis de ambiente.

Aqui usaremos o Docker Compose para realizar a composição de todo ambiente, fazendo com que a configuração dos distintos serviços e sua comunicação seja facilitada.

![](images/basecode.png)

Posteriormente, mais precisamente na terceira boa prática **Configuração** desse compêndio de sugestões, trataremos mais detalhadamente sobre parametrização da aplicação, por hora apenas aplicaremos opções via variável de ambiente para a arquitetura ao invés de utilizar internamente no código da aplicação.

Para configurar o ambiente de desenvolvimento para o exemplo apresentado temos esse arquivo docker-compose.yml:

```
version: '2'
services:
  web:
    build: .
    ports:
     - "5000:5000"
    volumes:
     - .:/code
    labels:
     - 'app.environment=${ENV_APP}'
  redis:
    image: redis
    volumes:
     - dados_${ENV_APP}:/data
    labels:
     - 'app.environment=${ENV_APP}'
```

O serviço redis será utilizado a partir da imagem oficial redis, sem modificação no momento e o serviço web será gerado a partir da construção de uma imagem Docker, que tem como base a imagem oficial do python 2.7. Criaremos nossa imagem através do seguinte Dockerfile:

```
FROM python:2.7
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
ADD . /code
WORKDIR /code
CMD python app.py
```

Com posse de todos os arquivos na mesma pasta, iniciaremos o ambiente com o seguinte comando:

```
export ENV_APP=devel ; docker-compose -p $ENV_APP up -d
```

Como podemos perceber na configuração que acabamos de construir, a variável “ENV_APP” definirá qual volume será usado para persistir os dados que serão enviados pela aplicação web, ou seja, com base na mudança dessa opção teremos o serviço rodando com um comportamento diferente, mas sempre a partir do mesmo código, dessa forma seguindo perfeitamente a ideia dessa primeira boa prática.