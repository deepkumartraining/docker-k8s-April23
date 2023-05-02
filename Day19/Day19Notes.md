#Day 19
****************************************************************************************************
```
Queries:

Why we should not deploy tasks/service on manager node?
why we have more managers and less workers?
what is the market share of Docker Swarm in terms of production implementation?
what are the benefits and lesson learning from Docker Swarm Implementation?

Response on Open Queries:

Docker Share Market Share
	https://discovery.hgdata.com/product/docker-swarm

Docker Swarm Rocks: 
	https://dockerswarm.rocks/

Some more installation steps:
	https://www.aquasec.com/cloud-native-academy/docker-container/docker-swarm/
	https://www.ibm.com/docs/ru/planning-analytics/2.0.0?topic=swarm-create-docker

Docker Swarm Setup and Installation on Cloud - AWS - Instances:
	https://medium.com/analytics-vidhya/docker-swarm-creating-deploying-services-a0da071339d3


Docker VS K8S:
	https://circleci.com/blog/docker-swarm-vs-kubernetes/
	https://www.freecodecamp.org/news/kubernetes-vs-docker-swarm-what-is-the-difference/	

Some lesson learnt from Docker Swarm Implementation;
	https://www.bugsnag.com/blog/container-orchestration-with-docker-swarm-mode


Example of running services on Docker Swarm:
	https://semaphoreci.com/community/tutorials/running-applications-on-a-docker-swarm-mode-cluster
	https://www.techrepublic.com/article/how-to-deploy-service-docker-swarm-cluster/

Play with Docker Lab example
	https://dockerlabs.collabnix.com/intermediate/workshop/getting-started-with-swarm.html

Docker Lab:
	https://labs.play-with-docker.com/p/ch7ipgae69v00096ja8g#ch7ipgae_ch7ipmg1k7jg0099he10

Docker Swarm Admin Guide:
	https://docs.docker.com/engine/swarm/admin_guide/#recover-from-disaster

docker service CLI reference: 
	https://docs.docker.com/engine/reference/commandline/service/

running services on docker swarm:
https://www.cloudbees.com/blog/running-services-within-docker-swarm

Commands Execute:

------------------------------Executed on Docker Lab-----------------------------

docker swarm init --advertise-addr 192.168.0.18
docker swarm join --token SWMTKN-1-3gy6m9oxuqm2nn0268umwa1p4d8flr58ucccxlmruq9htz8p1d-0twbrre6udrwhvarhvqiy3gur 192.168.0.18:2377
docker node promote node2 -- Promote to Manager
docker node demote node2 -- Demote to worker from Manager
docker node update --label-add managernode1  node1
docker node update --label-add managernode2  node2
docker node ls
docker node inspect node1
docker service create --name my_web nginx
docker service ls
docker service ps my_web
docker service rm dreamy_poitras
docker service update --replicas 5 redis
docker service create --name myredis redis
---Drain manager node
docker node update --availability drain node1
docker node update --availability drain node2
docker node inspect node1 --format "{{ .ManagerStatus.Reachability }}"
docker service update --replicas 3 --constraint node.labels!=managernode1 redis
---placement costraints
docker service update --replicas 3 --constraint-add node.role==worker redis
docker service update --replicas 3 --constraint-add node.role!=manager redis
docker service update --replicas 9 redis
docker service create --name redis --replicas 2 --publish 6379:6379 redis

Refer all links from ppt
```