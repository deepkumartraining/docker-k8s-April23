#Day 13 Notes

```
Docker compose up
Detach mode
Docker compose build

#Install Docker-compose from official docker page
https://docs.docker.com/compose/install/other/

curl -SL https://github.com/docker/compose/releases/download/v2.17.2/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
ll /usr/local/bin/docker-compose
docker-compose --version


#yaml validation

apt install yamllint -y
yamllint docker-compose.yml

Problem with upgraded docker-compose version 
--- (root) Additional property app is not allowed

(root) Additional property Version is not allowed

#Problems faced with v1.0

https://geshan.com.np/blog/2021/12/docker-postgres/

postgresql common problem with earlier versions - https://itecnote.com/tecnote/postgresql-how-to-solve-problem-with-empty-docker-entrypoint-initdb-d-postgresql-docker/

because of version compatibility, needs to downgrade to v1. < v2.0

docker-compose --version
docker-compose up

github link demo for v1.0 - https://github.com/deepkumartraining/release-example-voting-app

Docker Compose overview
https://docs.docker.com/compose/reference/

Docker-compose versioning and examples : https://docs.docker.com/compose/compose-file/compose-versioning/

docker run --name db -e POSTGRES_PASSWORD=secrect -e POSTGRES_USER=postgres postgres:14

docker run --name db -v postgres-data:/var/lib/postgresql/data -e POSTGRES_USER=password -e POSTGRES_HOST_AUTH_METHOD=trust postgres:14

docker run --name db --rm -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e PGDATA=/var/lib/postgresql/data/pgdata -v /tmp:/var/lib/postgresql/data -it postgres:14


```
