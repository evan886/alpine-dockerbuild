# alpine-mysql
a docker image base on alpine with mysql

## build image (docker)
```
docker build -t local/evan/alpine-mysql:3.14 .
```
## build image (docker-compose)
```
cp .env-dist .env
vi  .env # change environment if you need
docker-compose build
```

## Usage (docker)
```
docker run -it --name mysql -p 3306:3306 -v $(pwd):/app -e MYSQL_DATABASE=admin -e MYSQL_USER=lai -e MYSQL_PASSWORD=evanlaixxxx -e MYSQL_ROOT_PASSWORD=111111 local/evan/alpine-mysql:3.14
```

## Usage (docker-compose)
```
docker-compose up -d
```

It will:
- set no password for 'root' with localhost connections;
- set password for 'root' with non-localhost connections (default is 'root2240881');
- create a new db (default is 'admin');
- create an user and set his password for non-localhost connections only (defaults are 'evan' and 'evanlai36').
