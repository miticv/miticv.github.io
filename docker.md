

# Docker

## What are containers

VMWare: 
* physical server
* has one hypervisor
* that runs multiple VMs
* each VM has its own OS 
   * (licenses, security upgrades) 
   * (take time to boot up every time start vm)
* which run its own app

Container: (same as VM with shared OS instead)
* one physical server
* on **one OS** (docker)
* contains many secure containers
* which run its own app

AWS services Docker OS engine ubauntu
`docker run -d --name web -p 8080:8080 nigelpoulton/pluralsight-docker-ci`
8080 host to 8080 outside
`docker stop web`
`docker start web`


## What is Docker
dotCloud originaly now docker inc. (dock worker british language) (solomon hike) 
* [open source](https://github.com/docker/docker) (apache license 2.0)
* [Docker Hub](https://hub.docker.com/) is public docker registry where you can store and get images

**Open Container Initiative**

2 standards:
* Docker
* CoreOS roket rkt appc specification
* Then they created OCI - created June 2015
   * lightweight
   * Standardise 
      * Container format
      * Container runtime
   * Vendor neutral
   * Platform neutral

Private repositories:
inside corp
Docker Trusted Registry (DTR)
Quay Enterprose
etc

Docker Content Trust: 
* publisher certificate the image to be integral
 
Container Orchestration 
multi interlinked containers
* Docker Machine
  provisions host/engines
* Docker Compose
  compose multi container apps
* Docker Swarm
  schedule containers over multi docker engines

ALSO:
* Kubernetes (google)
* Mesosphere DCOS (commercial)
* Core OS fleet, etcd... 
* OpenStack Magnum 


# Setting up Docker:

* Download ubuntu iso (or CentOS)
* Download and install Oracle VM Virtual Box Manager
```
name it as "ubuntu1604"/"Centos7", with recommended settings.
In settings, under Network, go to Adapter 2, enable it, and attached to: "Hosty-only Adapter"
Under storage add downloaded ubuntu server ISO. 
Then click Start
```

Ubuntu:
```
English
Instal Ubanty Server 
location
keybord
eth default one 
name: "ubuntu1604"
"Vladimir Mitic"
user: "vlad"
pass: "password" 
no (encripting home dir) 
timezone
Partitioning method: use entire disk and set up LVM 
select partition 
write changes: yes 
use 80% of the partition just in case 
proxy none 
no automatic updates
check OpenSSH server 
GRUB boot loader install: OK

HOST KEY: right Control

```
CentOS:
```
English
Installation Destination (default)
Software Delection: GNOME Desktop
Network Hostname: enable both
root password: "password"
user creation: "vlad" "password"
```


Install Docker Engine:
* Docker Client (sends command to deamon)
* Docker Demon (creates containers)
* They both get downloaded and installed as a single package
* They can talk on same machine or over network

CentOS (has newer docker version, and better(faster) file system: devicemapper)
``` 
yum install -y docker            #install docker
systemctl status docker.service  # check if running
systemctl start docker.service   # start if not
```
Ubuntu (file system is AUFS)
```
sudo su                       # pain in the butt: so make sure you are admin first
cd                            # 
service docker status         # check if it is install or running
# for me it was not
uname -a                      # check kernel version (min of 3.8, even better 3.10 it is number after Linux ubanutu1604-04 #.#.#)
apt-get update                # sync packages from source
apt-get install -y docker.io  # install docker
service docker status         # check if it is install or running (now it should)
```

#UPDATE Docker (BACK UP before update docker)
Ubuntu
```
wget -qO- https://get.docker.com/gpg | apt-key add -
echo deb http://get.docker.com/ubuntu docker main > /etc/apt/sources.list.d/docker.list
apt-get update
apt-get install lxc-docker
docker -v
```

```
ls -l /run                    # shows that runs as root under group "docker"
                              # which means user has to be root or under "docker" group to run docker command
ls -l /run | docker.sock      # or this is above give too long result
ps -elf                       # check what is running
```
Now let try run iteractive ubuntu container with /bin/bash as start up:
```
docker run -it ubuntu /bin/bash
root@e30eb40f82d9:/# exit         # exit command exts and terminates our container!

exit                              # let also exit the root account to vlad account
```
we can add current user to the docker group so dont have to run under "sudo su":
```
cat /etc/group                #check user groups 
sudo gpasswd -a vlad docker   #command to add a user to a group
                              #long off and log on!!!!!!!! so that cache get cleared
```
now we can start this under "vlad" user account:
```
docker run -it ubuntu /bin/bash   # span ubuntu container
docker run -it centos /bin/bash   # span centos container
root@e30eb40f82d9:/# exit         # exit command exts and terminates our container!
```
docker details:
```
docker -v
docker version
docker info
```

# talk through network
clone VM.
VM1: (server)
```
netstat -tlp         # show network listeners on this box
service docker stop  # stop existing docker service
ifconfig             # get IP address (under ) in my case is:
cat /etc/hosts      # or like this
docker -H 192.168.56.50:2375 -d &
netstat -tlp
                     # ourlocal client would listen on network 
docker info          # would give erorr since local client is listening to internal socket
                     # to enable deamon to listen to both network port AND socket run:
docker -H 192.168.56.50:2375 -H unix:///var/run/docker.sock -d &
```
VM2: (client)
```
export DOCKER_HOST="tcp://192.168.56.50:2375"     # nowe ANYONE can connect to the deamon
export DOCKER_HOST=                               # to clean it up - now it is socket (only root or the docker group)

```

#Play around

```
docker run -it centos /bin/bash    #spin centos container from ubuntu
exit
docker ps -a                       # list what used to run here
ls -l /var/lib/docker/aufs/diff/   # lists all 
ls -l /var/lib/docker/aufs/diff/HASH   # lists all 
                                   # you can view files inside container!!
docker start HASH
docker attach HASH                 # you are now inside container same as starting it
                                   

```

#DOCKER components

Docker engine     = shipping yard  (aka Docker Daemon, Docker runtime)
Docker images     = manifests
Docker containers = shipping containers

##Docker Engine
Installing it provides environment infrastructure.
Can run on laptop, cloud, servers, vms etc.

##Docker Images
List everything in container and how to build it.
To launch container we need an image.
```
docker run -it fedora /bin/bash   # we are getting fedore image from docker hub
docker pull fedora                # download newest image
docker pull -a fedora             # download all fedora images
docker pull -a coreos/etcd        # download all coreos/etcd images
docker images fedora              # list all local fedora images
docker images --tree              # shows hierarchy
docker ps                         # list of containers running
docker ps -a                      # list of containers running and ran before
```
They are stored under: /var/lib/docker/<storage driver> (eufs or )
ls -l /var/lib/docker/aufs/layers    # can walk down the tree of layers of the image structure
ls -l /var/lib/docker/aufs/diff/     # lists all 
ls -l /var/lib/docker/aufs/diff/HASH # lists all directory structure under that layer

Images are layered (example) done by **union mounts**:
- bootfs (short lived lightweight starting container)
- ubuntu (base) UUID abc
- nginx  (web)  UUID def
- updates       UUID ghi (higher levels always win if conflicts)
- writeable layer  :only one that is writeable! when running if we change anything it is written in there!
 

##Docker Containers
Container is running instance of the image.
*************
One process per container! If that process terminate = container will stop running too
We CAN run more than one, but against simplicity, check:
phusion/baseimage  - it is ubuntu with full multi process feel
Inside container there is PID1 (and others) and outside you dont see PID1

We start container (not boot container) since container is a process running under docker host.
```
docker run -it ubuntu /etc/bash                          # to lunch container
###########################################Ctrl+P+Q to exit without terminating it
docker stop HASH          
docker start HASH   
docker restart HASH 
docker attach HASH  (to PID 1 aka init)(all processes are child of this PID)        

docker kill -s <signal>

docker run -d ubuntu16.04 /etc/bash -c "ping 8.8.8.8 -c 30"   # detached in background
docker ps
docker top HASH  # list processes within that container 

docker run --cpu-shares=256                     #
docker run memory=1g                            #
docker inspect HASH
docker attach HASH

docker info            # how many containers and images we are hosting
ls -l /var/lib/docker/containers # will list all the containers
docker rm HASH         # delete container!!! (not running one, has to stop it first)
docker rm -f HASH      # with force!!

alias dps="docker ps" # put it in your bash file to load on starting

```


##Docker Registries and Repos

Registry is https://hub.docker.com/
Repo for Fedora, Ubuntu, CentOS, Coreos, radial/nginx
http://registry.docker.com

## copying images
```
docker run ubuntu /bin/bash -c "echo 'cool content'" > /tmp/cool-file
docker ps -a
docker commit HASH fridge    
docker images                # now this is the latest
docker history fridge        # show command used to create image
docker save -o /tmp/fridge.tar fridge   # copying fridge image (.tar is optional)
ls -lh /tmp/fridge.tar
```
lets copy it to centos
```
tar -tf /tmp/fridge.tar      # look under tar structure 
# for each layer we would have:
#HASH/
#HASH/VERSION/
#HASH/json
#HASH/layer.tar

docker load -i /tmp/fridge.tar
docker run -it fridge /bin/bash
```
so you can have one base image and 100s containers on top of it



#Low level info
```
docker ps
docker inspect HASH    # NetworkingSettings.IPAddress

docker inspect HASH | grep Pid
# instead of attach:
nsenter -m -u -n -p -i -t 1293 /bin/bash  #mount name space, utf, network, process, ipc, target pid
# when exit it is still running
#or simplier way:
docker_enter HASH 

docker exec -it HASH /bin/bash  #start new terminal
docker run -v /usr/local/bin:/target vmitic/nsenter  # quickest way to install nsenter. WOuld copy nsenter container to user start command


```

## building from Dockerfile
instead of docker commit command
everything beneath Dockerfile root folder structure get included in the build!!

```
# comment line

```

