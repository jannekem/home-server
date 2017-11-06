# Docker
Next we will install Docker and docker-compose to the server. 

## Quick intro
Docker is a containerization platform that lets you run processes in isolated environments that only contain the services that the application needs. It is somewhat similar to virtualization but without needing to install a full OS for each application.

Containers are supposed to be stateless. All persistent data should be written on mounted volumes so that the container instances can be thrown away and replaced when they need to be updated. What is great about containers is that they can be run on different platforms by just having Docker installed.

## Install Docker
Installing Docker is quite easy, just copy and paste the following command:
```
$ curl -fsSL https://get.docker.com/ | sh
```

This will download and run the installation script. After successful installation start and enable docker:
```
$ sudo systemctl start docker
$ sudo systemctl enable docker
```

Check that Docker is running:
```
$ sudo systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; enabled; vendor preset: disabled)
   Active: active (running) since Mon 2017-11-06 17:53:24 EET; 10s ago
     Docs: https://docs.docker.com
 Main PID: 3902 (dockerd)
   CGroup: /system.slice/docker.service
           ├─3902 /usr/bin/dockerd
           └─3907 docker-containerd -l unix:///var/run/docker/libcontainerd/docker-containerd.sock --metrics-interval=0 --start-timeo...
```

Add your user account to the docker group so that you can call docker without always having to prepend the command with `sudo`:
```
sudo usermod -aG docker $(whoami)
```

Log out and log back in to to activate the new settings.

No let's try a docker command:
```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

If you didn't get any error messages your docker installation is ready!

## Install docker-compose
Docker-compose is a tool that lets us write the container configurations in a text file and then automatically create the containers without having to remember all the parameters. First we install the EPEL repository:
```
$ sudo yum install epel-release
```

and python-pip:
```
$ sudo yum install python-pip
```

Then docker-compose can be installed with pip:
```
sudo pip install docker-compose
```

Upgrade all Python packages just in case:
```
sudo yum upgrade python*
```

## Testing
Now let's test that everything works, create a new directory under your home folder and move there:
```
$ mkdir hello-world
$ cd hello-world
```

Create a new file called `docker-compose.yml` with the following contents:
```
app:
  image: hello-world
```

Now we can run docker-compose and see what happens:
```
$ docker-compose up
Pulling app (hello-world:latest)...
latest: Pulling from library/hello-world
9a0669468bf7: Pull complete
Digest: sha256:0e06ef5e1945a718b02a8c319e15bae44f47039005530bc617a5d071190ed3fc
Status: Downloaded newer image for hello-world:latest
Creating helloworld_app_1 ...
Creating helloworld_app_1 ... done
Attaching to helloworld_app_1
app_1  |
app_1  | Hello from Docker!
app_1  | This message shows that your installation appears to be working correctly.
app_1  |
app_1  | To generate this message, Docker took the following steps:
app_1  |  1. The Docker client contacted the Docker daemon.
app_1  |  2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
app_1  |  3. The Docker daemon created a new container from that image which runs the
app_1  |     executable that produces the output you are currently reading.
app_1  |  4. The Docker daemon streamed that output to the Docker client, which sent it
app_1  |     to your terminal.
app_1  |
app_1  | To try something more ambitious, you can run an Ubuntu container with:
app_1  |  $ docker run -it ubuntu bash
app_1  |
app_1  | Share images, automate workflows, and more with a free Docker ID:
app_1  |  https://cloud.docker.com/
app_1  |
app_1  | For more examples and ideas, visit:
app_1  |  https://docs.docker.com/engine/userguide/
app_1  |
helloworld_app_1 exited with code 0
```

And there we have it! Now we're ready to containerize things!
