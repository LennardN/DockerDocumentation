# Commands

## Run MySQL Databse Container
```bash
docker run --name container_name -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=testdb -v my-db-volume:/var/lib/mysql -d mysql
```
## Run SQL Query
```bash
docker exec -it container_name mysql -p -e 'SELECT * FROM testdb.testtable'
```
## Create DB Volume
```bash
docker volume create dbvolume
```
## Build own Webserver Image
```bash
docker build -t lennard/webserver .
```
## Run own Webserver Container
```bash
docker run -p 80:8080 -d lennard/webserver
```