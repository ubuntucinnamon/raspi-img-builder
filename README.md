# This is elementary's build scripts (https://github.com/elementary/os), we just modified and use build-rpi.sh
---

## Building Locally

As elementary OS is built with the Debian version of `live-build`, not the Ubuntu patched version, it's easiest to build an elementary .iso in a Debian VM or container. This prevents messing up your host system too.

The following examples assume you have Docker correctly installed and set up, and that your current working directory is this repo. When done, your image will be in the `builds` folder.

### 64-bit AMD/Intel

Configure the channel in the `etc/terraform.conf` (stable, daily), then run:

```sh
docker run --privileged -i -v /proc:/proc \
    -v ${PWD}:/working_dir \
    -w /working_dir \
    debian:latest \
    /bin/bash -s etc/terraform.conf < build.sh
```

### Raspberry Pi 4

```sh
docker run --privileged -i -v /proc:/proc \
    -v ${PWD}:/working_dir \
    -w /working_dir \
    debian:unstable \
    ./build-rpi.sh
```

### Pinebook Pro

```sh
docker run --privileged -i -v /proc:/proc \
    -v ${PWD}:/working_dir \
    -w /working_dir \
    debian:unstable \
    ./build-pinebookpro.sh
```

## Further Information

More information about the concepts behind `live-build` and the technical decisions made to arrive at this set of tools to build an .iso can be found [on the wiki](https://github.com/elementary/os/wiki/Building-iso-Images).
