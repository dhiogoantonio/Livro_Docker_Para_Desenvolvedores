# Configurações

Com o objetivo de viabilizar que o código seja o mais parametrizável possível, essa boa prática indica que parametrização deve armazenar as configurações no seu código. Essa parametrização deve estar no ambiente, normalmente especificada via variável de ambiente.

Normalmente quando a configuração está estaticamente explícita no código, será necessário modificar manualmente e efetuar um novo build dos binários a cada reconfiguração do sistema.

Como demonstramos na boa prática codebase, usamos uma variável de ambiente para modificar qual o volume que usaremos no redis, ou seja, de certa forma já estamos seguindo essa boa prática.

A configuração foi realizada no docker-compose.yml, que é o arquivo responsável por configurar o ambiente em questão. Perceba no arquivo abaixo a configuração da variável **ENV_APP**:

```
web:
  build: .
  ports:
   - "5000:5000"
  volumes:
   - .:/code
  links:
   - redis
  labels:
   - 'app.environment=${ENV_APP}'
redis:
  image: redis
  volumes:
   - dados_${ENV_APP}:/data
  labels:
   - 'app.environment=${ENV_APP}'
```

Esse arquivo tem todos os detalhes de configuração implantados até então, ou seja, essa boa prática é seguida com ajuda do Docker, pois o código é o mesmo e a configuração é um anexo da solução e pode ser parametrizada de maneira distinta com base no que for configurado nesse arquivo.

Se aplicação crescer bastante, as variáveis podem ser carregadas em arquivo e parametrizadas no docker-compose.yml com a opção **"env_file"**.