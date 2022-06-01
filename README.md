
https://www.aliyundrive.com/s/LJrcDVjkx27

# DockerAppStore
DockerAppStore is a AppStore full of Docker Images


##  管理类

###  Portainer

```

docker volume rm portainer_data
 
docker volume create portainer_data
```

```

docker run -d -p 58000:8000 -p 59000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce

```
###  Web-ssh terminal 

** web ssh terminal**
https://github.com/Jrohy/webssh    


```

docker run -d -p 50032:5032 --log-driver json-file --log-opt max-file=1 --log-opt max-size=100m --restart always --name webssh -e TZ=Asia/Shanghai ibackchina2018/webssh
```

or 
```

docker run -d -p 5032:5032 --log-driver json-file --log-opt max-file=1 --log-opt max-size=100m --restart always --name webssh -e TZ=Asia/Shanghai jrohy/webssh



```

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


```
docker run -d --name postgres-container -e TZ=UTC -p 30432:5432 -e POSTGRES_PASSWORD=My:s3Cr3t/ ubuntu/postgres:14-22.04_beta

```

https://hub.docker.com/r/ubuntu/postgres


###  mysql


```

docker run -d --name=mysql --restart=always -p 127.0.0.1:3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:5.6

docker run -d --name=mysql -p 127.0.0.1:3306:3306 -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:5.6

```

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
docker run -d -p 6379:6379  --restart=always  --name redis -e ALLOW_EMPTY_PASSWORD=yes bitnami/redis:latest

```


```
docker run --name some-redis -d redis


docker run --name redis -e ALLOW_EMPTY_PASSWORD=yes bitnami/redis:latest

```




#   IDE

https://github.com/JetBrains/projector-docker   


goland

```
docker run --name  goland  -d -p 8887:8887 -p 8989:8989   -p 8964:8964   -it registry.jetbrains.team/p/prj/containers/projector-goland 


```

##  添加golang sdk之后

```
docker run --name  goland  -d -p 58887:8887 -p 58989:8989   -p 58964:8964   -it   ibackchina2018/goland:v1  

```

#  webstorm

```
  docker run --name  webstorm  -d -p 48887:8887 -p 48080:8080  -p 48989:8989   -p 48964:8964   -it   registry.jetbrains.team/p/prj/containers/projector-webstorm

```

##  DockerHUb



```

docker run --name  webstorm  -d -p 48887:8887 -p 48080:8080  -p 48989:8989   -p 48964:8964   -it  ibackchina2018/webstorm:v1

```
