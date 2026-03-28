# jenkins-docker-pipeline

Commands to run Jenkins inside a docker

Blue Ocean: New UI which heps to graphically create, visualise and diagonise CI/CD pipeline

Step 1: Build the Jenkins BlueOcean Docker Image from the dockerfile
  docker build -t myjenkins-blueocean:2.414.2 .

Step 2: Create the network 'jenkins'
  docker network create jenkins

Step 3: Run the Container
  MacOS / Linux
    docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.556

  
We have jenkins running in port 8080 and we need a password to unlock the Jenkins, use the below password to start using Jenkins

Password:
  docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword


To start the same container from the second time:
docker start jenkins-blueocean

To go to the bash terminal --> to view the file system
docker exec -it jenkins-blueocean bash

1. pwd  --> print working directory
2. check for volume location and do a cd
3. cd workspace
4. cd job name