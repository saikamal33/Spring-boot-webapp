# Spring-boot-webapp
Deplyoing spring boot with full ci/cd process using jenkins, git,maven,sonarqube,dockerhub,argocd,kubenet
![lifecycle image](https://github.com/saikamal33/Spring-boot-webapp/blob/main/spring-boot.png)
## Execute the application locally and access it using your browser
we need to clone this repo and change into this proj root file
~~~
git clone https://github.com/saikamal33/Spring-boot-webapp
cd ci_cd_full_pipe-Proj-3
~~~

To execute the maven
~~~
mvn clean package
~~~
To deploy in docker
~~~
docker build -t ultimate-cicd-pipeline:v1 .
~~~
~~~
docker run -d -p 8010:8080 -t ultimate-cicd-pipeline:v1
~~~
we can access this using "http://localhost:8010" apt install unzip


## Sonarqube server locally
We can install sonarqube in the server using below steps
~~~
System Requirements
Java 17+ (Oracle JDK, OpenJDK, or AdoptOpenJDK)
Hardware Recommendations:
   Minimum 2 GB RAM
   2 CPU cores
sudo apt update && sudo apt install unzip -y
adduser sonarqube
su - sonarqube
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
unzip *
chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
cd sonarqube-9.4.0.54424/bin/linux-x86-64/
./sonar.sh start
~~~
we can access it using " http://<*ip address*>:9000 "

Once the pipeline is executed and the image is updated to dockerhub the CI process will end

Please find the CD Part at "https://github.com/saikamal33/Mark-10-Kubernet_repo/tree/main/kube-Mark-10.3"

