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
docker run -d --restart=always --name registry -v registryvolume:/var/lib/registry -p 5000:5000 registry:2
```
Now we need to change our compose file and tell our containers what the new path for the images is.
In our case that would be done with:
```yaml
    build: <manager_with_registry_ip>:<registry_port>/<image_name>
    container_name: <container_name>
    environment:
        <bla>: <bli>
        <blo>: <blub>
    ports:
      - "<host_port>:<guest_port>"
    networks:
      - <network_name>
```
Be sure to also update your network and set it to overlay
```yaml
networks:
  <network_name>:
    driver: overlay
    name: backendnetwork
```
Upload your images, with the use of your compose file this will be very simple.
```bash
docker compose push
```
A swarm running the containers defined in your compose file is called a stack, go ahead and deploy your stack.
```bash
docker stack deploy --compose-file compose.yaml <stack_name>
```
Bring the stack down:
```bash
docker stack rm <stack_name>
```
Bring the service down:
```bash
docker service rm <service_name>
```
Leave swarm:
```bash
docker swarm leave --force
```