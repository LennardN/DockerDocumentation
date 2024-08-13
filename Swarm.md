# Docker Swarm
Docker Swarm is a tool for managing a group of Docker containers across multiple machines as if they were one system. It helps you deploy and scale applications easily.
### Setting up Docker Swarm
If you wish to create a swarm, start by running the following command. This will make the current node a manager-node
```bash
docker swarm init 
```
You can make another machine join the swarm as a worker-node by running:
```bash
docker swarm join --token <JOIN_TOKEN> <MANAGER_IP>:<PORT>
```
In case you don't know what these parameters should look like, run:
```bash
docker swarm join-token worker
```
or alternatively:
```bash
docker swarm join-token manager
```
### Create a registry
If you want to have your containers run across multiple nodes, a way of sharing container images is necessary.
The best practice is to create a registry on your manager, you can create a registry with the following command:
```bash
docker service create --name <registry_name> -e "REGISTRY_STORAGE_DELETE_ENABLED=true" -e "REGISTRY_VALIDATION_DISABLED=true" --publish published=<host_port>,target=<container_port> registry:<version>
``` 
`REGISTRY_STORAGE_DELETE_ENABLED=true` enables the deletion of images in the Docker registry, which is otherwise disabled by default.
`REGISTRY_VALIDATION_DISABLED=true` is set to disable validation of the registry configuration.
