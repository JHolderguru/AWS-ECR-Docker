#### Creating Docker Containers (ECR) AWS CLI

#### 1. ssh into the machine from cmd line

 ``` powershell
sudo yum update -y

sudo amazon-linux-extra install docker

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
 chmod 755 /root/run/run_apache.sh

EXPOSE 80

CMD /root/run_apache.sh

```

```
