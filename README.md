[![build-image](https://github.com/ryanfobel/balena-anvil/actions/workflows/main.yml/badge.svg)](https://github.com/ryanfobel/balena-anvil/actions/workflows/main.yml)

# balena-anvil

This image provides a basic [anvil] server for a [Raspberry Pi].

## Build Instructions

1. Build the docker image using [buildx and QEMU emulation](https://medium.com/@artur.klauser/building-multi-architecture-docker-images-with-buildx-27d80f7e2408):

```sh
> npx dockerfile-template -d BALENA_MACHINE_NAME=raspberrypi4-64 -f Dockerfile.template > Dockerfile.raspberrypi4-64 && \
  docker buildx build . --pull --build-arg BALENA_ARCH=aarch64 --platform=linux/arm64 --file Dockerfile.raspberrypi4-64 \
    --tag ryanfobel/raspberrypi4-64-anvil --load && rm Dockerfile.raspberrypi4-64
```

2. Push the image to docker hub
```sh
> docker push ryanfobel/raspberrypi4-64-anvil
```

**Note:** these steps are performed automatically every time a commit or tag is pushed to this repository via a [GitHub Action](https://github.com/ryanfobel/balena-anvil/blob/main/.github/workflows/main.yml).

## Use this as a base image for your own balena `Dockerfile`

Include the following line at the top of your `Dockerfile`:

```
FROM ryanfobel/raspberrypi4-64-anvil
```

[Raspberry Pi]: https://www.raspberrypi.org
[balena]: https://www.balena.io
[anvil]: https://anvil.works
