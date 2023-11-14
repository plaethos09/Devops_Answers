
1 **How do you list all containers?**
   Command: `docker ps -a`

2. **What command would you use to stop a running container?**
   Command: `docker stop [container_id/name]`

3. **How can you remove a container?**
   Command: `docker rm [container_id/name]`

4. **How do you pull a Docker image from a repository?**
   Command: `docker pull [image_name]`

5. **How do you run a Docker container interactively and attach to its console?**
   Command: `docker run -it [image_name]`

6. **How can you check the logs of a running container?**
   Command: `docker logs [container_id/name]`

7. **How do you list all Docker images?**
   Command: `docker images`

8. **How can you remove a Docker image?**
   Command: `docker rmi [image_id/name]`

9. **What's the command to run a container in detached mode?**
   Command: `docker run -d [image_name]`

10. **How do you map a host port to a container port when running a container?**
    Command: `docker run -p [host_port]:[container_port] [image_name]`

11. **How do you enter into a running container's shell?**
    Command: `docker exec -it [container_id/name] bash`

12. **How can you inspect a Docker container's configuration?**
    Command: `docker inspect [container_id/name]`

13. **How do you create a Docker network?**
    Command: `docker network create [network_name]`

14. **What command would you use to list Docker networks?**
    Command: `docker network ls`

15. **How do you remove a Docker network?**
    Command: `docker network rm [network_name]`

16. **How do you list all Docker volumes?**
    Command: `docker volume ls`

17. **How can you create a Docker volume?**
    Command: `docker volume create [volume_name]`

18. **How do you remove a Docker volume?**
    Command: `docker volume rm [volume_name]`

19. **How can you see detailed information about Docker system events?**
    Command: `docker events`

20. **What command would you use to pause a running container?**
    Command: `docker pause [container_id/name]`

21. **How do you unpause a paused container?**
    Command: `docker unpause [container_id/name]`

22. **What's the command to restart a container?**
    Command: `docker restart [container_id/name]`

23. **How can you create a Docker image using a Dockerfile?**
    Command: `docker build -t [image_name] .`

24. **How do you push a Docker image to a repository?**
    Command: `docker push [image_name]`

25. **What's the command to tag a Docker image?**
    Command: `docker tag [image_id] [new_image_name:tag]`



1. **How do you list all running containers?**
   Command: `docker ps`

2. **What command would you use to display the sizes of all containers, images, and volumes?**
   Command: `docker system df`

3. **How can you show detailed information about a specific container?**
   Command: `docker inspect [container_id/name]`

4. **How do you remove all stopped containers?**
   Command: `docker container prune`

5. **What's the command to remove all unused images?**
   Command: `docker image prune`

6. **How can you remove all unused volumes?**
   Command: `docker volume prune`

7. **How do you run a container with environment variables?**
   Command: `docker run -e "KEY=VALUE" [image_name]`

8. **What command would you use to list dangling images?**
   Command: `docker images -f "dangling=true"`

9. **How can you limit the CPU usage of a container?**
   Command: `docker run --cpus=0.5 [image_name]`

10. **How do you limit memory usage for a container?**
    Command: `docker run -m 512m [image_name]`

11. **What's the command to display the history of an image?**
    Command: `docker history [image_name]`

12. **How can you copy files from a container to the local filesystem?**
    Command: `docker cp [container_id]:[source_path] [destination_path]`

13. **How do you view real-time resource usage statistics of running containers?**
    Command: `docker stats`

14. **What command would you use to create a Docker network with a specific subnet and gateway?**
    Command: `docker network create --subnet=192.168.1.0/24 --gateway=192.168.1.1 [network_name]`

15. **How can you inspect the network configuration of a specific container?**
    Command: `docker network inspect [network_name]`

16. **How do you attach a container to a specific network at runtime?**
    Command: `docker network connect [network_name] [container_id/name]`

17. **What's the command to detach a container from a network?**
    Command: `docker network disconnect [network_name] [container_id/name]`

18. **How do you set up a Docker container to automatically restart on failure?**
    Command: `docker run --restart=always [image_name]`

19. **What command would you use to stop and remove all containers?**
    Command: `docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q)`

20. **How can you prune all unused Docker resources in a single command?**
    Command: `docker system prune -a`

21. **How do you change the default location of Docker containers and images storage?**
    Command: Update Docker daemon configuration.

22. **What's the command to set up a container to restart unless explicitly stopped?**
    Command: `docker run --restart=unless-stopped [image_name]`

23. **How can you change the Docker container's restart policy post-creation?**
    Command: `docker update --restart=always [container_id/name]`

24. **How do you create a Docker volume and specify a storage driver?**
    Command: `docker volume create --driver [driver_name] [volume_name]`

25. **What's the command to prune all stopped containers and volumes?**
    Command: `docker container prune -f && docker volume prune -f`



