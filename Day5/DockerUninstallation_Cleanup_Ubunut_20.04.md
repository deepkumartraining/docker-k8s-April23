
First Approach : -

Removal of Docker installation module, in case module selected during ubuntu 20.04_LTS installation

snap remove docker
snap remove --purge docker

*****************************************************************************************************
Second Approach : -

Individual Docker component uninstallation

Step 1:

	dpkg -l | grep -i docker
To identify what installed repackage you have:

Step 2:

	sudo apt-get purge -y docker-engine docker docker.io docker-ce docker-ce-cli docker-compose-plugin
	sudo apt-get autoremove -y --purge docker-engine docker docker.io docker-ce docker-compose-plugin

The above commands will not remove images, containers, volumes, or user created configuration files on your host. If you wish to delete all images, containers, and volumes run the following commands:

Step 3:

	sudo rm -rf /var/lib/docker /etc/docker
	sudo rm -rf /etc/apparmor.d/docker
	sudo groupdel docker
	sudo rm -rf /var/run/docker.sock
	sudo rm -rf /usr/local/bin/docker-compose
	sudo rm -rf /etc/docker
	sudo apt-get purge docker-ce-cli
	sudo rm -rf ~/.docker


Once you removed Docker from the system completely, reboot your OS for complete impact.
