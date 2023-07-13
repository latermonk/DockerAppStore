# make a huge image
```
docker run -it ibackchina2018/ubuntu-sshd:1804 /bin/bash

sudo truncate -s +10G /var/log/lastlog

docker commit Container-ID ibackchina2018/ubuntu-sshd:huge

docker push ibackchina2018/ubuntu-sshd:huge
```

# check the size






---
Reference:
https://gist.github.com/MichaelSimons/fb588539dcefd9b5fdf45ba04c302db6        

