

# Start zookeeper

(commands are store in `/usr/bin`)
`docker pull confluentinc/cp-zookeeper`   
`docker image inspect confluentinc/cp-zookeeper` (check version)
```powershell
docker run -it confluentinc/cp-zookeeper bash
# zookeeper-server-start /etc/kafka/zookeeper.properties
```

# Start kafka

`docker pull confluentinc/cp-kafka`
`docker image inspect confluentinc/cp-kafka` (check version)
```powershell
docker run -it confluentinc/cp-kafka bash
# cd /usr/bin
# kafka-server-start
```
