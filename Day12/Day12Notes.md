Docker Network Concepts:

```

git clone https://github.com/deepkumartraining/example-voting-app.git

Voting App brief in details
Architecture Diagram
Individual component Image Build
Individual Container Build
Links

Execute in GUI channel
Reference of Voting App - https://github.com/deepkumartraining/example-voting-app.git

Need to install lightdm


Individual Command reference

#Voting App 
docker build -t voting-app .
docker run -p 5000:80 voting-app

#Redis Container start
docker run -d --name redis redis

#Voting-app start with redis reference
docker run -dp 5000:80 --link redis:redis voting-app

#Postgres container start

docker run --name db -p 5432:5432 postgres:14 #Would be failing

docker run -d --name db postgres:14 -e POSTGRES_PASSWORD=postgres
docker run --name db -dp 5432:5432 -e POSTGRES_PASSWORD=postgres postgres:14

#Worker-App container

docker build -t worker-app .
docker run -d --name worker-app --link redis:redis --link db:db worker-app

#Result-App Container 
docker build -t result-app .
docker run --name result-app -p 5001:80 --link db:db result-app

Test from GUI
enable lightdm
service lightdm status/start/restart
systemctl status lightdm

Design Walkthrough + Fitment to Docker Compose

```
