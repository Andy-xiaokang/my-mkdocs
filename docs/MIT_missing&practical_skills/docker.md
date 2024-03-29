# Docker  
## docker commands
`run`-start a container
```
docker run nginx
```  
`ps`-list containers
```
docker ps  #list all running containers
```
```
docker ps -a  #list all containers
```
`stop`-stop a container
```
docker ps
docker stop silly_sammet
docker ps -a
```
`rm`-remove a container
```
docker rm silly_sammet
docker ps -a
```
`images`-list images
```
docker images
```
`rmi`-remove images
```
docker rmi nginx
```
`pull`-download an image
```
docker run nginx   # if can't find locally then pull from the repository
docker pull nginx
```
`exec`-execute a command
```
docker exec container_name cat /etc/hosts
```
`run`-attach and detach
```
docker run kodekloud/simple-webapp
docker run -d kodekloud/simple-webapp
docker attach sha_numbers
```

## docker run
`run`-tag
```
docker run redis
docker run redis:4.0  #image:tag
```
`run`-port mapping
```
docker run -p 80:5000 kodekloud/simple-webapp  #  host_port:container_port
```   
`run`-volume mapping
```
docker run -v /opt/datadir:/var/lib/mysql mysql  # docker_host_address:container_address
```
`inspect` container
```
docker inspect container_name
```
container logs
```
docker logs blissful
```
## docker environment variables
set environment variables
```
docker run -e APP_COLOR=blue simple-webapp-color
docker run -e APP_COLOR=green simple-webapp-color
docker run -e APP_COLOR=pink simple-webapp-color
```
inspect environment variables
```
docker inspect blissful_hopper
```
## docker images
how to create my own image  
```title='Dockerfile'
FROM Ubuntu  # 1.OS-Ubuntu

RUN apt-get update  # 2.Update apt repo
RUN apt-get install python # 3. Install dependencies using apt

RUN pip install flask  # 4. Install python dependencies using pip
RUN pip install flask-mysql

COPY . /opt/source-code  # 5. copy source code to /opt folder

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run  # 6. run the web server using flask command
```
```
docker build Dockerfile -t mmumshad/my-custom-app
docker push mmumshad/my-custom-app   # docker registry
```
![20230626135744](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230626135744.png)

## Docker networking
![20230630235415](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230630235415.png)  
![截屏2023-06-30 23.54.59](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-06-30%2023.54.59.png)  
![20230630235604](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230630235604.png)  
![20230630235626](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230630235626.png)  

## Docker storage
![20230630235838](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230630235838.png)  
![20230630235908](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230630235908.png)  
![20230701000004](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230701000004.png)  
![20230701000034](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230701000034.png)  

## Docker compose
![20230701000513](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230701000513.png)  
![20230701000605](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/20230701000605.png)  

## Docker registry
![截屏2023-07-01 00.06.36](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-07-01%2000.06.36.png)