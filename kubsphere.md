#  kubsphere



```
apt update   &&   apt install curl nload  socat ipset conntrack chrony docker.io nfs-common  ceph-common glusterfs-client  -y

```


```
export KKZONE=cn  curl -sfL https://get-kk.kubesphere.io | VERSION=v1.2.1 sh -

```


```
export KKZONE=cn   ./kk create cluster --with-kubernetes v1.21.5 --with-kubesphere v3.2.1 -y

```

