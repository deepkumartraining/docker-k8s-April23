#Day 18
****************************************************************************************************
```
#Configure Host Only Adapter

Enable second network adapter in Virtual Box 

1) Go To Machine -> Setting -> Network -> Adapter 2
	- Enable Network Adapter
	- Attached to -  Host-Only Adapter
	- Click on Advanced
		- Adapter Type - Leave for Default
		- Promiscuous Mode - Allow All
Apply setting

2) Select target VM -> Go To File -> Tools -> Network Manager -> Properties
	- Adapter - Configure Adapter Automatically
	- DHCP Server - leave it as Default

Login to VM
	- Go to - cd /etc/netplan
	- Edit yaml file - only single file available
	- provide configuration
		- enp0s8:
			dhcp: true
			
	- Execute command
		netplan apply
	- Reboot VM

Post reboot - Check for host-only-network
	- It should start with 198.162.56.XX


#Check connectivity between VMs (Nodes) Prior to Swarm Creation
	Below is my machines reference
	- from Manager node - ping 192.168.56.xx
	- From Worker Nodes - ping 192.168.56.xx

Refer video for setup - https://www.youtube.com/watch?v=PEL0e51oeaE

#Docker Swarm Commands

Initiate Docker Swarm
	docker swarm init --advertise-addr 192.168.56.102

#Docker Join commands for worker
	docker swarm join --token SWMTKN-1-<Runtime Token> 192.168.xx.xx:2377

#Docker Join commands for manager
	docker swarm join-token manager


Manager modes
	- Leader
	- Reachable - can be promoted to leader
	- Unavailable - New manager via docker swarm Join or promote your one of worker node to Manager


#Node type/mode updates
	- docker node promote node-3 node-2
	- docker node demote node-3 node-2
	- docker node update --role manager ubuntuslave (Promoting worker to be manager)
	- docker node update --role worker ubuntuslave (Demoting from Manager to Worker)
	
	
Refer all links from ppt
```