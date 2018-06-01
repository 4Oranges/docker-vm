# Dubuntu

[![Build Status](https://travis-ci.org/4Oranges/Dubuntu.svg)](https://travis-ci.org/4Oranges/Dubuntu) [![Docker Stars](https://img.shields.io/docker/stars/4oranges/dubuntu.svg)](https://hub.docker.com/r/4oranges/dubuntu/) [![Docker Pulls](https://img.shields.io/docker/pulls/4oranges/dubuntu.svg)](https://hub.docker.com/r/4oranges/dubuntu/) 

A handy ubuntu enviroment in docker.

## What's Inside
- Ubuntu bionic (18.04LTS)
- basic network utils like telnet, ping, etc.
- lsb
- ssh server
- oh my zsh
- docker engine (docker in docker)
- python2 and python3
- ...


## Installation
```bash
# Install command line tools to /usr/local/bin
./install
```

## Command Line Reference
### `dubuntu-pull`
pull the image from docker hub

### `dubuntu-build`
build the image locally

### `dubuntu-recreate`
recreate / restart Dubuntu

### `dubuntu-attach`
attatch to running Dubuntu

### start / stop container
use `docker start dubuntu` and `docker stop dubuntu`

## Recipes
### Change Docker Settings
Any docker related settings are defined in `docker-compose.yaml`. Simply add port mapping / volumes as you wish.

### Connect to Dubuntu via SSH
```bash
# make sure you are in side the Dubuntu directory
# And port 22 is mapped in `docker-compose.yaml`
cat ~/.ssh/id_rsa.pub >> shared/authorized_keys
docker stop dubuntu && docker start dubuntu
ssh root@localhost	# or somewhere you defined
```

## Configurations
Priority: ENV > Conf files

### Config via Environment
- APT_SOURCE=< tuna | official >
- APT_PACKAGES=< additional package list seprated by space >

### Configuration Files
Put files listed below inside `/shared` to override corresponding files inside the container.
- `sources.list`: override `/etc/apt/sources.list` in VM.
- `resolv.conf`: override `/etc/resolv.conf` in VM.
- `authorized_keys`: override `/root/.ssh/authorized_keys` in VM.
- `dircolors`: override color mapping of the inside console.
- `profile`: addition `zsh` startup source script.
- `ssh_host_rsa_key`: override /etc/ssh/ssh_host_rsa_key, the host rsa key. Will be generated automatically if not exists.
- `zsh_history`: override `/root/.zsh_history` in VM.

## Know Issues
- Because Docker for Mac is running in a real virtual machine([hyperkit](https://github.com/moby/hyperkit)), after a long sleep, the hyperkit may have its clock drift, which may cause the ssh connection fails. restart the container to workaround.
- `/shared/zsh_history` currently not working

## TODO
- Setup node.js dev environment
- Basic web server environment

