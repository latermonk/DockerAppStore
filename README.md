# DockerAppStore
DockerAppStore is a AppStore full of Docker Images


##  管理类

###  Portainer

```
docker volume create portainer_data

docker run -d -p 9000:9000 -p 8000:8000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data. portainer/portainer

docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

```

##  系统类
###  Ubuntu docker

**Ubuntu 18.04**

```
docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd:1804   


docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd-python3:1804


docker run -d -P --name test_sshd    ibackchina2018/ubuntu-sshd-python38:1804  

```


**20.04 Desktop Docker with vnc**
```
docker run -d  -p 6080:80 -p 5900:5900 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc   

```




##  数据库


###  Postgras

```
mkdir ${HOME}/postgres-data/
```


```
docker run -d --name dev-postgres -e POSTGRES_PASSWORD=Pass2020! -v ${HOME}/postgres-data/:/var/lib/postgresql/data   \
 -p 5432:5432  postgres
```



###  mysql

```
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
```



###  redis
[https://hub.docker.com/_/redis](https://hub.docker.com/_/redis)
[https://github.com/bitnami/bitnami-docker-redis](https://github.com/bitnami/bitnami-docker-redis)

```
docker run --name some-redis -d redis


docker run --name redis -e ALLOW_EMPTY_PASSWORD=yes bitnami/redis:latest

```

##  下载工具

###  Aria2 + AriaNg + Filebrowser

https://github.com/wahyd4/aria2-ariang-docker

```
docker run -d --name aria2-ui -p 80:80 wahyd4/aria2-ui
```






