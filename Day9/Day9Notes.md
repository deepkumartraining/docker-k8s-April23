#Day 9
******************************************************************************************
```
Docker Volume
Docker Logging and tracing
DockerFile Multi Stage Build
Need of DockerCompose

Commands
docker volume create dockerpoc
docker volume ls
docker volume inspect dockerpoc
Mount - 
docker run -it -v dockerpoc:/insidecontainer --name my-container-01 ubuntu/<imageid>
Test with persistent data and multiple container
docker run -it -v dockerpoc:/insidecontainer --name my-container-02 ubuntu/<imageid>

Docker logs <container id>
docker logs --tail 100 <container id>
docker logs --follow 1m <container-id>

docker run -it -v dockerpoc:/insidecontainer --name volumepoc 08d22c0ceb15

Example with Mysql - https://www.freecodecamp.org/news/docker-mount-volume-guide-how-to-mount-a-local-directory/

docker volume rm <Volume>

Remove all unused volume in case no container connected

docker volume prune

Mount with -v and --mount


systemctl status lightdm
service lightdm status

docker run --volumes-from  dockervolumepoc:insidecontainer3 

docker run --volumes-from some-volume docker-image-name:tag
docker run -d --volumes-from dockerpoc node-docker:latest

docker exec baee9b3f82b3 sh -c 'ls -altr'
ll /insideubuntu2
```