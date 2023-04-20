Docker Network Concepts:

```
Docker Networking Drivers
-- Bridge Network
-- None
-- Host Network
-- Overlay Network
-- Macvlan Network

Key Task:
	Create own bridge network
	Won't be able to create own Host network because there is only one host 
	Won't be able to create own None Network because ther is only one is allowed
	Overlay for clustering and internal communication of container in orchestration
	Macvlan is used for physical MAC address assignment

Commands:
docker network create --driver bridge --subnet 182.18.0.0/16 custom_bridgenetwork
docker network ls
docker network inspect custom_bridgenetwork
docker network inspect host
docker run -d --name custom_network --network custom_bridgenetwork deepkumartraining/node-docker

Key Pointers on Docker Networks:

-Need to explicitly mention host & None n/w during container creation
 
-All ports of the container remain hidden from the host and the host would need to use http://<container-ip>:<port> URL for HTTP communication. However, the host can use the --publish or -p flag to bind a local port with a port of the container to make things

	-- Port forwarding for publishing ports

Blog for quick reference: 
	https://itnext.io/a-beginners-guide-to-networking-in-docker-ca5b822fb935
official Docker Network link
	https://docs.docker.com/engine/reference/commandline/network/


```

#Docker Compose:

```
YAML understanding is must prior to Docker Compose, refer below links for reference:
	https://www.javatpoint.com/yaml
	https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started

Docker Compose Topics:
Overview
Need and Use Cases
Multi Container on Single Host
	Web Layer - Priority 3
	App Layer - Priority 2
	DB layer - Priority 1
Dockercompose.yml - example/explanation
links/depends on
Docker Compose Evolution/Versions/Comparisons
	https://docs.docker.com/compose/compose-v2/
	https://sreeninet.wordpress.com/2017/03/28/comparing-docker-compose-versions/

```
