# Como usar o docker-compose
- Copie o arquivo [docker-compose.yml](https://github.com/uspdev/dockerfiles/blob/master/docker-compose-laravel/docker-compose.yml) para o diretório do seu projeto
- Adicione o docker-compose.yml ao .gitignore (para não atrapalhar quem estiver usando outras imagens ou não estiver usando Docker)
- Substitua <app-name> pelo nome do seu projeto
- Altere os dados de conexão no arquivo .env
```
    DB_CONNECTION=mysql
    DB_HOST=mysql
    DB_PORT=3306
    DB_DATABASE=<app-name>
    DB_USERNAME=<app-name>
    DB_PASSWORD=<app-name>
```
- Suba os serviços
    - docker-compose up -d
- Rode os comandos a partir do host
    - ```docker exec -it -w /usr/src/app <app-name>-app composer install```
    - ```docker exec -it -w /usr/src/app <app-name>-app cp .env.example .env```
    - ```docker exec -it -w /usr/src/app <app-name>-app php artisan key:generate```
    - etc.

Crie aliases para a parte repetitiva do comando, por exemplo:
- ```alias dr="docker exec -it -w /usr/src/app <app-name>-app"```
- ```dr php artisan migrate```
