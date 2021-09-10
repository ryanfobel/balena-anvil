[![build-image](https://github.com/ryanfobel/balena-anvil/actions/workflows/main.yml/badge.svg)](https://github.com/ryanfobel/balena-anvil/actions/workflows/main.yml)

# balena-anvil

This image provides a basic [anvil] server for a [Raspberry Pi].

## Build Instructions

1. Build the docker image on the RPi at the given IP address

```sh
>balena build -a balena-anvil -h 192.168.0.114 -p 2375 .
```

2. List the images on the Pi

```sh
>ssh root@192.168.0.114 -p 22222 balena-engine image ls

REPOSITORY                                                       TAG                      IMAGE ID            CREATED             SIZE
balena-anvil_main                                                latest                   67ad19d687a5        2 minutes ago       1.1GB
```

3. Save the docker image `balena-anvil_main` on the pi and stream/import it into the docker service running on the laptop/desktop.

```sh
>ssh root@192.168.0.114 -p 22222 balena-engine save balena-anvil_main | docker load

>docker image ls
REPOSITORY                        TAG       IMAGE ID       CREATED       SIZE
balena-anvil_main                 latest    0e4e4314354f   2 hours ago   1.62GB
```

4. Tag the image with the proper username/image name for docker hub.
```sh
>docker tag balena-anvil_main ryanfobel/raspberrypi4-64-anvil
>docker image ls
REPOSITORY                        TAG       IMAGE ID       CREATED       SIZE
ryanfobel/raspberrypi4-64-anvil   latest    0e4e4314354f   2 hours ago   1.62GB
balena-anvil_main                 latest    0e4e4314354f   2 hours ago   1.62GB
```

5. Push the image to docker hub
```sh
>docker push ryanfobel/raspberrypi4-64-anvil
```

## Use this as a base image for your own balena `Dockerfile`

Include the following line at the top of your `Dockerfile`:

```
FROM ryanfobel/raspberrypi4-64-anvil
```

[Raspberry Pi]: https://www.raspberrypi.org
[balena]: https://www.balena.io
[anvil]: https://anvil.works
