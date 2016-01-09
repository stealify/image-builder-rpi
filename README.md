# image-builder-rpi [![Build Status](https://travis-ci.org/hypriot/image-builder-rpi.svg)](https://travis-ci.org/hypriot/image-builder-rpi)

This is work in progress and not yet finished.

# Setting up Docker
A `vagrant up` in the root folder of this repository sets up a Ubuntu Trusty VM with the latest Docker installed.

To use this Docker instance from your host one can use `docker-machine`.  
To set it up with your Vagrant VM execute the following command:

```bash
docker-machine create -d generic \
  --generic-ssh-user $(vagrant ssh-config | grep ' User ' | awk '{print $2}') \
  --generic-ssh-key $(vagrant ssh-config | grep IdentityFile | awk '{print $2}') \
  --generic-ip-address $(vagrant ssh-config | grep HostName | awk '{print $2}') \
  --generic-ssh-port $(vagrant ssh-config | grep Port | awk '{print $2}') \
  image-builder
```

Now set the Docker environments to this new docker machine:

```bash
eval $(docker-machine env image-builder)
```

From here just use `make` to make a new SD-Card image:

```bash
make sd-image
```
