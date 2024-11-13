# gen-app build and deploy

Сборка докер образов бэка и фронта с сохранением в GitHub Packages и разворачиванием через docker compose на VPS

## Структура
- .github
  - workflows - каталог с GitHub Action 
    * build-deploy-back.yml		- сборка бэка и деплой на VPS
    * build-deploy-front.yml 		- сборка фронта и деплой на VPS
    * deploy-back-to-vps.yml		- деплой последнего собранного образа бэка
    * deploy-front-to-vps.yml		- деплой последнего собранного образа фронта
 - Dockerfile-back	
 - Dockerfile-front
 - docker-compose-app-GA.yaml

**Бэк** -  в докерфайле собирается JAR и запускается (в контейнер передаются параметры базы данных из пайплайна), сохраняется образ в гитхабе, на VPS копируется docker compose который забирает образ из гита и запускает его

**Фронт** - в докерфайле собирается статика и запускается с помощью Serve, дальше также как бэк

## Используемые в пайплайне переменные 

|                |                          |
|----------------|-------------------------------|
|POSTGRES_NAME| Имя базы данных       |      
|POSTGRES_USERNAME          |Имя пользователя БД|
|POSTGRES_PASSWORD| Пароль пользователя БД|
|POSTGRES_PORT| Порт базы данных|
|REGISTRY_TOKEN|токен персонального доступа github|
|SERVER_HOST|IP адрес VPS|
|SERVER_PORT|SSH-порт для подключения|
|SERVER_USERNAME|Имя пользователя|
|SERVER_PASSWORD|Пароль|