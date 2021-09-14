# Docker Mysql

```sh
$ docker run --platform=linux/amd64 --name mysql-container -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d amd64/mysql
```