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


```
lscpu -e
```

```
lscpu -e
```