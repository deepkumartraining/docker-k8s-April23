#Day 10 - Notes
*******************************************************************************
```
share running container with same volume
--volume & --mount


Same drive mount to multiple containers
#First Container
docker run -it --volume dockerpoc:/insideubuntu1 --name dockervolumepoc ubuntu
#Second Container
docker run -it --volume dockerpoc:/insideubuntu2 --name dockervolumepoc2 ubuntu


Mount drive from running container
docker run -d --volumes-from <Source-container-name> <ImageName>:<tag>
docker run -d --volumes-from dockervolumepoc deepkumartraining/node-docker:latest

docker exec baee9b3f82b3 sh -c 'ls -altr /'
docker exec baee9b3f82b3 sh -c 'ls -altr /insideubuntu1'


#--mount
docker service create \
    --mount 'type=volume,src=<VOLUME-NAME>,dst=<CONTAINER-PATH>,volume-driver=local,volume-opt=type=nfs,volume-opt=device=<nfs-server>:<nfs-path>,"volume-opt=o=addr=<nfs-address>,vers=4,soft,timeo=180,bg,tcp,rw"'
    --name myservice \
    <IMAGE>

#tmpfs mounts
docker run -d -it --name tmptest --tmpfs /app nginx:latest

#Multi Stage Build
Multi Stage build - https://docs.docker.com/build/building/multi-stage/
    Name Your build Stage
    Stop At Specific Build Stage
    External Image as Stage
    Previous Stage as a new Stage
    Usage of Builderkit
    Difference b/w legacy build and BuilderKit
```