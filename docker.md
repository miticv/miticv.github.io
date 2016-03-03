

# Docker

# What are containers

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


# What is Docker
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


* Download and install Oracle VM Virtual Box Manager
* Download ubuntu iso (or CentOS)
* Follow instruction to set it up on [pluralsight](https://app.pluralsight.com/player?course=docker-deep-dive&author=nigel-poulton&name=docker-deep-dive-m3&clip=3&mode=live) 
 
Install Docker:
* Docker Client (sends command to deamon)
* Docker Demon (creates containers)
* They both get downloaded and installed as a single package
* They can talk on same machine or over network


```
sudo su                       # pain in the bottom. so make sure you are admin first
cd                            # 
service docker.io status      # check if it is install or running
uname -a                      # check kernel version (min of 3.8, even better 3.10 it is number after Linux ubanutu1404-04 #.#.#)
apt-get update                # sync packages from source
apt-get install -y docker.io  # install docker
service docker.io status      # check if it is install or running (now it should)
```



