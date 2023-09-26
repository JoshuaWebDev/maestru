<p style="display: flex; justify-content: center">
<img src="public/img/logo-maestru.png" alt="Logo Maestru">
</p>

## Sobre o Maestru

Maestru é um gerenciador de projetos criado para facilitar o gerenciamento de projetos e tarefas dos colaboradores envolvidos no projeto. Ele foi desenvolvido usando as seguintes tecnologias:

- [PHP](https://www.php.net/)
- [Laravel framework](https://laravel.com).
- [MySQL](https://www.mysql.com/).

## Instalação

### Ambiente de desenvolvimento

#### Requisitos

- Docker

#### Configurações Iniciais

Copie o arquivo ```.env.example``` e renomeie para ```.env```

```
cp .env.example .env
```
É possível modificar as configurações da base de dados alterando o valor de ```DB_DATABASE``` para o nome do banco de dados que desejar, o valor de ```DB_USERNAME``` para o usuário que terá acesso a base de dados e o valor de ```DB_PASSWORD``` para a senha de acesso a base de dados.

```
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=
```

Altere o valor de ```WWWUSER``` para o nome do seu usuário. E altere o valor de ```WWWGROUP``` para o nome do grupo do seu usuário.

```
WWWUSER=
WWWGROUP=
```

Acesse o arquivo ```docker/initial-configurations``` e altere a variável user para o nome do seu usuário.

```bash
#!/bin/bash
projectname="maestru"
user=<altere esse cara aqui>
```

Acesse a pasta do projeto e execute o comando a seguir para levantar o container com o ambiente de desenvolvimento.

```
docker-compose up -d
```

Após terminar o processo de criação de container execute o comando a seguir:

```
docker exec -it maestru-app initial-configurations
```

Após finalizar as configurações iniciais já é possível visualizar a página inicial da aplicação no navegador no endereço http://127.0.0.1

# FAQ (Frequent Answers & Questions)

Aqui algumas respostas de possíveis dúvidas que podem surgir durante o processo de instalação.

- O container `db` não sobe

> Se após executar o comando `docker-compose up -d` o container `app` subir mas o `db` verifica as mensagens de log se há alguma mensagem do tipo:
> 
>> [ERROR] [MY-013236] [Server] The designated data directory /var/lib/mysql/ is unusable. You can remove all files that the server added to it.
> 
> Acesse o diretório `docker/db/` e apague todos os arquivos que estejam dentro dele

