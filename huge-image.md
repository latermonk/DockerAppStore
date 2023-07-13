# Make a huge image
```
docker run -it ibackchina2018/ubuntu-sshd:1804 /bin/bash

sudo truncate -s +10G /var/log/lastlog

docker commit Container-ID ibackchina2018/ubuntu-sshd:huge

docker push ibackchina2018/ubuntu-sshd:huge
```

# Check the size
##  Compressed size
```
docker manifest inspect ibackchina2018/ubuntu-sshd:huge | grep "size" | awk '{s+=$2} END {print "Total size: " s/1024/1024 " MB"}'
```
got:     

```
Total size: 149.175 MB
```

## Uncompressed size  
```
docker pull ibackchina2018/ubuntu-sshd:huge
docker images -a |grep huge
```
got:     
```
ibackchina2018/ubuntu-sshd   huge      2bc923a8ae24   19 minutes ago   11GB
```







---
Reference:       
https://gist.github.com/MichaelSimons/fb588539dcefd9b5fdf45ba04c302db6        

