#  Docker: 
## Introduction:
 - running app in an isolated environment.
 - doesnt require mem and os like vm
 - standard for software deployment


## container: share os no need of space extra
- ```container1 continaer2 => Docker=>H.OS = > infra``` 
      	```vm1=>H.os=>hypervisor```
	`	||`
	`infrastructure`
	`	|| `
     ```vm2=>H.OS=>hypervisor``` 

##Install and run:
 - from docker website

## Docker Image:
 - image is a template, it has snapshot, contain os,software,appcode
## Container:
 - Running instance of image

``` Diagrmatic way:```
      `  run `
`Image=========>Container`

## Image installation and run:
```docker pull nginx[name]
docker images [ to see docker images ]
docker run  ImageName:Tag[ use -d to detach and run]

docker container ls [ to know more about containername and its port]
docker stop containerid/Name[to stop]
docker run -d -p 8080:80 ImageName:Tag[to map host port 8080[can be anything which is available ] to container port 80]
docker run -d -p 8080:80 -p 3000:80 nginx:latest[ multiple ports mapping]
docker start id/Name
docker rm id [to remove ]
docker rm $(docker ps -aq) [ to remove every single container]
[=] We can't remove running container directly using above command to remove it 
docker rm -f id
docker run --name nameYouWish -d -p 8080:80 nginx:latest [ to name it instead of default]
docker ps --format="ID\t{{.ID}}\nName\t{{.Name}}\n" [To display only what we need by using format] 
```
# Volumes:
allows shares data
container & filesystem=>docker area
create volume which allows sharing
Sharing between host and container:
```docker run --name webSite -v "$(pwd):/usr/share/nginx/html:ro" -d -p 8080:80 nginx
docker exec -it NameofContainer bash
Shareing between containers:
docker run --name Websiteclone --volumes-from NameOfOriginal -d -p 8081:80 nginx
```
Creating docker image:
 1. open the directory which u want to makes add into it 
 2. Create a file named Dockerfile
 3. add this lines
```	FROM nginx
		ADD . /usr/share/nginx/html  
 4. docker build --tag nameOfDirectory:latest .[current directory]
 5. docker image ls [ to check image]
 6. docker run --name webSite -d -p 8080:80 nameOfDirectory:latest 
```

Node Setup:
install npm
after installing check using node --version, npm --version

npm init ( to initilize npm modules in desired directory)
npm save --install express

Setting up node for image
 1. open the directory which u want to makes add into it 
 2. Create a file named Dockerfile
 3. add this lines
```		FROM node
		WORKDIR /app
		ADD . .
		RUN npm install
		CMD node index.js
```

Docker ignore:
1. Create file .dockerignore
starting wrting folder or files which u want to ignore.

Caching and Layers:
helps to fasten
		FROM node
		WORKDIR	/app
		`ADD package*.json /.
		RUN npm install`
		ADD . .
		RUN npm install
		CMD node index.js

Alpine:
Reduces size when we are using alpine version
		FROM node:alpine
Tags and version:
Allows you to control image version
avoids breaking changes

Creating on tags:
	`	docker tag Nameofimage:latest Nameofimage:youwishnumber `

## Registery:
 - publish you docker image
 - `docker push sherisk/name:tagname`

		
## To debug:
 `docker inspect id`
===============================================================================================================
# KUBERNETES:
 - open source container orechestration tool
 - by google
 - helps manage containerized application 
 - HIgh availability or no downtime
 - scalabitlity and high performance
 - disaster recovery 

## Architecture:
 - Master Node(atleast 1) [ have API server]
 - worker nodes[ containes different docker containers]

### Master:
 - API server [ entrypoint to k82 cluster]
 - controller manager[keep tracks of whats  happering in the cluster]
s - cheduler [ ensures pods placement]
 - Etcd[kubernets backing keycalue store, backup is made from this snapshot]

```VirtualNetwork helps all the node into one powerfull machine
		     ________________
		     |    Master    |	 
		     |--------------|		
		     | Apiserver    |
		     | Controller   |
		     | Schedular    |
		     |  Etcd        |
		     |______________|
			   _||_	
			   \  /
			    \/
         ______________________________________
        |		Virtual Network	      |
        |_____________________________________|
  			   _||_
  			   \  /
 			    \/
        _____________  _____________ _____________
       |WorkerNode1|  |WorkerNode2| |WorkerNode3|
       |___________|  |___________| |___________|

```
# Kubernetes components:
## Pod: 
 - abstration over container
 - meant to run one mainer application
 - helps to interact
 - They communicate with each other with their ip.

## Service:
 - setting permanent ip address
 - lifecycle of pod and service are not connected therefore even pod dies ip and service are saved
 - External and Internal service
 - ingress does dns forwarding 
 - also a load balancer 

## ConfigMap:
 - contain configuration data like url,database
 - we connect it to pod
 - we just adjust config map[ instead creating rep,pushing and pulling for small changes]

## Secret:
 - used to store secret dataa
 - base64 encoded format

## Volumes:
 - harddrive to pod
 - can also be from remotestorage as well with local node1 storage[worker ]

## Deployment:
 - blueprint of pods
















