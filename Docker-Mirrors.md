#  Docker-Mirrors

##  华为云
[https://mirrors.huaweicloud.com/](https://mirrors.huaweicloud.com/)


```

sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<- 'EOF'
{
    "registry-mirrors": ["https://732afdcb1c3c4dc2b8e6954941b724bf.mirror.swr.myhuaweicloud.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker

```




# ali-cloud

```
https://cbvdx9uw.mirror.aliyuncs.com

```


