## Что нужно добавить ##

___nginx.conf___

`
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
`
XXX
