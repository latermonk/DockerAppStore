# DockerAppStore
DockerAppStore is a AppStore full of Docker Images


##  管理类

###  Portainer

```

docker volume rm portainer_data
 
docker volume create portainer_data


docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

```
###  Web-ssh terminal 

```
docker run --rm -p 3000:3000 wettyoss/wetty --ssh-host=<YOUR-IP>



docker run -d -p 3000:3000 wettyoss/wetty --ssh-host=

```

Access @  http://1.2.3.4:3000/wetty   


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



##  下载工具

###  Aria2 + AriaNg + Filebrowser

https://github.com/wahyd4/aria2-ariang-docker

```
docker run -d --name aria2-ui -p 80:80 wahyd4/aria2-ui
```
*   Aria2: [http://yourip/ui/](http://yourip/ui/)
*   FileManger: [http://yourip](http://yourip)
*   Rclone: [http://yourip/rclone](http://yourip/rclone)
*   Please use `admin`/`admin` as username and password to login for the first time, and `user`/`password` to login `Rclone` if you don't update `ARIA2_USER` and `ARIA2_PWD`



###  youtube-dl-server

https://github.com/manbearwiz/youtube-dl-server     



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



**Aother. MYSQL. **    

```
docker run --name mysql8019 -p 13306:3306 -e MYSQL_ROOT_PASSWORD=root1234 -d mysql:8.0.19

docker run -it --network host --rm mysql mysql -h127.0.0.1 -P13306 --default-character-set=utf8mb4 -uroot -p

```




###  redis
[https://hub.docker.com/_/redis](https://hub.docker.com/_/redis)
[https://github.com/bitnami/bitnami-docker-redis](https://github.com/bitnami/bitnami-docker-redis)

```
docker run --name some-redis -d redis


docker run --name redis -e ALLOW_EMPTY_PASSWORD=yes bitnami/redis:latest

```






