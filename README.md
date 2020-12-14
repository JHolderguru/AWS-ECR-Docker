#### Creating Docker Containers (ECR) AWS CLI

#### 1. ssh into the machine from cmd line

 ``` powershell
sudo yum update -y

sudo amazon-linux-extra install docker

sudo service docker start

sudo usermod -a -G docker ec2-user

exit
```

##### ssh back into the machine

```powershell
docker --version

docker info

nano dockerfile #enter the below and save
```

FROM ubuntu:18.04

##### Install dependencies
RUN apt-get update && \
 apt-get -y install apache2

##### Install apache and write Jholderguru
RUN echo 'Hello World this is Jholderguru!'> /var/www/html/index.html                                                                                                                                             
##### Configure apache


RUN echo '. /etc/apache2/envvars' > /root/run_apache.sh && \
 echo 'mkdir -p /var/run/apache2' >> /root/run_apache.sh && \                                                                                                                                                      echo 'mkdir -p /var/lock/apache2' >> /root/run_apache.sh && \
 echo '/usr/sbin/apache2 -D FOREGROUND' >> /root/run_apache.sh && \
 chmod 755 /root/run_apache.sh

EXPOSE 80

CMD /root/run_apache.sh

```powershell
 docker build -t hello-world .

 docker images --filter reference=hello-world

 docker run -t -i -p 80:80 hello-world

```
#### copy the EC2 public ip address and that should be showing, but this has to run on our container not on the EC2.

## go to Amazon ECS console and choose the repository (under amazon ECR make syres its tthe same name and it is a pvt repository)

## create repository

## view push commands

```python

aws ecr get-login-password --region eu-west-1 | docker login --username AWS --password-stdin 5****ACCNO**1.dkr.ecr.eu-west-1.amazonaws.com

docker tag hello-world:latest 5****ACCNO**1.dkr.ecr.eu-west-1.amazonaws.com/hello-world:latest

docker push 5****ACCNO**1.dkr.ecr.eu-west-1.amazonaws.com/hello-world:latest




```
#### Go on over to Amazon ECS and create a new task for fargate and call it hello-world(same name as container) and on add container(input the image link from the ECS) port:80

#### create fargate cluster and go on task run new task

#### select myVPC and a security group which allows port 80
