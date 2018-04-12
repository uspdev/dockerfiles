# Docker + Laravel + PostgreSQL + Sybase/MSSQL
- Container para desenvolvimento com PHP
    - Possui as dependências para o acesso às bases Sybase/MSSQL replicadas
- Container para o banco de dados PostgreSQL

## Instruções
### Requisitos
- [Docker CE](https://www.docker.com/community-edition#/download)
- [Docker Compose](https://docs.docker.com/compose/install/#install-compose)
### Como usar
Os passos abaixo devem ser executados no mesmo diretório, mas você pode adaptar para o seu ambiente e para usar em aplicações já existentes.
- Crie um projeto Laravel usando a imagem "docker-laravel-sybase":
    - docker run -it --rm -v $(pwd):/app uspdev/docker-laravel-sybase composer create-project laravel/laravel app
- Altere os parametros de conexão no arquivo .env
```
    DB_CONNECTION=pgsql
    DB_HOST=database
    DB_PORT=5432
    DB_DATABASE=homestead
    DB_USERNAME=homestead
    DB_PASSWORD=secret
```
- Use o docker-compose.yml para subir a aplicação e o banco de dados:
    - ```docker-compose up -d```
    - Acesse http://localhost:8080 no navegador
- Faça suas tarefas usando o container
    - ```docker exec -it webserver php artisan make:auth```
    - ```docker exec -it webserver php artisan migrate```
    - etc.

