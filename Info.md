## Сборка образа Docker из репозитория ##

https://raw.githubusercontent.com/username/repository/main/Dockerfile

- username - имя пользователя
- repository - название репозитория

## Вход в консоль mongodb ##

__sudo docker exec -it deployment_mongo_1 mongo__

От администратора:
__admin -u name -p password__

## Подключение к mongodb через pymongo ##

__MongoClient('mongodb://user:password@mongo:port')__

__user, password__ - имя пользователя и пароль базы данных

__mongo__ - имя контейнера с mongodb из файла docker-compose.yml

[Руководство по добавлению mongodb в docker-compose.yml](https://hub.docker.com/_/mongo)

Чтобы требуемый контейнер увидел mongodb, нужно прописать его в разделе links:

  ```backend_test2:
    image: backend_test2:latest
    restart: always
    ports: 
      - 5006:5006
    links:
      - mongo
      ```
