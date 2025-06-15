# Spring-boot-webapp
Deplyoing spring boot with full ci/cd process using jenkins, git,maven,sonarqube,dockerhub,argocd,kubenet
![lifecycle image](https://github.com/saikamal33/Spring-boot-webapp/blob/main/sonar-pipeline.png)
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
# To automate this using a CI/CD Pipeline
Now we are going to automate the process of CI using jenkins and CD with argocd
## Steps to follow
1. we need to make sure if java 17 is present or not
~~~
sudo apt update
sudo apt install openjdk-17-jdk
~~~
2. install jenkins and add required plugins like docker pipeline(for docker slace setup), sonar scanner(for connecting to sonarqube for quality and maintanence)
~~~
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
~~~
3. launch the sonarqube server as per above instructions and generater a API key.

4. We will now add sonarqube keys(it as secret key) and dockerhub api key(this need to be as username and password) in jenkins. restart the jenkins for apply all the setup.

5. Now we just need to configure the pipeline and run the job.which will lauch a container of docker and maven image. 

6. it will install required plugins and perform the build and unit testing along with code quality testing and maintanence with maven and sonar.

7. once all the testing is once it will proceed to wraping it as an image and pusing it to dockerhub.

8. Then a shell script auto update the version for the CD deployment in Mark-10-Kubernet_repo. this will trigger an CD responce.

9. lauch a k8s cluster and deploy an argocd server with an operator. access it with username admin.
~~~
https://operatorhub.io/operator/argocd-operator
~~~
OR
for the minikube we can use this
~~~
kubectl create ns argocd
kubectl apply -f https://raw.githubusercontent.com/argoproj-labs/argocd-operator/master/manifests/install.yaml
##to get password
kubectl edit secrets argocd-initial-admin-secret -n argocd ###get password here
echo "<password>"|base64 --decode
~~~

10.configure the argocd server with the destination deployment.

we can access it using " http://<*ip address*>:9000 "

Once the pipeline is executed and the image is updated to dockerhub the CI process will end

Please find the CD Part at "https://github.com/saikamal33/Mark-10-Kubernet_repo/tree/main/kube-Mark-10.3"

## Version-2

To build the image for the base jenkins, we need to run below for the docker build.
~~~
docker build -f dock/Dockerfile -t kamalsai33/maven-docker-pre:v3 .
~~~

