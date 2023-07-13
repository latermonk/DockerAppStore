# 01 - Make a huge image
```
docker run -it ibackchina2018/ubuntu-sshd:1804 /bin/bash

sudo truncate -s +10G /var/log/lastlog

docker commit Container-ID ibackchina2018/ubuntu-sshd:huge

docker push ibackchina2018/ubuntu-sshd:huge
```

# 02 - Check the size
##  Compressed size - Size in docker registry
```
docker manifest inspect ibackchina2018/ubuntu-sshd:huge | grep "size" | awk '{s+=$2} END {print "Total size: " s/1024/1024 " MB"}'
```
got:     

```
Total size: 149.175 MB
```

## Uncompressed size  - Size in local node
```
docker pull ibackchina2018/ubuntu-sshd:huge
docker images -a |grep huge
```
got:     
```
ibackchina2018/ubuntu-sshd   huge      2bc923a8ae24   19 minutes ago   11GB
```

# 03 - Trivy Scan
```
trivy image ibackchina2018/ubuntu-sshd:huge
```

got:    

```
2023-07-13T12:32:30.691Z        INFO    Need to update DB
2023-07-13T12:32:30.692Z        INFO    DB Repository: ghcr.io/aquasecurity/trivy-db
2023-07-13T12:32:30.692Z        INFO    Downloading DB...
38.37 MiB / 38.37 MiB [-----------------------------------------------------------------------------------------------------------------------------------] 100.00% 28.32 MiB p/s 1.6s
2023-07-13T12:32:32.553Z        INFO    Vulnerability scanning is enabled
2023-07-13T12:32:32.556Z        INFO    Secret scanning is enabled
2023-07-13T12:32:32.556Z        INFO    If your scanning is slow, please try '--scanners vuln' to disable secret scanning
2023-07-13T12:32:32.556Z        INFO    Please see also https://aquasecurity.github.io/trivy/v0.43/docs/scanner/secret/#recommendation for faster secret detection

2023-07-13T12:36:34.681Z        FATAL   image scan error: scan error: scan failed: failed analysis: analyze error: pipeline error: failed to analyze layer (sha256:65bdd50ee76a485049a2d3c2e92438ac379348e7b576783669dac6f604f6241b): unable to get uncompressed layer sha256:65bdd50ee76a485049a2d3c2e92438ac379348e7b576783669dac6f604f6241b: failed to get the layer (sha256:65bdd50ee76a485049a2d3c2e92438ac379348e7b576783669dac6f604f6241b): unable to populate: unable to open: unable to export the image: Error response from daemon: write /var/lib/docker/tmp/docker-export-137505303/c99b63a4e860ec23bfd037f5d43f86d26d0221829993bf5644ed766f5e8a7c1c/layer.tar: no space left on device
```


# 04 ctr
```
ctr images  pull  docker.io/ibackchina2018/ubuntu-sshd:huge
ctr images  ls
```
got:  149.2 MiB         

```
docker.io/ibackchina2018/ubuntu-sshd:huge application/vnd.docker.distribution.manifest.v2+json sha256:2230b2c7de6baae3142fd2fe260d73458671ba1f9e16fd6023e71cfb9c1bdff6 149.2 MiB linux/amd64 -

```


# 05 -> WHY ?     ctr will display the size of the image as it is stored in the image registry
```
The ctr command is a low-level tool for interacting with the CRI (Container Runtime Interface) used by container runtimes like CRI-O, and it is designed to work with images in their compressed form. When you use the ctr images ls command to list the available images, ctr will display the size of the image as it is stored in the image registry (e.g., Docker Hub). This size represents the compressed size of the image.

This is because the images stored in the image registry are typically stored in a compressed format (such as a tarball), and are downloaded and uncompressed by the container runtime when a container is created. The uncompressed size of the image can vary depending on the specific image content and layers, and may not be known until the image is actually pulled and uncompressed by the container runtime.

While it is possible to calculate the uncompressed size of an image by downloading and uncompressing it, this can be a time-consuming process and is not necessary for most use cases. The compressed size of the image is usually a good indicator of how much disk space will be required to store the image on the local system or in the image cache of the container runtime.
```





---
Reference:       
https://gist.github.com/MichaelSimons/fb588539dcefd9b5fdf45ba04c302db6        
https://icloudnative.io/posts/getting-started-with-containerd/               



