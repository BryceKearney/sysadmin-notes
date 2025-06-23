Basic Docker commands, so easy even your grandma can do it!

-------
List running containers.
```
docker ps
```
- Shows container ID, image, status, ports, and names.
- **Tip**: Use docker ps -a to include stopped containers.

------
Display Docker system information.
```
docker info --format '{{.ContainersRunning}}/{{.Containers}} containers running/total'
```
* Docker Info command also works*

--------------
Monitor real-time resource usage (CPU, memory, network) for containers.
```
docker stats
```
- Press Ctrl+C to exit.
- **Tip**: Use docker stats --no-stream for a single snapshot.

---------------
docker logs: View logs for a specific container.
```
docker logs webserver
```
- Replace webserver with container name or ID.
- **Real-Time Logs**: Use docker logs -f to follow logs (like tail -f).
- **Example Use**: Debug a container failing to start.

----------
**docker top**: Show running processes inside a container.
```
docker top webserver
```
- Displays processes (like ps aux) for the container.
- **Use Case**: Check if a process (e.g., nginx) is running correctly.

---------------
**docker system df**: Check disk usage by Docker images, containers, and volumes.
```
docker system df
```
* Identifies space hogs (e.g., unused images).

-----

### 2. Managing Containers

These commands help you create, start, stop, and remove containers.

- **docker run**: Create and start a new container.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker run -d --name webserver -p 80:80 nginx`
    
    - -d: Run in detached mode (background).
    - --name: Assign a name (e.g., webserver).
    - -p 80:80: Map host port 80 to container port 80.
    - **Example**: Runs an Nginx web server accessible at http://<host-ip>:80.
- **docker start/stop/restart**: Control container state.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker start webserver docker stop webserver docker restart webserver`
    
    - Use container name or ID.
    - **Tip**: stop gracefully shuts down; use docker kill for immediate termination.
- **docker rm**: Remove a stopped container.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker rm webserver`
    
    - **Tip**: Use docker rm -f webserver to force-remove a running container.
- **docker exec**: Run a command inside a running container.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker exec -it webserver bash`
    
    - -it: Interactive terminal (e.g., open a shell).
    - **Example Use**: Run docker exec webserver ps aux to check processes.
- **docker inspect**: View detailed container configuration.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker inspect webserver`
    
    - Shows JSON with IP, ports, volumes, etc.
    - **Filter**: docker inspect --format '{{.NetworkSettings.IPAddress}}' webserver for container IP.

---

### 3. Managing Images

Docker images are the templates for containers. These commands help you manage them.

- **docker images**: List all images.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker images`
    
    **Example Output**:
    
    text
    
    CollapseWrap
    
    Copy
    
    `REPOSITORY TAG IMAGE ID CREATED SIZE nginx latest 1234567890ab 2 weeks ago 140MB`
    
    - **Tip**: Use docker images -a to include intermediate images.
- **docker pull**: Download an image from a registry (e.g., Docker Hub).
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker pull ubuntu:20.04`
    
    - Specify tag (e.g., 20.04) for a specific version.
- **docker rmi**: Remove an image.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker rmi nginx`
    
    - **Tip**: Use docker rmi -f to force removal if in use.
- **docker build**: Build an image from a Dockerfile.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker build -t myapp:latest .`
    
    - -t: Tag the image (e.g., myapp:latest).
    - .: Build from Dockerfile in current directory.

---

### 4. Docker System Maintenance

Keep Docker clean and running efficiently with these commands.

- **docker system prune**: Remove unused containers, networks, and dangling images.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker system prune`
    
    - **Caution**: Confirm before running, as it deletes stopped containers and unused data.
    - **Advanced**: Use docker system prune -a to remove all unused images.
- **docker volume ls and docker volume rm**: Manage volumes (persistent storage).
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker volume ls docker volume rm my_volume`
    
    - **Tip**: Check for orphaned volumes with docker volume ls -f dangling=true.
- **docker network ls and docker network rm**: Manage Docker networks.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker network ls docker network rm my_network`
    
    - **Example Use**: Create a custom network for containers to communicate:
        
        bash
        
        CollapseWrapRun
        
        Copy
        
        `docker network create my_network`
        
- **docker system info**: Check Docker’s system status.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker system info`
    
    - Shows version, storage driver (e.g., overlay2), and resource limits.
    - **Proxmox Note**: If using ZFS, ensure Docker’s storage driver is compatible (e.g., overlay2 or zfs).
- **docker update**: Adjust container resource limits.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker update --cpus="2" --memory="512m" webserver`
    
    - Limits webserver to 2 CPUs and 512MB RAM.
    - **Proxmox Tip**: Align with VM/container resource allocations.

---

### 5. Docker-Specific Monitoring

These commands provide deeper insights into Docker’s performance and health.

- **docker events**: Monitor real-time Docker events (e.g., container start/stop).
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker events`
    
    - Press Ctrl+C to stop.
    - **Use Case**: Debug unexpected container crashes.
- **docker container top**: Show top-like process info for all containers.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker container top`
    
- **docker container ls -s**: List containers with size information.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker container ls -a -s`
    
    - Shows container size (useful for disk management).
- **Resource Monitoring with cAdvisor**: Install cAdvisor (Container Advisor) for detailed container metrics via a web UI:
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker run -d -p 8080:8080 --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro google/cadvisor:latest`
    
    - Access at http://<host-ip>:8080.
    - Shows CPU, memory, and network usage per container.

---

### 6. General Docker Commands to Know

These foundational commands help you navigate and troubleshoot Docker.

- **docker version**: Check Docker client and server versions.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker version`
    
    - Ensures compatibility between client and daemon.
- **docker login**: Authenticate with a Docker registry.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker login`
    
    - Required for private registries or pushing images.
- **docker cp**: Copy files to/from a container.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker cp webserver:/etc/nginx/nginx.conf ./nginx.conf docker cp ./new.conf webserver:/etc/nginx/new.conf`
    
- **docker commit**: Create a new image from a container’s changes.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker commit webserver my-nginx:custom`
    
    - Saves container state as a new image.
- **docker export/import**: Export/import container filesystems.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker export webserver > webserver.tar docker import webserver.tar myimage:latest`
    
- **docker history**: Show an image’s layer history.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `docker history nginx`
    
    - Helps understand image size and composition.