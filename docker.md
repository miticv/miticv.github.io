

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
name it as "ubuntu1604", with recommended settings.
In settings, under Network, go to Adapter 2, enable it, and attached to: "Hosty-only Adapter"
Under storage add downloaded ubuntu server ISO. 
Then click Start
[]
```

* Follow instruction to set it up on [pluralsight](https://app.pluralsight.com/player?course=docker-deep-dive&author=nigel-poulton&name=docker-deep-dive-m3&clip=3&mode=live)  
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

Install Docker Engine:
* Docker Client (sends command to deamon)
* Docker Demon (creates containers)
* They both get downloaded and installed as a single package
* They can talk on same machine or over network


```
sudo su                       # pain in the butt: so make sure you are admin first
cd                            # 
service docker status      # check if it is install or running
# for me it was not
uname -a                      # check kernel version (min of 3.8, even better 3.10 it is number after Linux ubanutu1604-04 #.#.#)
apt-get update                # sync packages from source
apt-get install -y docker.io  # install docker
service docker status         # check if it is install or running (now it should)

ls -l /run                    # shows that runs as root under group "docker"
                              # which means user has to be root or under "docker" group to run docker command
ls -l /run | docker.sock      # or this is above give too long result

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
docker run -it ubuntu /bin/bash
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

