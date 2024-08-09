# Docker Compose Documentationservices:
```yaml
services:
  webserver:
    build: ./testWebserver
    container_name: webserver
    environment:
      DATABASE_CONNECTION_HOST: mysqlserver
      DATABASE_CONNECTION_USER: root
      DATABASE_CONNECTION_NAME: testdb
      DATABASE_CONNECTION_PASSWORD: 123
    ports:
      - "80:8080"
    networks:
      - testnetwork

  database:
    build: ./testMysqlserver
    container_name: mysqlserver
    environment:
      MYSQL_ALLOW_EMPTY_PASSWORD: true
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
  testnetwork: {}
```