# Docker Compose:
Docker Compose is a tool used to define and manage multi-container Docker applications. 
It simplifies the process of setting up, configuring, and running multiple Docker containers that work together as part of a single application.
Start by creating a directory containung the build contexts of all the neccesary containers for your application.
In the next step you're going to create a file called: docker-compose.yml Example for such a file can be seen below.
```yaml
services:
  webserver:
    build: ./testWebserver
    image: 141.51.134.158:5000/testwebserver
    environment:
      DATABASE_CONNECTION_HOST: userapp_database
      DATABASE_CONNECTION_USER: root
      DATABASE_CONNECTION_NAME: testdb
      DATABASE_CONNECTION_PASSWORD: 123
    ports:
      - "80:8080"
    networks:
      - testnetwork

  database:
    build: ./testMysqlserver
    image: 141.51.134.158:5000/testsqlserver
    environment:
      MYSQL_DATABASE: testdb
      MYSQL_ROOT_PASSWORD: 123
    volumes:
      - dbvolume:/var/lib/mysql:rw
    networks:
      - testnetwork

volumes:
  dbvolume:
    driver: local

networks:
  testnetwork: 
    driver: overlay
    name: backendnetwork
```
### After successfully creating your docker-compose.yaml file, you can start the application and all its containers by running:
```bash
docker compose up
```
### Following options are available:
#### To see all options, visit [the official documentation](https://docs.docker.com/reference/cli/docker/compose/up/)
| Option                    | Description                                                          |
|---------------------------|----------------------------------------------------------------------|
| `-d`, `--detach`          | Run containers in the background.                                    |
| `--abort-on-container-exit` | Stops all containers if any container is stopped. Incompatible with `-d`. |
| `--pull <policy>`         | Pull the image before running. The policy can be `"always"`, `"missing"`, or `"never"`. |

### If you choose to run the application in detached mode, you can stop it by using
```bash
docker compose down
```