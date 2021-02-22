# DockerAppStore
DockerAppStore is a AppStore full of Docker Images



** Useful Docker images **

##  System docker

###  Portainer

```
ocker volume create portainer_data

docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data. portainer/portainer

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

```

###  Ubuntu docker

** Ubuntu 18.04  **

```
docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd:1804   


docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd-python3:1804


docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd-python38:1804  

```


** 20.04 Desktop Docker with vnc **
```
docker run -d  -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc   

```






###  rancher
###  
