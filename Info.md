## Сборка образа Docker из репозитория ##

https://raw.githubusercontent.com/username/repository/main/Dockerfile

- username - имя пользователя
- repository - название репозитория

## Вход в консоль mongodb ##

`sudo docker exec -it deployment_mongo_1 mongo`

От администратора:
__admin -u name -p password__

## Подключение к mongodb через pymongo ##

__MongoClient('mongodb://user:password@mongo:port')__

__user, password__ - имя пользователя и пароль базы данных

__mongo__ - имя контейнера с mongodb из файла docker-compose.yml

[Руководство по добавлению mongodb в docker-compose.yml](https://hub.docker.com/_/mongo)

Чтобы требуемый контейнер увидел mongodb, нужно прописать его в разделе links:

  `backend_test2:
    image: backend_test2:latest
    restart: always
    ports: 
      - 5006:5006
    links:
      - mongo`
 
 ## Прописка контейнера в nginx.conf ##
 
 Вверху файла
 
 `    upstream backend_test2 {
      server backend_test2:5006;  `
      
__backend_test2 №1__ - имя хоста?

__backend_test2 №2__ - имя образа и порт, который он использует

Внизу файла (блок server)

`      location /api/questionnaries/ {
        proxy_pass http://backend_test2/;
      }`
      
После __location__ идет адрес на сервере, по которому будет работать контейнер

После __proxy_pass__ - имя из __upstream__
      
## Docker-compose ##

`sudo docker-compose up -d` - запустить то, что прописано в __docker-compose.yml__? -d - фоновый режим

`sudo docker-compose -f docker-compose.yml up` - перезапустить то, что прописано в __docker_compose.yml__

## Yarn не хотел запускаться ##

Решение было найдено [здесь](https://laracasts.com/discuss/channels/laravel/sh-1-cross-env-permission-denied).

## Импорт данных в mongodb из файла ##

1. Загрузить файлы для импорта на сервер:

```
scp _"путь до файла"_ "имя пользователя"@"адрес сервера":"путь назначения для файла"
```

2. Добавить их в контейнер с MongoDB:

```
sudo docker cp "путь до файла" "'название контейнера с БД':/'путь назначения для файла'"
```
3. Выполнить команду импорта (в этом примере - с авторизацией в MongoDB в качестве администратора):

```
sudo docker exec "название контейнера с БД" mongoimport -d "название БД" -c "название коллекции" --authenticationDatabase admin --username "имя пользователя" --password "пароль" --file "путь до файла с данными внутри контейнера"
```
