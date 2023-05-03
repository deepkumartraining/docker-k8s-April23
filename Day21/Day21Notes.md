#Day 20
****************************************************************************************************
```
---Docker Swarm details

Commands executed on Docker Swarm:

Identify tokens which used for Token  
	docker swarm join-token manager -q

docker swarm join --token <RuntimeToken> 192.168.0.7:2377
docker node ls
vim docker-stack.yml
docker stack deploy -c docker-stack.yml voting-app
docker stack ls
docker stack services voting-app
docker stack services voting-app
docker stack ps voting-app
history | awk '{print substr($0, index($0, $2))}'

#---Updating with some more advance configuration
docker stack ls
docker stack ps voting-app
vim docker-stack-v1.yml
docker stack ls
docker stack deploy -c docker-stack-v1.yml voting-app
docker node ls
docker stack ls
docker stack ps voting-app
docker stack ls
docker stack ps voting-app
docker stack ps voting-app | grep shutdown
docker stack ps voting-app | grep -i shutdown
docker stack ps voting-app | grep -i running
clear
docker stack ls
docker stack ps voting-app
docker stack ps voting-app | grep -i running
history | awk '{print substr($0, index($0, $2))}'

update configuration and deploy
docker stack deploy -c docker-stack-v1.yml voting-app
docker stack ps voting-app | grep -i running

vim docker-stack-wordpress.yml
docker stack deploy -c docker-stack-wordpress.yml wordpress
docker stack ls
docker stack ps wordpress
Refer all links from ppt
```