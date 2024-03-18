# Studentapp-3tier-docker
This studentapp project made in java is hosted through docker

## Getting started

# Created an EC2 instance in AWS:(Ubuntu)

# Added Security Group and add 80,8080,3306 port at inbound rules.

# Login into Instance:

Update your instance:
```shell
sudo apt update
```
Installing Docker:
```shell
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
#After installing docker in instance create an dockerfile and write the code to create docker containers and build + run those containers

To build the Docker file:
```shell
 cd repo_dir_path/
docker build Dockerfile_path # here you have to give the path.. The best practice is to go to that dir where your Dockerfile is present and type build . here . means same dir
#eg
docker build .
```
To run the Docker file:
```shell
docker run -d -p port_no docker_image_id
```
# To set-up Backend in EC2  
Run the following command to Build apache2 docker image:
```shell
docker run -d -p port_no
#eg
docker build .
docker run -d -p 8080:8080 
```
# To set-up Frontend in EC2  
Run the following command to Build httpd docker image:
```shell
docker run -d -p port_no
#eg
docker build .
docker run -d -p 80:80
```

# To set-up Database in EC2  
Run the following command to install mysql docker image:
```shell
docker run -d -p port_no -e MYSQL_ROOT_PASSWORD docker_image_name
#eg
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD='password' mysql:latest
```
Now create database and table inside the docker container:
```shell
docker exec -it docker_container_id mysql -u user_name -p password
create database database_name; #studentapp
use database database_name;
CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,
	student_name VARCHAR(100) NOT NULL,
    student_addr VARCHAR(100) NOT NULL,
	student_age VARCHAR(3) NOT NULL,
	student_qual VARCHAR(20) NOT NULL,
	student_percent VARCHAR(10) NOT NULL,
	student_year_passed VARCHAR(10) NOT NULL,
	PRIMARY KEY (student_id));
exit
```

Now you can access the studentapp through your public i.p.
