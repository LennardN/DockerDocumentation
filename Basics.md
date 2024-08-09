# Commands
## Run und Setup MySQL Database Container
### Run
```bash
docker run --name container_name -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=testdb -v dbvolume:/var/lib/mysql -d mysql
```
## Run SQL Query
```bash
docker exec -it container_name mysql -p -e 'SELECT * FROM testdb.testtable'
```
`-i` keep Standart Output (Console) open even if not attached

`-t` opens TTY from the container    
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
docker run --name container_name -p 80:8080 -d lennard/webserver
```
## Connect to shell of running container
```bash
docker exec -it <container_name> sh
```
## Create Network Bridge
```bash
docker network create network_name --driver='bridge'
```
## Connect Container to Network
```bash
docker network connect network_name container_name
```