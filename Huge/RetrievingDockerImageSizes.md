# Retrieving Docker Image Sizes

There are two metrics that are important to consider when discussing the size of Docker images.

1. Compressed size - This is often referred to as the wire size.  This affects how fast/slow images can be pulled from a registry.  This impacts the first run experience on machines where images are not cached.
1. Uncompressed size - This is often referred to as the size on disk.  This affects how much local storage is required to support your Docker workloads.

The example commands shown below will work on Windows, MacOS, and Linux.

## How to Measure the Compressed Size

Measuring the compressed size of a Docker image depends on where the image resides - in a Docker registry or locally.

### Docker Registry Image

If the image resides in a registry, you can retrieve the size of the image without pulling it locally.  To do this you can utilize the [docker manifest command](https://docs.docker.com/engine/reference/commandline/manifest/).  At the time this article was written, the docker manifest command is in experimental and must be enabled. See [experimental docker features](https://docs.docker.com/engine/reference/commandline/cli/#experimental-features) for more information.

```console
> docker manifest inspect mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim
  {
          "schemaVersion": 2,
          "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
          "config": {
                  "mediaType": "application/vnd.docker.container.image.v1+json",
                  "size": 3957,
                  "digest": "sha256:f1017ebdaf1137beb2e39ecb7e0541418accec7b4ea28800ffd948e6c8140cf2"
          },
          "layers": [
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 27092654,
                          "digest": "sha256:000eee12ec04cc914bf96e8f5dee7767510c2aca3816af6078bd9fbe3150920c"
                  },
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 17057932,
                          "digest": "sha256:db438065d0640cd860aed4addc2db1b55714063bc11ec86f47e9b55ba26c42e1"
                  },
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 1016592,
                          "digest": "sha256:e345d85b1d3e0c9edc36dad0f7a9cc3b7155dd98024d5773fdff02eac6550b94"
                  },
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 31200951,
                          "digest": "sha256:f6285e2730365f6529506d2445a0b4f9fd8a3e76fd5f3c6c268a2946cc08ba13"
                  },
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 98,
                          "digest": "sha256:c39dcdf2780c320c6cdbf3b014a980b067c0b872ae2b9ba5dc196050116bd2c0"
                  },
                  {
                          "mediaType": "application/vnd.docker.image.rootfs.diff.tar.gzip",
                          "size": 39727,
                          "digest": "sha256:da98c9d305deab5fbfb759a98b73e88ed6461ca8e2b43468d6abc047575dae60"
                  }
          ]
  }
```

By adding up the config and layer sizes you will get the total compressed size of the image.  In this example, the compressed size of the `mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim` image is 76,411,911 bytes (74.6 MB).

### Local Image

If you are building Docker images and want to get an ideal of what the compressed size, you could push it to a registry and then utilize the technique describe in the previous Docker Registry Image section to retrieve the compressed size, but that can be wasteful and/or undesirable.  An alternative option is to use the [docker save command](https://docs.docker.com/engine/reference/commandline/save/) to get a good approximation of the compressed size.

```console
> docker save mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim -o samples-dotnetapp-buster-slim.tar
> docker run --rm -v d:\samples:/work debian:buster-slim gzip /work/samples-dotnetapp-buster-slim.tar
> ls .\samples-dotnetapp-buster-slim.tar.gz
  Directory: D:\temp\dantest

  Mode                LastWriteTime         Length Name
  ----                -------------         ------ ----
  -a----        12/6/2019   2:09 PM       73991595 samples-dotnetapp-buster-slim.tar.gz
```

You see here that the compressed size is reported as 73,991,595 bytes (72.3 MB).  Keep in mind I said this technique would get a close approximate.  This technique creates a single file versus a file per layer.  As a result the single file is slightly smaller.

## How to Measure the Uncompressed Size

To measure the uncompressed size of a Docker image, it is easiest to pull the image locally.  You can then retrieve the size of the image with the [docker inspect command](https://docs.docker.com/engine/reference/commandline/inspect/).

```console
> docker pull mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim
  dotnetapp-buster-slim: Pulling from dotnet/core/samples
  000eee12ec04: Pull complete
  db438065d064: Pull complete
  e345d85b1d3e: Pull complete
  f6285e273036: Pull complete
  c39dcdf2780c: Pull complete
  da98c9d305de: Pull complete
  Digest: sha256:1b1566f2b864c6fa0522d48f805a59b0a9e7da9eea75551d0603d8ef8159f04d
  Status: Downloaded newer image for mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim
  mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim
> docker inspect -f "{{ .Size }}" mcr.microsoft.com/dotnet/core/samples:dotnetapp-stretch
  189371468
```

You can see that the uncompressed size of the `mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim` image is 189,371,468 bytes (185 MB).

If you would like to get a more detailed breakdown of the image size by layer you can utilize the [docker history command](https://docs.docker.com/engine/reference/commandline/history/).

```console
> docker history mcr.microsoft.com/dotnet/core/samples:dotnetapp-buster-slim
  IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
  f1017ebdaf11        13 days ago         /bin/sh -c #(nop)  ENTRYPOINT ["dotnet" "dot…   0B
  <missing>           13 days ago         /bin/sh -c #(nop) COPY dir:dddbbb7806aa5feae…   102kB
  <missing>           13 days ago         /bin/sh -c #(nop) WORKDIR /app                  0B
  <missing>           13 days ago         /bin/sh -c curl -SL --output dotnet.tar.gz h…   76.4MB
  <missing>           13 days ago         /bin/sh -c #(nop)  ENV DOTNET_VERSION=3.0.1     0B
  <missing>           13 days ago         /bin/sh -c apt-get update     && apt-get ins…   2.28MB
  <missing>           13 days ago         /bin/sh -c #(nop)  ENV ASPNETCORE_URLS=http:…   0B
  <missing>           13 days ago         /bin/sh -c apt-get update     && apt-get ins…   41.3MB
  <missing>           2 weeks ago         /bin/sh -c #(nop)  CMD ["bash"]                 0B
  <missing>           2 weeks ago         /bin/sh -c #(nop) ADD file:bc8179c87c8dbb3d9…   69.2MB
```

If you don't like the truncation seen above, try using the `--no-trunc` option.
