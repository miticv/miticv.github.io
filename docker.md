

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








