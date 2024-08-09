# Docker Compose:
Docker Compose is a tool used to define and manage multi-container Docker applications. It simplifies the process of setting up, configuring, and running multiple Docker containers that work together as part of a single application.
Start by creating a directory containung the build contexts of all the neccesary containers for your application. In the next step you're going to create a file called: docker-compose.yml Example for such a file can be seen below.
```yaml
    build: <path_to_webserver>
    container_name: <webserver_name>
    environment:
      DATABASE_CONNECTION_HOST: <mysqlserver_name>
      DATABASE_CONNECTION_USER: <username>
      DATABASE_CONNECTION_NAME: <db_name>
      DATABASE_CONNECTION_PASSWORD: <passwd>
    ports:
      - "<host_port>:<guest_port>"
    networks:
      - <network_name>

  database:
    build: <path_to_mysql_server>
    container_name: <mysqlserver_name>
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: true
      MYSQL_DATABASE: <db_name>
      MYSQL_ROOT_PASSWORD: <passwd>
    volumes:
      - <volume_name>:<path_in_container>:<permissions>
    networks:
      - <network_name>

volumes:
  <volume_name>:
    driver: local

networks:
  <network_name>: {}
```
### After successfully creating your docker-compose.yml file, you can start the application and all its containers by running:
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