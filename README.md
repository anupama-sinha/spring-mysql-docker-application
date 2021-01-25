## Getting Started
* Creating Application JAR in Docker folder using maven plugin
> mvn clean package

> cd Docker/
* Creating Docker Image for Spring Boot App(When only Dockerfile, No docker-compose file)
> docker build -t employee-compose-img .
* Building Spring Boot & MYSQL Image together
> docker-compose up –-build

## Container Status
<pre><font color="#4E9A06"><b>anupamasinha@power-house</b></font>:<font color="#3465A4"><b>~</b></font>$ docker ps -a
CONTAINER ID   IMAGE                  COMMAND                  CREATED         STATUS         PORTS                    NAMES
a108bc6389d9   mysql:latest           &quot;docker-entrypoint.s…&quot;   4 minutes ago   Up 4 minutes   3306/tcp, 33060/tcp      docker_dbapp_1
b44d13800885   employee-compose-img   &quot;java -jar spring-my…&quot;   4 minutes ago   Up 4 minutes   0.0.0.0:8082-&gt;8082/tcp   docker_springapp_1
</pre>

* Checking Images
> docker images
* Checking Containers
> docker ps -a
* Entering inside MYSQL container to check Database & Tables
> docker exec -it 53a578923229 mysql -u root -p
* Entering inside Spring Boot App with SH Command Line of Alpine OS
> docker exec -it 0f6115e44710 sh  
* Checking MYSQL logs
> docker logs mysql

## When Linux AppArmor security module blocks container to be stopped
* Checking status for all 
> sudo apparmor_status
* Removing unknown from AppArmor(Can be used, but use only if required)
> sudo aa-remove-unknown
* Force stop Containers(Required when permission not given or use sudo mode)
> docker rm -f f93a76bb7d81

## Stopping the Containers individually
> docker container stop container-id

> docker container rm container-id

> docker container prune

## Stopping Containers at once for docker-compose
> docker-compose down

## Running MySQL as separate Docker Container without docker-compose.yaml
> docker pull mysql

> docker images

> docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mydb mysql:latest

## Debugging Initialization of MYSQL DB
* Copy MYSQL Hostname using below command
> docker inspect mysql

* Use Hostname ID in below
> mysqldump -h 1b772a9e2045 -u root -p --no-data employee > schema.sql

## References
* https://stackoverflow.com/questions/49104733/docker-on-ubuntu-16-04-error-when-killing-container
* https://stackoverflow.com/questions/29145370/how-can-i-initialize-a-mysql-database-with-schema-in-a-docker-container