<h2 align="center"> Docker - Nginx - Php7.3-fpm - Maria DB - Redis </h2>

## 1° Download
```console
git clone https://github.com/csvitor/nginx-php7.4fpm-in-docker.git "projeto" 
```
```console
cd projeto
```
## 2º configurar dominio se necessario
```console
nano ./nginx/config/web.conf
```
## 3° rodar container docker
```console
  ./start 
```

## Acesso ao banco de dados
- acesse localhost:8080
- user: root
- pass: root
- server: db ( como foi definido no docker-compose.yml )