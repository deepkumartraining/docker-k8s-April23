#Docker commands executed on 17th April 23

```
docker build --tag java-docker .
docker images
docker tag java-docker:latest java-docker:v1.0.0
docker images
docker rmi java-docker:v1.0.0
docker images
docker images
docker run java-docker
docker run --publish 8080:8080 java-docker
docker ps
docker images
cd node-docker/
cat .dockerignore
docker images
docker images
docker container ls
docker stop b8e0dbb6cb68
docker ps
docker images
docker run 184efd5b37ed
docker ps
docker ps -a
docker rm 0a5763ee7f3d b8e0dbb6cb68 2c9ac4f05c31 75bdc3804443 3491e89c3c8f 71a77b794cbb
docker ps -a
docker images
docker run --publish 8000:8000 184efd5b37ed
docker run --name dockerpoc --publish 8000:8000 184efd5b37ed
docker ps
docker images
docker images
history | grep docker
docker images
docker run --name javadockerpoc --publish 8080:8080 c309d4cd9f32
docker images
git clone https://github.com/docker/getting-started.git
docker build -t getting-started .
docker images
docker run -dp 3000:3000 getting-started
docker ps
docker stop 2b62cbb77b7a b4545389c838
docker ps
cd node-docker/
docker ps
docker ps
docker ps
docker images
docker container ls
docker run -dp 3000:3000 getting-started
docker ps
docker images
docker rmi getting-started
docker build --tag deepkumartraining/getting-started:latest .
docker images
docker push deepkumartraining/getting-started:latest
docker images
docker run -dp 8000:8000 dbfa264e80d5 --name node-dockerpoc
docker run -dp 8000:8000 dbfa264e80d5
docker ps
docker ps
docker inspect bfe354385482
docker log bfe354385482
docker logs
adduser dockerpoc
groups dockerpoc
usermod -aG sudo dockerpoc
su dockerpoc
docker ps
docker stop e8df5c2795d3
docker images
docker rmi 09ad651a3209
docker ps -a
docker rm e8df5c2795d3 2b62cbb77b7a dca92d777083 d79b8c1ac29f
docker ps -a
docker images
docker rmi 09ad651a3209
docker build -t getting-started .
docker run -dp 3000:3000 getting-started
docker images
docker tag deepkumartraing/node-docker:v.1.0.0 deepkumartraing/node-docker:latest
docker images
docker push deepkumartraing/node-docker:latest
docker images
docker rmi 184efd5b37ed
docker images
docker rmi 184efd5b37ed
docker ps -a
docker ps -a
docker ps -a
docker stop 6c646e359290
docker stop b4545389c838 cc817cc16f04
docker ps -a
docker rm cc817cc16f04 b4545389c838 6c646e359290
docker ps -a
docker images
docker rmi 184efd5b37ed
docker rmi --force 184efd5b37ed
docker rmi --force 184efd5b37ed
docker images
docker image
docker images
docker push java-docker
docker images
cd node-docker/
docker build --name dockerpocnodejs --tag deepkumartraining/node-docker:latest .
docker build --tag deepkumartraining/node-docker:latest .
docker imagers
docker images
docker push deepkumartraining/node-docker
docker images
docker rmi java-docker
docker images
docker build --tag deepkumartraining/java-docker:latest .
docker images
docker push deepkumartraining/java-docker:latest
docker ps
docker logs bfe354385482
docker logs bfe354385482 --follow
docker logs --since 1m bfe354385482
docker logs --since 100m bfe354385482
docker logs --tail 10 bfe354385482
docker logs --tail 10 bfe354385482
history | grep docker
history | grep docker
history | grep docker
docker volume ls
history | grep docker
docker ps
docker volume ls
docker volume inspect
docker volume inspect dockerpoc
history | grep docker | awk '{print substr($0, index($0, $3))}'
history | grep docker | awk '{print substr($0, index($0, $4))}'
docker container ls
docker stop dbfa264e80d5
docker container stop dbfa264e80d5
docker ps
docker stop bfe354385482
docker ps
docker images
cd node-docker/
cd /var/lib/docker/volumes/dockerpoc/
docker volume inspect dockerpoc
docker volume ls
docker volume ls
docker volume ls
docker compose
docker compose version
docker volume create dockerpoc
docker volume ls
docker volume inspect dockerpoc
docker images
docker run -it -v dockerpoc:/insidecontainer --name volumepoc 08d22c0ceb15
history | grep docker
history | grep docker | awk '{print substr($0, index($0, $4))}'
```