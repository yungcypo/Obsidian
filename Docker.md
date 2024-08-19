# Docker
[Docker](https://www.docker.com/) is a platform for building, running and shipping applications  
I'm learning from [Docker tutorial for Beginners](https://www.youtube.com/watch?v=pTFZFxd4hOI) by Programming with Mosh on YouTube  

If your code works on one machine, it can work on any other machine, so you don't have to say *"It works on my machine"*    
With Docker, you can "pack" your application with everything it needs and run it on any machine with Docker  
For example, you are developing a website with Node 14 and MongoDB 4, you can make a package and run this package on any machine with Docker  
Docker will automatically install and run all the dependencies in isolated environment called *container*  
This is also helpful if you are running multiple applications with different versions on software on one machine, now you can run them side by side    
Another benefit is, when you are finished using/developing one application, you can remove it with all it's dependencies in one go  

Docker helps consistently build, run and ship applications  

## Virtual Machines vs. Containers  
You might think that *container* is similar to a *virtual machine (VM)*   

The main difference is that VM needs a full operating system to run  
It makes VM slower to load and more intensive on resources  

Container uses the operating system of host  
This makes containers more lightweight  

# Installation  
`yay -S docker` or go to [their website](https://docs.docker.com/get-docker/) and download it from there  

Check if everything is correct with `docker version`  

You might get some errors, run these commands   
```shell
sudo systemctl enable docker  
sudo systemctl start docker  
sudo usermod -aG docker ${USER}  
```  
> Note: You might need to log out and log back in to apply changes  

Now, after running `docker version` you want to see something like this (both client and server running)  
```  
Client:
 Version:           27.1.1
 API version:       1.46
 Go version:        go1.22.5
 Git commit:        63125853e3
 Built:             Thu Jul 25 17:06:22 2024
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
  Version:          27.1.1
  API version:      1.46 (minimum version 1.24)
  Go version:       go1.22.5
  Git commit:       cc13f95251
  Built:            Thu Jul 25 17:06:22 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.7.20
  GitCommit:        8fc6bcff51318944179630522a095cc9dbf9f353.m
 runc:
  Version:          1.1.13
  GitCommit:        
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

# Development Workflow
Imagine you have an application  
Now you need to *"dockerize"* it - add *Dockerfile* to it  

Dockerfile is a plain text file which provides information to Docker   
Now, Docker can make an *Image* from the app  

Image contains everything our application need to run:   
- Cut-down OS   
- Runtime environment (Node for example)  
- Application files  
- Third-party libraries  
- Environment variables  

Once we have an Image, we tell Docker to run a container using this Image  

Container is a special type of process  
It has it's own file system, which is provided by the Image  

Once you have an Image, you can push it to Docker Registry - [Docker Hub](https://hub.docker.com/) (like GitHub to Git) so everyone else can use it  
Docker Hub is a registry for Docker images  

## Dockerfile
Once you have starting developing your application, you need to add `Dockerfile`    
Just add a new file called `Dockerfile`, the name has to be the same as you see there, no extension  
Now we will be typing code into the `Dockerfile`

First, you need to specify what container you are starting on, like a base container, like what container will you inherit from   
You can do this with `FROM` command  
```dockerfile
FROM linux
```

Now if you have JavaScript application, you are most likely using Node  
In this case, you don't need to start from `linux`, you can start from `node`, which is already based on `linux`   
```dockerfile
FROM node
```

You can specify what Linux distribution you want to use  
For example Alpine Linux is very small *(5MB !)*, so it might be a good consideration for Docker container (small image size, even faster load times)   
```dockerfile
FROM node:alpine
```

If you want to explore more containers, go to [hub.docker.com](https://hub.docker.com/)

Now we need to copy our application files with the `COPY` command  
With following command, we will copy all the files from our program into Image's `/app` directory  
The Image has a file system, and we will create a directory called `app` inside this filesytem
```dockerfile
FROM node:alpine
COPY . /app
```

Finally, you can use `CMD` function to run commands on Image  
```dockerfile
FROM node:alpine
COPY . /app
CMD node /app/index.js
```

If you don't want to use the absolute path for files, you can set work directory with `WORKDIR` command  
It's basically like `cd` on Linux   
```dockerfile
FROM node:alpine
COPY . /app
WORKDIR /app
CMD node index.js
```

## Building Docker Image  
Now, once you are done, you can go to terminal to Build Docker Image   
You can do this with `docker build` command, which looks like this:    
```shell
docker build -t <tag> <dockerfile_location>   
```

Tag is like a name for the Docker Image, which will identify it. It is set with `-t` flag  
At the end, you need to add location to the `Dockerfile`. Since we are in the same directory as the `Dockerfile`, you can just add `.`   
Whole command could look something like this   
```shell
docker build -t hello-docker .
```

You might think that you will see a new file/files after building Docker Image, but it's not the case  
You project will look exactly the same as before  
How Docker stores files is complex and not needed to understand right now  

To see all Docker Images on your computer, type one of following command in your terminal  
```shell
docker images
docker image ls
```  

You can see `Repository`, `Tag`, `Image ID`, `Created` and `Size` there  

## Running Docker Image
```shell
docker run <name>
```  

Make sure to replace `<name>` with the actual name of Docker Repository, for example   
```shell
docker run hello-docker 
```  

After entering this command, your application should run  

## Publish Docker Image

## Pull Docker Image
When you want to take Docker Image to new machine, it's as simple as this  
```shell
docker pull <name>
```   

...where `<name>` is the name of Repository on Docker Hub you created previously, for example   

```shell
docker pull cyprich/website  
```  

You can verify and run the container with commands you have learned before    
```shell
docker images
docker run cyprich/website  
				```  

> Note: You can try it online with sites like [Play with Docker](https://labs.play-with-docker.com/), which allows you to make a virtual machine    

# Running Linux  
You can search for Ubuntu on [Docker Hub](https://hub.docker.com/)  
You can run it with following command  
```shell
docker run ubuntu
```

If you already have `ubuntu` image on your system, it will run, otherwise it will download it  

> Note: On the official site, there is `docker pull ubuntu` command, but this is like a shortcut  

By typing following command, you can list Docker processes on your system  
```shell
docker ps
```

You will (probably) not see anything right now, because the container that we ran stopped immediately  
To list all Docker processes, type the following command   
```shell
docker ps -a
```

Now you can see that you have "Exited" Ubuntu container  

To run container interactively, you can run this command  
```shell
docker run -it <name>
```

...so in this case it will be...  
```shell
docker run -it ubuntu
```  

Now you are running Ubuntu  
You can enter commands and whatever  
