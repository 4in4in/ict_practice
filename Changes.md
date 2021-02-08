## Что нужно добавить ##

___nginx.conf___


```
http {
  
  ...
  
  upstream backend_test2 {
    server backend_test2:5006;
  }

  server {
  ...
  index...
  add_header Access-Control-Allow-Origin *;
  add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range';
  ...
  
  location /api/questionnaries/ {
    proxy_pass http://backend_test2/;
  }
  
  }
```  
  
___docker-compose.yml___

```
...
mongo:
  image: postgres:13.1-alpine
  restart: always
  environment:
    MONGO_INITDB_ROOT_USERNAME: username
    MONGO_INITDB_ROOT_PASSWORD: password
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: username
      ME_CONFIG_MONGODB_ADMINPASSWORD: password
...
  backend_test2:
    image: backend_test2:latest
    restart: always
    ports:
      - 5006:5006
    links:
      - mongo
```
