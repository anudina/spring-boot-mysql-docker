# spring-boot-docker-mysql
Demo Spring Boot application running inside docker container linked with MySQL container.


Docker commands
-----------------------------------------
1. To pull an image from docker hub
   docker pull <image-name> 
   Eg: 
	C:\Users\anudi\git\spring-boot-docker-mysql>docker pull anudinaorg/docker-mysql
	Using default tag: latest
	latest: Pulling from anudinaorg/docker-mysql
	Digest: sha256:5e2ec5964847dd78c83410f228325a462a3bfd796b6133b2bdd590b71721fea6
	Status: Image is up to date for anudinaorg/docker-mysql:latest
2. To run a docker container
   docker run --name docker-mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=demo -e MYSQL_USER=demo_user -e MYSQL_PASSWORD=demo_pass -p 3333:3306 -d mysql:5.7
   --name running instance name 
   -p forward port where 3306 port has been forwareded to 3333
3. do any change with container like adding tables or creating db etc
4. commit the changes
   docker commit 83dad1b4c6b4<Container-Id>
5. push the image to hub
    docker push anudinaorg/docker-mysql
    


## How to run it with Docker
Assume you already have Docker installed. See https://docs.docker.com/installation/.

First, clone the project and build locally:

~~~
git clone https://github.com/jiwhiz/spring-boot-docker-mysql.git
cd spring-boot-docker-mysql
mvn clean package docker:build
~~~

Run MySQL 5.6 in Docker container:

~~~
docker run --name demo-mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=demo -e MYSQL_USER=demo_user -e MYSQL_PASSWORD=demo_pass -d mysql:5.7
~~~

Check the log to make sure the server is running OK:
~~~
docker logs demo-mysql
~~~

Run demo application in Docker container and link to demo-mysql:

~~~
docker run -p 8080:8080 --name demo-app --link demo-mysql:mysql -d anudinaorg/spring-boot-docker-mysql
~~~

You can check the log by
~~~
docker logs demo-app
~~~

Open http://localhost:8080 in browser and you should see the message. If you are using Boot2Docker in Mac OSX, 
find ip by *boot2docker ip* and replace _localhost_ to _boot2docker ip_.

