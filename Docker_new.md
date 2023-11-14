
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


26. **How can you view the Docker logs in real-time for multiple containers?**
    Command: `docker logs -f $(docker ps -q)`

27. **What command would you use to limit the container's network bandwidth?**
    Command: `docker run --net=container:[container_id/name] [image_name]`

28. **How do you share namespaces between containers?**
    Command: Not directly achievable via command; it involves custom configurations and orchestration tools like Kubernetes.

29. **How can you run a Docker container with a specific user ID?**
    Command: `docker run --user=[user_id] [image_name]`

30. **What's the command to list dangling volumes?**
    Command: `docker volume ls -f dangling=true`

31. **How do you specify a custom Dockerfile name while building an image?**
    Command: `docker build -t [image_name] -f [Dockerfile_name] .`

32. **How can you limit the number of available CPUs for a container?**
    Command: `docker run --cpuset-cpus=0,1 [image_name]`

33. **What command would you use to create a Docker container with a specific hostname?**
    Command: `docker run --hostname [custom_hostname] [image_name]`

34. **How do you pause all running containers at once?**
    Command: `docker pause $(docker ps -q)`

35. **How can you set up a Docker container to automatically remove itself after exiting?**
    Command: `docker run --rm [image_name]`

36. **What's the command to set up a container to start in read-only mode?**
    Command: `docker run --read-only [image_name]`

37. **How do you execute a command inside a running container without starting a new shell?**
    Command: `docker exec [container_id/name] [command]`

38. **How can you copy a file from the local filesystem to a running container?**
    Command: `docker cp [local_file_path] [container_id]:[destination_path]`

39. **What command would you use to list all Docker containers sorted by their creation time?**
    Command: `docker ps --format "table {{.ID}}\t{{.CreatedAt}}\t{{.Image}}\t{{.Names}}" --sort=created`

40. **How do you enable Docker's experimental features?**
    Command: Update the Docker daemon configuration file to include `"experimental": true`.

41. **How can you view the detailed history of a specific image layer?**
    Command: `docker history --no-trunc [image_name]`

42. **What's the command to display the version of Docker Engine?**
    Command: `docker version`

43. **How do you set up a container to share the network namespace with another container?**
    Command: Use the `--network container:[container_id/name]` flag during container creation.

44. **How can you run a command on a Docker container directly from a stopped state?**
    Command: `docker start -a -i [container_id/name]`

45. **What command would you use to list the events emitted by Docker daemon?**
    Command: `docker events`

46. **How do you set up a container to limit its I/O read and write rate?**
    Command: `docker run --device-read-bps=/dev/sda:1mb --device-write-bps=/dev/sda:1mb [image_name]`

47. **How can you view detailed information about Docker's resource usage and constraints?**
    Command: `docker system df`

48. **What command would you use to export a container's filesystem as a tar archive?**
    Command: `docker export [container_id] > /path/to/container.tar`

49. **How do you view the Docker Hub official images available for pull?**
    Command: `docker search [image_name]`

50. **How can you create a Docker container with a specific DNS server?**
    Command: `docker run --dns [dns_server] [image_name]`


26. **How can you view the Docker logs in real-time for multiple containers?**
    Command: `docker logs -f $(docker ps -q)`

27. **What command would you use to limit the container's network bandwidth?**
    Command: `docker run --net=container:[container_id/name] [image_name]`

28. **How do you share namespaces between containers?**
    Command: Not directly achievable via command; it involves custom configurations and orchestration tools like Kubernetes.

29. **How can you run a Docker container with a specific user ID?**
    Command: `docker run --user=[user_id] [image_name]`

30. **What's the command to list dangling volumes?**
    Command: `docker volume ls -f dangling=true`

31. **How do you specify a custom Dockerfile name while building an image?**
    Command: `docker build -t [image_name] -f [Dockerfile_name] .`

32. **How can you limit the number of available CPUs for a container?**
    Command: `docker run --cpuset-cpus=0,1 [image_name]`

33. **What command would you use to create a Docker container with a specific hostname?**
    Command: `docker run --hostname [custom_hostname] [image_name]`

34. **How do you pause all running containers at once?**
    Command: `docker pause $(docker ps -q)`

35. **How can you set up a Docker container to automatically remove itself after exiting?**
    Command: `docker run --rm [image_name]`

36. **What's the command to set up a container to start in read-only mode?**
    Command: `docker run --read-only [image_name]`

37. **How do you execute a command inside a running container without starting a new shell?**
    Command: `docker exec [container_id/name] [command]`

38. **How can you copy a file from the local filesystem to a running container?**
    Command: `docker cp [local_file_path] [container_id]:[destination_path]`

39. **What command would you use to list all Docker containers sorted by their creation time?**
    Command: `docker ps --format "table {{.ID}}\t{{.CreatedAt}}\t{{.Image}}\t{{.Names}}" --sort=created`

40. **How do you enable Docker's experimental features?**
    Command: Update the Docker daemon configuration file to include `"experimental": true`.

41. **How can you view the detailed history of a specific image layer?**
    Command: `docker history --no-trunc [image_name]`

42. **What's the command to display the version of Docker Engine?**
    Command: `docker version`

43. **How do you set up a container to share the network namespace with another container?**
    Command: Use the `--network container:[container_id/name]` flag during container creation.

44. **How can you run a command on a Docker container directly from a stopped state?**
    Command: `docker start -a -i [container_id/name]`

45. **What command would you use to list the events emitted by Docker daemon?**
    Command: `docker events`

46. **How do you set up a container to limit its I/O read and write rate?**
    Command: `docker run --device-read-bps=/dev/sda:1mb --device-write-bps=/dev/sda:1mb [image_name]`

47. **How can you view detailed information about Docker's resource usage and constraints?**
    Command: `docker system df`

48. **What command would you use to export a container's filesystem as a tar archive?**
    Command: `docker export [container_id] > /path/to/container.tar`

49. **How do you view the Docker Hub official images available for pull?**
    Command: `docker search [image_name]`

50. **How can you create a Docker container with a specific DNS server?**
    Command: `docker run --dns [dns_server] [image_name]`

51. **How can you create a Docker container with a specific entry point?**
    Command: `docker run --entrypoint [entry_point_command] [image_name]`

52. **What command would you use to set up a container to use a specific network interface?**
    Command: Not directly achievable via command; requires configuring Docker networking and potentially using custom network plugins.

53. **How do you limit the container's read-only mounts to specific directories?**
    Command: `docker run --read-only --tmpfs /tmp [image_name]`

54. **How can you display the layers of a specific image with their IDs and sizes?**
    Command: `docker image inspect --format='{{json .RootFS.Layers}}' [image_name]`

55. **What's the command to check the Docker daemon's current configuration?**
    Command: `docker system info`

56. **How do you set up a container to run with a specific capability?**
    Command: `docker run --cap-add [capability_name] [image_name]`

57. **How can you limit the container's access to specific devices?**
    Command: `docker run --device=/dev/sda [image_name]`

58. **What command would you use to list all the available Docker plugins?**
    Command: `docker plugin ls`

59. **How do you mount a host directory into a Docker container with read-write access?**
    Command: `docker run -v /host/dir:/container/dir [image_name]`

60. **How can you create a Docker container with a specific timezone?**
    Command: `docker run -e TZ=Europe/London [image_name]`

61. **What's the command to display the Docker container's environmental variables?**
    Command: `docker inspect --format '{{ .Config.Env }}' [container_id/name]`

62. **How do you set up a Docker container to use a custom network bridge?**
    Command: `docker run --network [custom_network_bridge] [image_name]`

63. **How can you copy a file from a container to the local filesystem?**
    Command: `docker cp [container_id]:[source_path] [destination_path]`

64. **What command would you use to view the changes made to a container's file system?**
    Command: `docker diff [container_id/name]`

65. **How do you set up a container to limit its CPU shares relative to other containers?**
    Command: `docker run --cpu-shares 512 [image_name]`

66. **How can you set up a container to limit its block IO read and write rate?**
    Command: `docker run --device-read-iops=/dev/sda:1000 --device-write-iops=/dev/sda:1000 [image_name]`

67. **What's the command to show the Docker container's networking details?**
    Command: `docker network inspect [network_name]`

68. **How do you set up a container to use a specific DNS search domain?**
    Command: `docker run --dns-search [search_domain] [image_name]`

69. **How can you check the security configuration of a Docker container?**
    Command: `docker container inspect [container_id/name] --format '{{ .HostConfig.SecurityOpt }}'`

70. **What command would you use to display a Docker container's PID (Process ID)?**
    Command: `docker inspect --format '{{ .State.Pid }}' [container_id/name]`

71. **How do you set up a Docker container to share the PID namespace with another container?**
    Command: Use the `--pid=container:[container_id/name]` flag during container creation.

72. **How can you view the Docker container's CPU usage in percentage?**
    Command: `docker stats --format "table {{.Container}}\t{{.CPUPerc}}"`

73. **What command would you use to limit the container's memory usage and swap space?**
    Command: `docker run -m 512m --memory-swap=1g [image_name]`

74. **How do you set up a Docker container to restart only a specific number of times on failure?**
    Command: `docker run --restart=on-failure:5 [image_name]`

75. **How can you display the Docker container's network statistics?**
    Command: `docker stats --format "table {{.Container}}\t{{.NetIO}}"`

76. **How do you set up a Docker container to use a specific kernel version?**
    Command: Not directly achievable via command; requires advanced configurations and potentially using custom kernel parameters.

77. **What command would you use to view the Docker container's memory usage statistics?**
    Command: `docker stats --format "table {{.Container}}\t{{.MemUsage}}"`

78. **How can you view the Docker container's I/O statistics?**
    Command: `docker stats --format "table {{.Container}}\t{{.BlockIO}}"`

79. **How do you set up a container to restrict its network ingress/egress traffic?**
    Command: Not directly achievable via command; involves network policies and firewall configurations.

80. **How can you set up a Docker container to use a specific cgroup parent?**
    Command: `docker run --cgroup-parent [cgroup_parent_name] [image_name]`

81. **What command would you use to display the current Docker container's CPU throttling information?**
    Command: `docker inspect --format '{{ .HostConfig.CPUQuota }}' [container_id/name]`

82. **How do you set up a Docker container to use a specific MAC address?**
    Command: `docker run --mac-address [custom_MAC_address] [image_name]`

83. **How can you list all the Docker container's mounted volumes and their paths?**
    Command: `docker inspect --format '{{range .Mounts}}{{.Source}} -> {{.Destination}}{{"\n"}}{{end}}' [container_id/name]`

84. **What's the command to show the Docker container's hostname?**
    Command: `docker inspect --format '{{ .Config.Hostname }}' [container_id/name]`

85. **How do you set up a Docker container to use a specific CPU architecture?**
    Command: Not directly achievable via command; requires building images for specific architectures or using emulators.

86. **How can you view the Docker container's total memory and CPU limits?**
    Command: `docker inspect --format '{{ .HostConfig.Memory }}' [container_id/name]` and `docker inspect --format '{{ .HostConfig.CPUShares }}' [container_id/name]`

87. **What command would you use to display the Docker container's filesystem type and mounts?**
    Command: `docker inspect --format '{{json .Mounts}}' [container_id/name]`

88. **How do you set up a Docker container to share the IPC namespace with another container?**
    Command: Use the `--ipc=container:[container_id/name]` flag during container creation.

89. **How can you display the Docker container's environment variables including defaults?**
    Command: `docker inspect --format '{{json .Config.Env}}' [container_id/name]`

90. **What's the command to display the Docker container's current state, including running or stopped?**
    Command: `docker inspect --format '{{ .State.Status }}' [container_id/name]`

91. **How do you set up a Docker container to use a specific UTS namespace?**
    Command: Not directly achievable via command; requires custom configurations and potentially namespace sharing.

92. **How can you view the Docker container's attached devices and their paths?**
    Command: `docker inspect --format '{{range .Mounts}}{{.Name}} -> {{.Source}}{{"\n"}}{{end}}' [container_id/name]`

93. **What command would you use to display the Docker container's current health status?**
    Command: `docker inspect --format '{{ .State.Health.Status }}' [container_id/name]`

94. **How do you set up a Docker container to use a specific user namespace?**
    Command: Not directly achievable via command; involves advanced configurations and potentially custom namespaces.

95. **How can you view the Docker container's exit code from its last run?**
    Command: `docker inspect --format '{{ .State.ExitCode }}' [container_id/name]`

96. **What's the command to view Docker container's resource utilization over time?**
    Command: `docker stats --format "table {{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}\t{{.NetIO}}\t{{.BlockIO}}"`

97. **How do you set up a Docker container to share the UTS namespace with another container?**
    Command: Use the `--uts=container:[container_id/name]` flag during container creation.

98. **How can you display the Docker container's start time and uptime?**
    Command: `docker inspect --format '{{ .State.StartedAt }}' [container_id/name]` for start time and calculate uptime manually.

99. **What command would you use to display the Docker container's Open ports?**
    Command: `docker port [container_id/name]`

100. **How do you set up a Docker container to use a specific SELinux label?**
     Command: `docker run --security-opt "label=type:label_value" [image_name]`

