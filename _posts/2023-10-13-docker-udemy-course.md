---
layout: post
title: Docker Udemy Course
date: 2023-10-13 18:16 -0500
categories: [Containers, Docker, Kubernetes]
image:
  path: /2023-10-13-docker-udemy-course/profile.png
---

- [Course curriculium](#course-curriculium)
- [Code for this course](#code-for-this-course)
- [Miscellaneous](#miscellaneous)
  - [format option](#format-option)
  - [filter option](#filter-option)
- [Section 1](#section-1)
  - [Build, Ship, Run](#build-ship-run)
  - [Docker Lab](#docker-lab)
  - [Linux concepts that Docker utilizes](#linux-concepts-that-docker-utilizes)
  - [Why docker in todays world](#why-docker-in-todays-world)
- [Section 4](#section-4)
  - [Sanity test check](#sanity-test-check)
  - [Docker cli structure](#docker-cli-structure)
  - [Image vs container](#image-vs-container)
  - [Getting a list of containers](#getting-a-list-of-containers)
  - [Creating Container from image](#creating-container-from-image)
  - [How publishing ports works](#how-publishing-ports-works)
  - [Removing Containers](#removing-containers)
  - [Getting the logs for a container](#getting-the-logs-for-a-container)
  - [Get the processes and their PIDs for a container](#get-the-processes-and-their-pids-for-a-container)
  - [What happens in when we run a container?](#what-happens-in-when-we-run-a-container)
  - [Container vs Vms](#container-vs-vms)
  - [Passing environment variables to our container](#passing-environment-variables-to-our-container)
  - [docker stats](#docker-stats)
  - [Getting a shell inside containers](#getting-a-shell-inside-containers)
  - [Docker networking](#docker-networking)
    - [Bridge network](#bridge-network)
      - [How bridge network works](#how-bridge-network-works)
      - [Multiple networks](#multiple-networks)
    - [View what port a container is listening on](#view-what-port-a-container-is-listening-on)
    - [Docker network](#docker-network)
    - [Docker network drivers](#docker-network-drivers)
    - [Docker networks DNS](#docker-networks-dns)
      - [Docker DNS Round Robin](#docker-dns-round-robin)
  - [Docker inspect](#docker-inspect)
- [Section 5 Container Images](#section-5-container-images)
  - [What is an image?](#what-is-an-image)
  - [Official and unofficial images](#official-and-unofficial-images)
  - [Image layers](#image-layers)
  - [docker history \& docker inspect](#docker-history--docker-inspect)
  - [Building an image from a dockerfile](#building-an-image-from-a-dockerfile)
  - [Ordering of the dockerfile](#ordering-of-the-dockerfile)
  - [Keywords](#keywords)
- [Section 6 Persistent Data : Volumes](#section-6-persistent-data--volumes)
  - [Volume Command](#volume-command)
  - [Bind Mounting](#bind-mounting)
  - [Bind Mounts vs Volumes](#bind-mounts-vs-volumes)
  - [docker volume create](#docker-volume-create)
- [Section 7. Docker Compose](#section-7-docker-compose)
  - [What is docker compose](#what-is-docker-compose)
  - [Docker cli tool](#docker-cli-tool)
  - [docker-compose down --rmi local -v](#docker-compose-down---rmi-local--v)
  - [docker build](#docker-build)
- [Section 8. Swarm Intro and Creating a 3-Node Swarm Cluster](#section-8-swarm-intro-and-creating-a-3-node-swarm-cluster)
  - [What is it](#what-is-it)
  - [How it works](#how-it-works)
  - [docker swarm init](#docker-swarm-init)
  - [docker node ls](#docker-node-ls)
  - [docker service ls](#docker-service-ls)
  - [docker service ps ](#docker-service-ps-)
  - [docker service](#docker-service)
  - [Say one of those containers goes down](#say-one-of-those-containers-goes-down)
  - [Overlay Multi-Host Networking](#overlay-multi-host-networking)
  - [Swarm Routing mesh](#swarm-routing-mesh)
  - [mounting volumes in swarm](#mounting-volumes-in-swarm)
  - [Stacks](#stacks)
  - [Updating a stack](#updating-a-stack)
  - [Secrets in stacks](#secrets-in-stacks)
  - [Creating the secret through the file](#creating-the-secret-through-the-file)
  - [Creating the secret by passing it through the shell](#creating-the-secret-by-passing-it-through-the-shell)
  - [Telling docker to use a secret for a docker container](#telling-docker-to-use-a-secret-for-a-docker-container)
  - [Telling docker to use secrets in a container in the docker compose file](#telling-docker-to-use-secrets-in-a-container-in-the-docker-compose-file)
  - [Secrets with stacks](#secrets-with-stacks)
- [Section 10: Swarm App Lifecycle](#section-10-swarm-app-lifecycle)
  - [Full App Lifecycle with Compose](#full-app-lifecycle-with-compose)
  - [Using the docker compose config to merge](#using-the-docker-compose-config-to-merge)
  - [Swarm Updates](#swarm-updates)
  - [Docker Healthcheck](#docker-healthcheck)
- [Section 13 The What and Why of Kubernetes](#section-13-the-what-and-why-of-kubernetes)
  - [What is Kubernetes](#what-is-kubernetes)
  - [Why Kubernetes](#why-kubernetes)
  - [Kubernetes vs Swarm](#kubernetes-vs-swarm)
- [Section 14 Kubernetes Architecture and Install](#section-14-kubernetes-architecture-and-install)
  - [Terminology](#terminology)
- [Section 15: Your first Pods](#section-15-your-first-pods)
  - [Kubectl run, create, apply](#kubectl-run-create-apply)
  - [kubectl explain](#kubectl-explain)
  - [General](#general)
  - [Deployment with kubectl](#deployment-with-kubectl)
  - [Scaling Relicasets](#scaling-relicasets)
- [Section 16. Inspecting Kubernetes Resources](#section-16-inspecting-kubernetes-resources)
  - [kubectl get ..](#kubectl-get-)
  - [kubectl describe](#kubectl-describe)
  - [Container Logs in Kubernetes](#container-logs-in-kubernetes)
- [Section 17. Exposing Kubernetes ports](#section-17-exposing-kubernetes-ports)
  - [Service Types](#service-types)
  - [Exposing Containers](#exposing-containers)
  - [Deleting Services](#deleting-services)
  - [Kubernetes DNS](#kubernetes-dns)
- [Section 18. Kubernetes Management Techniques](#section-18-kubernetes-management-techniques)
  - [Resource Generators](#resource-generators)
- [Section 19. Moving to Declarative Kubernetes YAML](#section-19-moving-to-declarative-kubernetes-yaml)
  - [apiVersion](#apiversion)
  - [Kind](#kind)
  - [spec](#spec)
  - [diff](#diff)
  - [Labels \& Label Selectors](#labels--label-selectors)
  - [Filtering the get command with  labels](#filtering-the-get-command-with--labels)


# Course curriculium
  - Getting requirements
  - Docker install
  - Container basics
  - Image basics
  - Docker networking
  - Docker Volumes
  - Docker Compose
  - Orchestration
  - Docker Swarm
  - Kubernetes (K8)
  - Swam vs K8s
  - Student Q&A
  - File Reviews
  - References Galore

# Code for this course
  - [github repo](https://github.com/bretfisher/udemy-docker-mastery)

# Miscellaneous

## format option
  - The --format options is available for a lot of docker commands like `docker container ls` and `docker image ls`
  - You can use a go template to format the output to customize it to your liking [go templates docs](https://docs.docker.com/config/formatting/)

  - `docker container ls --format {{json .}} | jq`
    - view all of the possible columns you can print out
    - pipes the output to jq to make it easier to read

  - `docker image ls --format {{.ID}}\t{{.Repository}}`
    - print out the ID and Repository information for all of the images

  - `docker image ls --format 'table {{.ID}}\t{{.Repository}}'`

  - `docker container inspect --format='{{range .NetworkSettings.Networks}}{{println .IPAddress}}{{println .MacAddress}}{{end}}' httpd`
    - print out a range of values inside of a nested json object
    - make sure to end with `{{end}}`

## filter option
  - The --filter option is available for a lot of docker commands like
  - you can either choose to use `--filter` or `-f`
  - it is in key=value format `--filter foo=bar`
  - Using the same filter multiple times is interpreted as a **logical OR** `--filter foo=bar --filter foo=mars`
  - Using a different filter is interpreted as a **logical AND** `--filter foo=bar age=25 state=Tx`


# Section 1

## Build, Ship, Run
  - ![bsr](/2023-10-13-docker-udemy-course/bsr.png)
  - The 3 steps to take non-containerized software and to containerize them

Docker Image (Build)
  - ![layers](/2023-10-13-docker-udemy-course/layers.png)
  - A docker file creates a docker image by using layers
  - `docker build`
    - the command to build the image

Docker Registry (Ship)
  - There are multilpe registries
  - how it gets those packages around
  - dockerHub is the most popular
  - just a place that that lets you store your docker image
  - `docker push`
    - Pushes docker image to the registry along with the
  - ![push](/2023-10-13-docker-udemy-course/push.png)
    - Uses a hash to make sure the user is downloading the correct docker image from the registry

Docker Run (Run)
  - Another machine can pull down the image from the registry with
  - `docker pull`
  - Then use `docker run`
    - This will create namespace for that container
  - containers cannot see what other containers are doing and their information

## Docker Lab
  - [Play with Docker](https://labs.play-with-docker.com)
  - ![Play with Docker](/2023-10-13-docker-udemy-course/play-with-docker.png)
  - His name is Moby Dock!

## Linux concepts that Docker utilizes
  - Namespaces
    - In Linux, namespaces are a feature of the kernel that provides process isolation and resource control. They allow multiple processes to run on the same system as if they had their own isolated view of the system.
  - CGroups
    -  Cgroup (Control Group) namespaces provide an isolated view of the control groups hierarchy. This allows processes to have their own resource limits and resource control settings.
  - VETH
    - In Linux, "veth" stands for "Virtual Ethernet." It is a virtual network interface pair used to connect two network namespaces. These pairs of interfaces are linked, allowing network traffic to pass between them. Veth pairs are frequently used in containerization and network virtualization to create isolated network environments for different processes, containers, or virtual machines.
  - IpTables
    - iptables is a powerful and versatile command-line tool in Linux for managing the network packet filtering rules of the Linux kernel's netfilter framework. It is used to configure, maintain, and inspect packet filtering and network address translation (NAT) rules.
  - Union Mount
    - A union mount is a type of mount in Linux that allows multiple file systems or directories to be combined or "stacked" on top of one another, creating a single virtual file system. Union mounts are particularly useful for overlaying directories, enabling you to present a unified view of multiple directories while preserving the original data.
    - When you drop into a docker container via shell we can see it looks like a linux file system with a lot less in it

## Why docker in todays world
  - 3 main areas
    - isolation
    - environments
    - speed

  - containers give you speed
    - develop faster
    - build faster
    - test faster
    - deploy faster

# Section 4

## Sanity test check
  - `docker version`
    - if you want to make sure the client and the docker engine are working
  - `docker info`
    - if you want more detailed information about the client and the docker engine

## Docker cli structure
  - old way (still works) docker COMMAND (options)
  - new way docker COMMAND SUB-COMMAND (options)

## Image vs container
  - an image is the application we want to run
  - a container is an instance of that image running as a **process**

## Getting a list of containers
  - `docker ps` or new way `docker container ls`
    - gets a list of running containers
  - `docker ps -a`
    - gets a list of all containers, **running and stopped**
  - `docker ps -aq`
    - gets a list of all containers just the container id's
  - ` docker ps -aq --filter "id=container_id" `
    - list docker containers with a certain id
  - ` docker ps -aq --filter "ancestor=nginx" `
    - list docker containers that have an image of **nginx**

## Creating Container from image
  - `docker run nginx -d`
    - run a new docker nginx container image and detach from the session

## How publishing ports works
  - `docker container run -p 8080:80  httpd`
    - we are saying the host machine is going to listen on 8080 and port forward to 80 in the docker container
    - 8080:80
    - host machine -> docker container

## Removing Containers
  - `docker rm container_id`
    - removes the container from the list of containers
  - `docker ps -aq --filter "ancestor=nginx" | xargs docker rm `
    - removes all docker images that are using the nginx image
  - `docker rm 634 123`
    - you don't have to give the entire container_id just the first couple that are unique
    - you can also remove multiple at one time

## Getting the logs for a container
  - `docker logs -f container_id`

## Get the processes and their PIDs for a container
  - `docker container top container_id`

## What happens in when we run a container?
  - example `docker run nginx`
  1. looks for image locally in image cache
  2. then looks in remote image repo (defaults to docker hub)
  3. downloads the latest version (nginx:latest)
  4. creates new container based on that image and prepares start
  5. gives it a virtual IP on a private network inside docker engine
  6. Opens up port 80 on host nad forwards to port 80 in container
  7. starts container by using the CMD in the docker file

## Container vs Vms
  - containers are just a restricted process running on the OS kernel
  - exit when process stops
  - Docker desktop uses a lightweight linux vm to run your containers

## Passing environment variables to our container
  - a lot of times a container will allow or even mandate you pass environment variables to the container
  - this is done with `-e` or `--env`
  - `docker run -e MYSQL_ROOT_PASSWORD=P@ssw0rd1 mysql`

## docker stats
  - `docker stats nginx`
    - look at real time stats for a container

  - `docker stats`
    - real time stats for all running containers

## Getting a shell inside containers
  - `docker run -it nginx bash`
    - start a **new container** interactively
  - `docker container exec -it nginx bash`
    - get shell inside **existing container**

## Docker networking
  - each container connected to a private virtual network "bridge"
  - each virtual network routes through NAT firewal on host IP
  - all containers on a virtual network can talk to each other without -p
  - best practice is to create a new virtual network for each app
    - network "my_web_app" for mysql and php/apache containers
    - network "my_api" for mongo and nodejs containers
  - we can attach containers to more than one network or none if we wanted
  - skip virtual networks and use host IP (--net=host)
  - "Batteries included, but removable"
    - docker motto
    -  defaults work well in many cases, but easy to swap out parts to customize it
  - typically starts defaults to 172.17 for the bridge network

### Bridge network
  - When you create a new container without explicitly specifying a custom network, it is connected to the "bridge" network.
  - The bridge network allows containers to communicate with each other using their container names as hostnames
  - Containers connected to the bridge network can also access the external network and the host machine.

#### How bridge network works
  - Each container connected to the "bridge" network is assigned a unique IP address within the bridge network's subnet.
  - The bridge network is NATed, allowing containers to access external resources and the internet via the host's IP address.
  - It's important to note that the default bridge network is for basic communication and isolation between containers on the same host. If you need more advanced network configurations, such as connecting containers across different hosts or requiring specific networking features, Docker provides support for user-defined custom networks that you can create and manage as needed.

#### Multiple networks
  - You can have multiple containers listening on the same port but the host must be listening on a different port
    - ex. we can have 8080:80 & 80:80
      - this means that when port 8080 is accessed on host it will route to container 1 to port 80 & when port 80 is accessed on host it will route to second container port 80
    - but we cannot do this. 80:80 & 80:8080
      - this will error out when we try to create the second container saying that the host machine is already listening on port 80

### View what port a container is listening on
  - `docker port container-name`

### Docker network
  - `docker network ls`
    - list all networks
  - `docker network inspect NETWORK_NAME`
    - inspect a network
    - among all of the information it gives you it will give you the running containers in the networkj0:w

```json
[
    {
        "Name": "bridge",
        "Id": "9cc27e1d79d7df5e7f15b5eea7e4de674acf99b0841fbda6dab6f81054f413ac",
        "Created": "2023-10-30T17:24:08.868915952-05:00",
        "Scope": "local",
        "Driver": "bridge",
        "ConfigOnly": false,

        // ...

        "Containers": {
            "595894343cb46781979de44dc5e5a87cc2c5a543ed23c3c7162b37bd461730a7": {
                "Name": "nginx",
                "EndpointID": "b943f2917d7e38b3672f4ee76a795dbfb0fc6103cd541ba0370a6ee50c381b0d",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164": {
                "Name": "portainer",
                "EndpointID": "f2a95d3c8e09a4cbe5242b53e2c863a1b59bcde867c7421cff79fd9517a9060f",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        }
        // ...
    }
]

```

  - `docker network create --driver`
    - create a network
  - `docker network connect`
    - attach a network to a container
  - `docker network disconnect`
    - detach a network from a container

### Docker network drivers
  - What is a network driver
    - built-in or 3rd party extension that gives you virtual network features

### Docker networks DNS
  - Docker daemon has built-in DNS server that containers use by default
  - docker defaults to the hostname but you can also set aliases
  - bridge network does not have built in dns server by default
  - however all custom networks come with dns sever enabled by default

#### Docker DNS Round Robin
  - we can multiple containers on a created network resopnd to the same DNS address
  - it will cycle through the dns records using dns round robin

## Docker inspect
  - uses Go templates
  - format is case sensitive

  - `docker inspect portainer`

```text
tpool@tpool-thinkpad-l480:~$ docker inspect portainer
[
    {
        "Id": "9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164",
        "Created": "2021-10-04T13:23:00.369505177Z",
        "Path": "/portainer",
        "Args": [],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 2545,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2023-10-30T22:24:10.553120828Z",
            "FinishedAt": "2023-10-30T22:15:42.373298346Z"
        },
        "Image": "sha256:580c0e4e98b06d258754cf28c55f21a6fa0dc386e6fe0bf67e453c3642de9b8b",
        "ResolvConfPath": "/var/lib/docker/containers/9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164/hostname",
        "HostsPath": "/var/lib/docker/containers/9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164/hosts",
        "LogPath": "/var/lib/docker/containers/9ac08dc89f5a9e6b06d2a76f8602a9d240db76c3e9bcb5795c7ba27ad3ab4164/9ac08dc89f5a9e6b06d2a76f8602a9d240db76e9bcb5795c7ba27ad3ab4164-json.log",
        "Name": "/portainer",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/var/run/docker.sock:/var/run/docker.sock",
                "portainer_data:/data"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "8000/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "8000"
                    }
                ],
                "9000/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9000"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "always",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                0,
                0
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/ef2ed5f8857015e17c63409cf30709ab27e28980904ff7485b71491398a40023-init/diff:/var/lib/docker/overl2/6446e65733c5aed3c46249e5591d0d0d5a4c2880d9677726de09d7264750fa34/diff:/var/lib/docker/overlay2/ea1bb36db029c8376e60ff20ffeaf6b2ffa1a87345ec3dc9d9873b7e19757e/diff:/var/lib/docker/overlay2/aec3d97f1397147c1cbd02e8940012108f46f00aa57feaf693d2e9288883818f/diff",
                "MergedDir": "/var/lib/docker/overlay2/ef2ed5f8857015e17c63409cf30709ab27e28980904ff7485b71491398a40023/merged",
                "UpperDir": "/var/lib/docker/overlay2/ef2ed5f8857015e17c63409cf30709ab27e28980904ff7485b71491398a40023/diff",
                "WorkDir": "/var/lib/docker/overlay2/ef2ed5f8857015e17c63409cf30709ab27e28980904ff7485b71491398a40023/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "volume",
                "Name": "portainer_data",
                "Source": "/var/lib/docker/volumes/portainer_data/_data",
                "Destination": "/data",
                "Driver": "local",
                "Mode": "z",
                "RW": true,
                "Propagation": ""
            },
            {
                "Type": "bind",
                "Source": "/var/run/docker.sock",
                "Destination": "/var/run/docker.sock",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
            "Hostname": "9ac08dc89f5a",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "8000/tcp": {},
                "9000/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": null,
            "Image": "portainer/portainer",
            "Volumes": {
                "/data": {}
            },
            "WorkingDir": "/",
            "Entrypoint": [
                "/portainer"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "07bbc281fa8bb4cd026e14b8ff43938038b0cef93acb8e8abeddf8847564b8bc",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "8000/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "8000"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "8000"
                    }
                ],
                "9000/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9000"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9000"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/07bbc281fa8b",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "f2a95d3c8e09a4cbe5242b53e2c863a1b59bcde867c7421cff79fd9517a9060f",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "9cc27e1d79d7df5e7f15b5eea7e4de674acf99b0841fbda6dab6f81054f413ac",
                    "EndpointID": "f2a95d3c8e09a4cbe5242b53e2c863a1b59bcde867c7421cff79fd9517a9060f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
```

  - ![alt-text](/2023-10-13-docker-udemy-course/inspect.png)
    - gets the ID for the container

  - ![alt-text](/2023-10-13-docker-udemy-course/inspect2.png)
    - gets the ip address for the container

# Section 5 Container Images

## What is an image?
  - app binaries and dependencies
  - metadata about the image data and how to run the image
  - not a complete os. no kernel, drivers
  - could be as small as one executable file
  - could be as big as a linux distro like ubuntu with ap, apache, php and more

## Official and unofficial images
  - There is only one image that is official, there is no slashes in the name just the name like nginx
  - unofficial images are ones that have a username/reponame

## Image layers
  - images are layers upon layers
  - you don't have to install layers you already have
  - as we make changes to our images, it creates more layers
  - we are never storing the same layer multiple times on our system

## docker history & docker inspect
  - `docker history`
    - gives the history of the docker image
    - uses copy on write concept

## Building an image from a dockerfile
  - `docker build -t customnginx .`
    - the t just specifies the name of the image
    - we just use a dot because docker will look for a file named DockerImage
    - after processing you can find your image with `docker image ls`
    - say we want to build it again but a couple of the lines are the same, docker will cache it for the next run
      - that is what makes docker so fast

## Ordering of the dockerfile
  - order matters especially when it comes to speed
  - when you build an image it will go line by line and use the cache if it has not changed.
    - if it has changed it will have to run the code again taking longer
    - but not only will it have to run that code again, it will have to run all of the code below that too
    - that is why you keep the code that changes less at the top, and the code that changes the most at the bottom

## Keywords
  - FROM
    - from an offical repo or a custom one to base your image off of
  - WORKDIR
    - just like a cd mydir. It just changes your directory
  - COPY
    - copy to/from your local machine into your docker images

# Section 6 Persistent Data : Volumes
  - containers are usually immutable and ephemeral
  - only re-deploy container, never change
  - Docker gives us this feature to ensure these "separation of concerns"
  - known as "persistent data"
  - Two ways
    - Volumes
      - make special location outside of container UFS
    - Bind Mounts
      - link container path to host path
      - cool because it links to a directory on your host, and your docker container can use that file/folder
      - Maps a host file or directory to a container file
      - Skips UFS (Union file system) and host files overwrite any in container


## Volume Command
  - VOLUME command
    - used to create a mount point and associate it with a directory in the container. This allows the container to share data between the host machine and the container or between containers.
    - all files created in the container will outlive the container in a separate place on the host
    - needs manual deletion if you were to delete a container, it would not delete the volume
  - you dont' have to use the volume command to create a volume in docker, because you can just specify the location manually, however it is recommended to make a volume

  - creating a volume
  `docker volume create <myVolume>`

  - `docker container run -d --name mysql -v mysqlVolume mysqlImage`
    - with **-v** you can specify the name of the volume

  - `docker container run -d --name mysql -v mysqlVolume:/var/lib/volumes/mysqlVol mysqlImage`
    - you can even specify the location and name like this

## Bind Mounting
  - Maps a host file or directory to a container file or directory
  - Can't use in Dockerfile, must be at container run
  - `docker container run -v $(pwd):/usr/share/nginx/`
    - this will bind the mount in the cwd to /user/share/nginx in the container

## Bind Mounts vs Volumes
  - Bind mounts directly map host files or directories to container files or directories, while volumes are managed by Docker and provide more portability and functionality.
  - Bind mounts are suitable for development and can be used to access host files during container runtime, while volumes are preferred for sharing data among containers and across different Docker hosts.


## docker volume create
  - you can create your own volume manually
  - you would want to do this if you want to add a specific **driver**

# Section 7. Docker Compose

## What is docker compose
  - Docker Compose is a tool provided by Docker that simplifies the process of defining, running, and managing multi-container Docker applications.
  - It allows you to define the services, networks, and volumes required for your application in a single **YAML file**, typically named docker-compose.yml.
  - it uses Declarative synatx making it easy to read and maintain
  - it allows you to define dependencies
  - allows you to easily scale by defining the number of instances you want to run the yaml file

## Docker cli tool
  - `docker-compose`
  - cli tool used for local/dev/test automation with those yaml files
  - `docker-compose.yml` - is the default filename, but any can be used with `docker-compose -f`
  - now with docker 1.13+ these yaml files can be used with swarm

## docker-compose down --rmi local -v
  - removes all of the images that were built specifically for this docker-compose file and also removes any volumes that were created in association with it

## docker build
  - creates custom images before creating a container that will use them

```docker-compose
services:
  drupal:
    image: custom-drupal-image
    build: .
    ports:
      - "8080:80"
    volumes:
      - drupal-module:/var/www/html/modules
      - drupal-profiles:/var/www/html/profiles
      - drupal-sites:/var/www/html/sites
      - drupal-themes:/var/www/html/themes

  postgres:
    image: postgres
    environment:
      - POSTGRES_PASSWORD=password
    volumes:
      - drupal-data:/var/lib/postgresql/data

volumes:
  drupal-data:
  drupal-module:
  drupal-profiles:
  drupal-sites:
  drupal-themes:
```
  - creates the image first with the Docker file that is in the current directory and names that image name 'custom-drupal-image'

# Section 8. Swarm Intro and Creating a 3-Node Swarm Cluster

## What is it
  - Swarm mode is a clustering solution built inside of docker
  - note related to swarm "classic" for pre-1.12 versions
  - Not enabled by default, new commands once enabled
    - `docker swarm`
    - `docker node`
    - `docker service`
    - `docker stack`
    - `docker secret`

## How it works
  - A swarm is made of nodes
  - A manager node has a database locally on them, it stores their configuration and gives them all the need to be the authority inside a swarm
  - They all have their own local db copy and encrypt their traffic to ensure integrity
  - the control plane is where all the traffic between the nodes gets sent over
  - ![docker manager](\2023-10-13-docker-udemy-course\docker-manager.png)
  - ![docker manager overview](\2023-10-13-docker-udemy-course\manager-overview.png)
  - a manager is just a worker with permissions to control the swarm
  - ![docker manager overview](\2023-10-13-docker-udemy-course\swarm-example.png)
    - a single service can have multiple tasks, as seen in the picture
  - ![docker swarm architecture](\2023-10-13-docker-udemy-course\swarm-architecure.png)

## docker swarm init
  - Lots of PKI and security automation
    - Root signing certificate created for our swarm
    - cert is issued for first manager role
    - join tokens were created
  - Raft database created to store root CA, configs, and secrets
    - encrypted by default
    - no need for another key/value system to hold orchestration/secrets

## docker node ls
  - gets all of the manager and nodes in a swarm

## docker service ls
  - gets all of the services sent to a swarm of containers

## docker service ps <service-id>
  - gets all of the tasks for a given service

## docker service
  - used to sort of in place of the docker run command so we don't break existing docker code

## Say one of those containers goes down
  - if were to remove a container while a docker swarm has a service that has 3 replicas spinned up. It will create another container and continue.
  - Swarm does its best to make sure if a container goes down to spin up a new one as fast as it can

## Overlay Multi-Host Networking
  - use `--driver overlay` when creating a network
  - for container to container traffic inside a single swarm
  - optional IPSec (AES) encryption on network creation
  - each service can be connect to multiple networks (ex. backend, frontend)

## Swarm Routing mesh
  - routes ingress (incoming) packets for a service to proper task
  - spans all nodes in a swarm
  - uses ipvs from linux kernel
  - two ways this works
    - container-to-container in an overlay network (uses vip)
    - external traffic incoming to published ports (all nodes listen)
  - stateless load balancing
  - Load balancer is at OSI Level 3
    - But the limitation can be overcame by using something like nginx that operates on level 4

## mounting volumes in swarm
  - [stackoverflow post](https://stackoverflow.com/questions/47756029/how-does-docker-swarm-implement-volume-sharing)

## Stacks
  - A new layer of abstraction to swarm called **stacks**
  - Stacks accept **compose files** as their **declarative** definition for **services, networks, and volumes**
  - `docker stack deploy`
  - stacks manages all thos objects for us, including the **overlay network** per stack. Adds stack name to start of their name
  - deploy key in compose file **Cannot** do **build**
    - compose ignores **deploy**: keyword
    - swarm ignores **build**: keyword
  - stacks only work on a 1 swarm basis. Meaning a single stack file can only deploy one swarm, that's it
  - `docker stack deploy -c mystackfile.yml stackName`
    - deploy a swarm with a yml file

## Updating a stack
  - If you wanted to updated a running stack, you just have to update the .yml file and rerun `docker stack deploy -c <mystackfile.yml> mystackname`
  - docker will go through the file and make any necessary updates

## Secrets in stacks
  - Easiest "secure" solution for storing secrets in swarm
  - built into swarm
  - secure because encrypted at rest, transit.
  - as of docker 1.13 swarm raft db is encrypted on disk
  - what is a secret
    - ssh keys
    - tls cert
    - username & passwords
    - etc. whatever you don't want anyone to view
  - supports generic strings or binary content up to **500kb** in size
  - doesn't require apps to be rewritten
  - only stored on disk of manager nodes
  - secrets are first stored in swarm, then assigned to a service
  - they look like files in container but are actually stored in **memory** fs
    - /run/secrets/<secret-name> or
      - /run/secrets/<secret-alias>

## Creating the secret through the file
  - `docker secret create password mypasswordfile.txt`
## Creating the secret by passing it through the shell
  - `echo "myDBpassword" | docker secret create psql_pass -`
    - the `-` at the end tells the shell to get the input from stdin which was passed via grep

## Telling docker to use a secret for a docker container

```shell
  docker service create --name psql \
    --secret psql_user --secret psql_pass \
    -e POSTGRES_PASSWORD_FILE=/run/secrets/psql_pass \
    -e POSTGRES_USER_FILE=/run/secrets/psql_user postgres
```
  - this is a security concern because the file gets stored on the file system of the container it is used for
  - if we were to connect to the shell of this container, the file would be stored here `/run/secrets/<secret-name>`

## Telling docker to use secrets in a container in the docker compose file

```yaml
version: "3.1"

# services
services:
  psql:
    image: postgres
    secrets:
      - psql_user
      - psql_pass
    environment:
      - POSTGRES_PASSWORD_FILE: /run/secrets/psql_pass
      - POSTGRES_USER_FILE: /run/secrets/psql_user

# define our secrets
secrets:
  psql_user:
    file: ./psql_user.txt
  psql_pass:
    file: ./psql_pass.txt
```
  - `docker stack deploy -c docker-compose.yml mydb`
  - creates the secrets before the services
  - At the bottom we are defining our environment variables by using the file it is stored in
  - And in the psql service we are using the file path where the environment variable will be stored in on the container

We could also define our secrets before hand and use them in our docker compose another way

## Secrets with stacks
  - version fo the compose file has to be at min 3.1
  - **external** keyword tells the compose file to look for the secret that has been declared before
```yaml
# This example file from a previous lecture where we ran drupal in docker compose
# in this Assignment, change it to work with the default drupal image, and change
# postgres to use a Swarm secret. More info in the README.md file.

version: "3.1"

services:

  drupal:
    image: custom-drupal
    ports:
      - "8080:80"
    volumes:
      - drupal-modules:/var/www/html/modules
      - drupal-profiles:/var/www/html/profiles
      - drupal-sites:/var/www/html/sites
      - drupal-themes:/var/www/html/themes

  postgres:
    image: postgres:14
    environment:
      - POSTGRES_PASSWORD=/run/secrets/psql-pw
    # the docker manager will share the secret with this container
    secrets:
      - psql-pw
    volumes:
      - drupal-data:/var/lib/postgresql/data

volumes:
  drupal-data:
  drupal-modules:
  drupal-profiles:
  drupal-sites:
  drupal-themes:

# tells compose file that the secret has already been declared
secrets:
  psql-pw:
    external: true
```

# Section 10: Swarm App Lifecycle

## Full App Lifecycle with Compose
  - `docker-compose up` for development environment
  - `docker-compose up` for CI environment
  - `docker stack deploy` production environment
  - `docker-compose.override.yml` - by default when you run `docker-compose up` it will run this file
  - `docker-compose -f docker-compose.override.yml up -d` - First runs docker-compose.yml then docker-compose.override.yml and merges them


## Using the docker compose config to merge
  `docker-compose -f docker-compose.yml -f docker-compose.test.yml config > output.yml`
  - merges the two compose files into one combined one and outputs it to `output.yml`

## Swarm Updates
  - Provides rolling replacement of tasks/containers in a service
  - Limits downtime (be careful with "prevents" downtime)

  - How to update the image used to a newer version
    - `docker service update --image myapp:1.2.1 myservicerunning`
  - Adding an environment variable and remove a port
    - `docker service update --env-add NODE_ENV=production --publish-rm 8080`
  - Change number of replicas of two services
    - `docker service scale web=8 api=6`
  - Rebalancing to even out the tasks to the nodes in a swarm
    - `docker service update --force web`

## Docker Healthcheck
  - `HEALTHCHECK` was added in 1.12
  - supported in dockerfile, compose yaml, docker run, and swarm services
  - docker engine will exec's the command in the container
  - it expects exit 0(OK) or exit 1(ERROR)
  - there are 3 container states (STARTING, HEALTHY, UNHEALTHY)
  - `docker service create --name db --replicas 3 -e POSTGRES_PASSWORD=mysecretpassword --health-cmd "pg_isready -U postgres || exit 1" -d postgres`
  - `docker container run --name db -e POSTGRES_PASSWORD=mysecretpassword --health-cmd "pg_isready -U postgres || exit 1" postgres`
```yaml
FROM UBUNTU:20.04

COPY ./Downloads /home/newuser/Downloads

WORKDIR /home/newuser/Downloads

HEALTHCHECK ./healcheck-script.sh || exit 1
```
- if the healthcheck script fails then it will return 1 and status will be unhealthy


# Section 13 The What and Why of Kubernetes

## What is Kubernetes
  -  Kubernetes = popular container orchestrator
  - Released by Google but now maintained by an open source community
  - Makes many machines act as one
  - Runs on Top of Docker (usually) as a set of APIs in containers
  - provides API/CLI to manage containers across servers
  - many clouds provide it for you
  - many vendors make a "distribution" of it
  - uses same raft protocol to get a consensus

## Why Kubernetes
  - It is the waythe industry is going
  - Servers + Change Rate = Benefit of orchestration

## Kubernetes vs Swarm
  - Swarm is Easy
  - Kubernetes has more features and flexibility
  - Swarm
    - Comes with docker
    - easiest orchestrator to deploy/manage yourself
    - Follows 80/20 rule, 20% of features of k8 and solves 80% of the uses cases
    - Runs anywhere Docker does: local,cloud,data-center, arm, windows, 32-bit
    - Secure by default
    - Easier to troubleshoot
  - Kubernetes
    - Clouds will deploy/manage kubernetes for you
    - infrastructure vendors are making their own distros
    - widest adoption and community
    - Flexible: Covers widest set of use cases
    - "No one ever got fired for buying IBM"

# Section 14 Kubernetes Architecture and Install

## Terminology
  Kubernetes
  - The whole orchestration system
  - K8s (Kube for short)
  - (K eight letters and then the s)

  Kubectl
  - CLI to configure k8 and manage apps
  - "cube control" - official pronunciation

  Node
  - Single server in the k8 cluster

  Pod
  - one or more containers running together on one node
  - basic unit of deployment. Containers are always in pods

  Controller
  - For creating/updating pods and other objects
  - Many types of Controllers
    - Deployment, Replicaset, Statefulset, DaemonSet, Job, CronJob

  Service
  - network endpoint to connect to a pod(s)
  - an abstraction which defines a logical set of Pods and a policy by which to access them.

  Jobs
  - Creates pods(s) and ensures that a specified number successfully completed. When a specified number of successful run of pods is completed, then the job is considered complete

  Namespace
  - Logical separation between teams and their environments. it allows various teams (Dev,Prod) to share K8's cluster by providing isolated workspace
  - Filtered group of objects in cluster

  Kubelet
  - k8 agent running on the nodes
  - since k8 runs on top of the docker engine, it needs its own agent and engine to function correctly (swarm didn't need one because it was built into docker)

  Control Plane:
  - Set of containers that manage the cluster
  - Includes API server, scheduler, controller manager, etcd, and more
  - sometimes called the "master"

# Section 15: Your first Pods

## Kubectl run, create, apply
  - `kubectl run` (single pod per command since 1.18)
    - similar to docker run
    - you always have to specify a name for the pod

  - `kubectl create` (create some resources via CLI or YAML)
    - similar to docker create

  - `kubectl apply` (create / update anything via YAML)
    - similar to docker stack deploy

## kubectl explain
  - the cli can give you information about something in k8 with the explain command
  - `kubectl explain pods`

## General
  - You typically use a yaml file for deployment and just the cli for testing and development
  - Unlike Docker, you can't create a container directly in k8
    - k8 creates pods (via cli,yaml or api) which k8 then in turn creates containers inside of it
  - kubelet tells the container runtime to create containers for you

## Deployment with kubectl
  - essentially the equivalent to what a swarm service is like
  - allows you to create one or more pods
  - `kubectl create deployment my-nginx --image nginx`
  - this will create a **relicateset** instead of a pod directly

  - `kubectl delete deployment my-nginx`
  - delete the deployment

## Scaling Relicasets
  - Essentially "add more pods or replicas to the node in the deploymment"
  - `kubectl scale` will change the deployment record
  - cm will see that only the replica count has changed
  - scheduler sees a new pod is requested, assigns to a node
  - kubelet sees a new pod, tells container runtime to start httpd



# Section 16. Inspecting Kubernetes Resources

## kubectl get ..
  - `kubectl get all`
    - List our common resources (in the default namespace)

  - `kubectl get deploy/<deployment-name>`
    - view only the kubectl resource you are trying to look at

  - `kubectl get deploy/apache -o wide`
    - view in wide format

  - `kubectl get deploy/apache -o json`
    - view in json format

  - `kubectl get` has a weakness
    - it can only show one resource at a time
    - we need a command that combines related resources
    - parent/child resources
    - events of that resource

  - `kubectl get events --watch-only`
    - only get the events that happen for future events

## kubectl describe
  - `kubectl describe deploy/my-apache`
  - describe does the following
    - Deployment summary
    - ReplicaSet status
    - Pod Template
    - Old/New ReplicaSet names
    - Deployment Events

  - Example output
```yaml
trestenp@PD-ITCADTEST6:~/Playground/dca-training/Docker-Certified-Associate-DCA-Exam-Guide$ k describe deploy/apache
Name:                   apache
Namespace:              default
CreationTimestamp:      Fri, 31 May 2024 09:28:28 -0500
Labels:                 app=apache
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=apache
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=apache
  Containers:
   httpd:
    Image:        httpd
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Progressing    True    NewReplicaSetAvailable
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   apache-f9489c7dc (2/2 replicas created)
Events:          <none>
```

## Container Logs in Kubernetes
  - the logs are not stored in etcd. They are stored on each node with the container runtime

  - `kubectl logs pod/mypod`
    - get the logs for one pod

  - `kubectl logs deploy/apache --all-containers=true`
    - gets the logs for all of the containers for the deployment
  

# Section 17. Exposing Kubernetes ports

## Service Types
  - A service in kubernetes is a stable network address for pods(s)
  - when you create a pod, you don't automatically get a dns name so it can communicate internally & externally. That has be done manually with services
  - CoreDNS allows us to resolve services by name
  - There are different types for services
    - Cluster IP (default)
      - Exposes the Service on a cluster-internal IP. Choosing this value makes the Service only reachable from within the cluster. This is the default that is used if you don't explicitly specify a type for a Service. You can expose the Service to the public internet using an Ingress or a Gateway.
    - NodePort
      - Exposes the Service on each Node's IP at a static port (the NodePort). To make the node port available, Kubernetes sets up a cluster IP address, the same as if you had requested a Service of type: ClusterIP.
    - LoadBalancer
      - Exposes the Service externally using an external load balancer. Kubernetes does not directly offer a load balancing component; you must provide one, or you can integrate your Kubernetes cluster with a cloud provider.
    - ExternalName
      - Maps the Service to the contents of the externalName field (for example, to the hostname api.foo.bar.example). The mapping configures your cluster's DNS server to return a CNAME record with that external hostname value. No proxying of any kind is set up.

## Exposing Containers
  - `kubectl expose deploy/<deployment-name> --port 8888`
  - `kubectl expose deploy/<deployment-name> --port 8888 --name httpenv-np --type NodePort`
  
```bash
trestenp@PD-ITCADTEST6:~$ kubectl get services
NAME         TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
httpenv      ClusterIP   10.97.133.11   <none>        8888/TCP         2d15h
httpenv-np   NodePort    10.103.86.5    <none>        8888:30805/TCP   35s
kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP          2d23h
```
  - In K8, it is opposite to how docker describes and views ports
    - In docker it is Host:Container
    - In K8 it is Cluster:Host

## Deleting Services
  - `kubectl delete <type>/<service-name>`
    - format
  - `kubectl delete service/httpenv`
    - example
  - `kubectl delete service/httpenv deployment/nginx pod/mypod1`
    - exampe of deleting multiple objects in k8

## Kubernetes DNS
  - DNS is optional or an addon inside of a k8 cluster
  - CorDNS
    - Starting with 1.11
    - Like Swarm, this is DNS-based service discovery

# Section 18. Kubernetes Management Techniques
  - k8 is un-opinionated, meaning you can adapt it for whatever technique you would like to use like imperative or declarative. from the cmdline or yaml

## Resource Generators
  - the command in kubectl have some automation behind them called generators
  - These commands are helper templates called "generators"
  - Every resource in kubernetes has a specification or **"spec"**
  - To view the spec of a command without executing it, use `--dry-run=client -o yaml` 
  - `kubectl create deployment nginxDeployment --image nginx --dry-run=client -o yaml`
  - `kubectl create pod nginxPod --image nginx --dry-run=client -o yaml`
  - `kubectl create task nginxTask --image nginx --dry-run=client -o yaml`
  - you can use those YAML defaults as a starting poin
  - generators are "opinionated defaults"

# Section 19. Moving to Declarative Kubernetes YAML
  - storing your configuration in yaml and using the `kubectl apply -f myconfig.yaml`
  - can be yaml or json but humans prefer yaml. K8 will convert to json and relay to api in json
  - each file contains one or more **manifests**
  - Each manifest needs **four parts** (rootKey: values)
    1. `apiVersion:<version>`
    2. `kind:<kind>`
    3. `metadata:<metadata>`
    4. `spec:<spec>`
  - the apiVersion & kind are what decide what resource you are going to get and what version of the api you are going to use for that resource or kind
  
## apiVersion
  - `kubectl api-versions`
    - get a list of all of the possible versions you can use in your yaml file

## Kind
  - `kubectl api-resources`
    - gives you a list of all the options you can put under **kind** in the yaml file

## spec
  - `kubectl explain services --recursive`

```text
trestenp@PD-ITCADTEST6:~$ kubectl explain services --recursive
KIND:       Service
VERSION:    v1

DESCRIPTION:
    Service is a named abstraction of software service (for example, mysql)
    consisting of local port (for example 3306) that the proxy listens on, and
    the selector that determines which pods will answer requests sent through
    the proxy.

FIELDS:
  apiVersion    <string>
  kind  <string>
  metadata      <ObjectMeta>
    annotations <map[string]string>
    creationTimestamp   <string>
    deletionGracePeriodSeconds  <integer>
    deletionTimestamp   <string>
    finalizers  <[]string>
    generateName        <string>
    generation  <integer>
    labels      <map[string]string>
    managedFields       <[]ManagedFieldsEntry>
      apiVersion        <string>
      fieldsType        <string>
      fieldsV1  <FieldsV1>
      manager   <string>
      operation <string>
      subresource       <string>
      time      <string>
    name        <string>
    namespace   <string>
    ownerReferences     <[]OwnerReference>
      apiVersion        <string> -required-
      blockOwnerDeletion        <boolean>
      controller        <boolean>
      kind      <string> -required-
      name      <string> -required-
      uid       <string> -required-
    resourceVersion     <string>
    selfLink    <string>
    uid <string>
  spec  <ServiceSpec>
    allocateLoadBalancerNodePorts       <boolean>
    clusterIP   <string>
    clusterIPs  <[]string>
    externalIPs <[]string>
    externalName        <string>
    externalTrafficPolicy       <string>
    healthCheckNodePort <integer>
    internalTrafficPolicy       <string>
    ipFamilies  <[]string>
    ipFamilyPolicy      <string>
    loadBalancerClass   <string>
    loadBalancerIP      <string>
    loadBalancerSourceRanges    <[]string>
    ports       <[]ServicePort>
      appProtocol       <string>
      name      <string>
      nodePort  <integer>
      port      <integer> -required-
      protocol  <string>
      targetPort        <IntOrString>
    publishNotReadyAddresses    <boolean>
    selector    <map[string]string>
    sessionAffinity     <string>
    sessionAffinityConfig       <SessionAffinityConfig>
      clientIP  <ClientIPConfig>
        timeoutSeconds  <integer>
    type        <string>
  status        <ServiceStatus>
    conditions  <[]Condition>
      lastTransitionTime        <string> -required-
      message   <string> -required-
      observedGeneration        <integer>
      reason    <string> -required-
      status    <string> -required-
      type      <string> -required-
    loadBalancer        <LoadBalancerStatus>
      ingress   <[]LoadBalancerIngress>
        hostname        <string>
        ip      <string>
        ipMode  <string>
        ports   <[]PortStatus>
          error <string>
          port  <integer> -required-
          protocol      <string> -required-
```
  - get a spec list of the possible options you can use
  - good for a quick lookup and reference because it only tells you the name and the data type it accepts
  
  - `kubectl explain services.spec`

```text
trestenp@PD-ITCADTEST6:~$ k explain services.spec
KIND:       Service
VERSION:    v1

FIELD: spec <ServiceSpec>

DESCRIPTION:
    Spec defines the behavior of a service.
    https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#spec-and-status
    ServiceSpec describes the attributes that a user creates on a service.

FIELDS:
  allocateLoadBalancerNodePorts <boolean>
    allocateLoadBalancerNodePorts defines if NodePorts will be automatically
    allocated for services with type LoadBalancer.  Default is "true". It may be
    set to "false" if the cluster load-balancer does not rely on NodePorts.  If
    the caller requests specific NodePorts (by specifying a value), those
    requests will be respected, regardless of this field. This field may only be
    set for services with type LoadBalancer and will be cleared if the type is
    changed to any other type.

  clusterIP     <string>
    clusterIP is the IP address of the service and is usually assigned randomly.
    If an address is specified manually, is in-range (as per system
    configuration), and is not in use, it will be allocated to the service;
    otherwise creation of the service will fail. This field may not be changed
    through updates unless the type field is also being changed to ExternalName
    (which requires this field to be blank) or the type field is being changed
    from ExternalName (in which case this field may optionally be specified, as
    describe above).  Valid values are "None", empty string (""), or a valid IP
    address. Setting this to "None" makes a "headless service" (no virtual IP),
    which is useful when direct endpoint connections are preferred and proxying
    is not required.  Only applies to types ClusterIP, NodePort, and
    LoadBalancer. If this field is specified when creating a Service of type
    ExternalName, creation will fail. This field will be wiped when updating a
    Service to type ExternalName. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies

  clusterIPs    <[]string>
    ClusterIPs is a list of IP addresses assigned to this service, and are
    usually assigned randomly.  If an address is specified manually, is in-range
    (as per system configuration), and is not in use, it will be allocated to
    the service; otherwise creation of the service will fail. This field may not
    be changed through updates unless the type field is also being changed to
    ExternalName (which requires this field to be empty) or the type field is
    being changed from ExternalName (in which case this field may optionally be
    specified, as describe above).  Valid values are "None", empty string (""),
    or a valid IP address.  Setting this to "None" makes a "headless service"
    (no virtual IP), which is useful when direct endpoint connections are
    preferred and proxying is not required.  Only applies to types ClusterIP,
    NodePort, and LoadBalancer. If this field is specified when creating a
    Service of type ExternalName, creation will fail. This field will be wiped
    when updating a Service to type ExternalName.  If this field is not
    specified, it will be initialized from the clusterIP field.  If this field
    is specified, clients must ensure that clusterIPs[0] and clusterIP have the
    same value.

    This field may hold a maximum of two entries (dual-stack IPs, in either
    order). These IPs must correspond to the values of the ipFamilies field.
    Both clusterIPs and ipFamilies are governed by the ipFamilyPolicy field.
    More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies

  externalIPs   <[]string>
    externalIPs is a list of IP addresses for which nodes in the cluster will
    also accept traffic for this service.  These IPs are not managed by
    Kubernetes.  The user is responsible for ensuring that traffic arrives at a
    node with this IP.  A common example is external load-balancers that are not
    part of the Kubernetes system.

  externalName  <string>
    externalName is the external reference that discovery mechanisms will return
    as an alias for this service (e.g. a DNS CNAME record). No proxying will be
    involved.  Must be a lowercase RFC-1123 hostname
    (https://tools.ietf.org/html/rfc1123) and requires `type` to be
    "ExternalName".

  externalTrafficPolicy <string>
    externalTrafficPolicy describes how nodes distribute service traffic they
    receive on one of the Service's "externally-facing" addresses (NodePorts,
    ExternalIPs, and LoadBalancer IPs). If set to "Local", the proxy will
    configure the service in a way that assumes that external load balancers
    will take care of balancing the service traffic between nodes, and so each
    node will deliver traffic only to the node-local endpoints of the service,
    without masquerading the client source IP. (Traffic mistakenly sent to a
    node with no endpoints will be dropped.) The default value, "Cluster", uses
    the standard behavior of routing to all endpoints evenly (possibly modified
    by topology and other features). Note that traffic sent to an External IP or
    LoadBalancer IP from within the cluster will always get "Cluster" semantics,
    but clients sending to a NodePort from within the cluster may need to take
    traffic policy into account when picking a node.

    Possible enum values:
     - `"Cluster"`
     - `"Cluster"` routes traffic to all endpoints.
     - `"Local"`
     - `"Local"` preserves the source IP of the traffic by routing only to
    endpoints on the same node as the traffic was received on (dropping the
    traffic if there are no local endpoints).

  healthCheckNodePort   <integer>
    healthCheckNodePort specifies the healthcheck nodePort for the service. This
    only applies when type is set to LoadBalancer and externalTrafficPolicy is
    set to Local. If a value is specified, is in-range, and is not in use, it
    will be used.  If not specified, a value will be automatically allocated.
    External systems (e.g. load-balancers) can use this port to determine if a
    given node holds endpoints for this service or not.  If this field is
    specified when creating a Service which does not need it, creation will
    fail. This field will be wiped when updating a Service to no longer need it
    (e.g. changing type). This field cannot be updated once set.

  internalTrafficPolicy <string>
    InternalTrafficPolicy describes how nodes distribute service traffic they
    receive on the ClusterIP. If set to "Local", the proxy will assume that pods
    only want to talk to endpoints of the service on the same node as the pod,
    dropping the traffic if there are no local endpoints. The default value,
    "Cluster", uses the standard behavior of routing to all endpoints evenly
    (possibly modified by topology and other features).

    Possible enum values:
     - `"Cluster"` routes traffic to all endpoints.
     - `"Local"` routes traffic only to endpoints on the same node as the client
    pod (dropping the traffic if there are no local endpoints).

  ipFamilies    <[]string>
    IPFamilies is a list of IP families (e.g. IPv4, IPv6) assigned to this
    service. This field is usually assigned automatically based on cluster
    configuration and the ipFamilyPolicy field. If this field is specified
    manually, the requested family is available in the cluster, and
    ipFamilyPolicy allows it, it will be used; otherwise creation of the service
    will fail. This field is conditionally mutable: it allows for adding or
    removing a secondary IP family, but it does not allow changing the primary
    IP family of the Service. Valid values are "IPv4" and "IPv6".  This field
    only applies to Services of types ClusterIP, NodePort, and LoadBalancer, and
    does apply to "headless" services. This field will be wiped when updating a
    Service to type ExternalName.

    This field may hold a maximum of two entries (dual-stack families, in either
    order).  These families must correspond to the values of the clusterIPs
    field, if specified. Both clusterIPs and ipFamilies are governed by the
    ipFamilyPolicy field.

  ipFamilyPolicy        <string>
    IPFamilyPolicy represents the dual-stack-ness requested or required by this
    Service. If there is no value provided, then this field will be set to
    SingleStack. Services can be "SingleStack" (a single IP family),
    "PreferDualStack" (two IP families on dual-stack configured clusters or a
    single IP family on single-stack clusters), or "RequireDualStack" (two IP
    families on dual-stack configured clusters, otherwise fail). The ipFamilies
    and clusterIPs fields depend on the value of this field. This field will be
    wiped when updating a service to type ExternalName.

    Possible enum values:
     - `"PreferDualStack"` indicates that this service prefers dual-stack when
    the cluster is configured for dual-stack. If the cluster is not configured
    for dual-stack the service will be assigned a single IPFamily. If the
    IPFamily is not set in service.spec.ipFamilies then the service will be
    assigned the default IPFamily configured on the cluster
     - `"RequireDualStack"` indicates that this service requires dual-stack.
    Using IPFamilyPolicyRequireDualStack on a single stack cluster will result
    in validation errors. The IPFamilies (and their order) assigned to this
    service is based on service.spec.ipFamilies. If service.spec.ipFamilies was
    not provided then it will be assigned according to how they are configured
    on the cluster. If service.spec.ipFamilies has only one entry then the
    alternative IPFamily will be added by apiserver
     - `"SingleStack"` indicates that this service is required to have a single
    IPFamily. The IPFamily assigned is based on the default IPFamily used by the
    cluster or as identified by service.spec.ipFamilies field

  loadBalancerClass     <string>
    loadBalancerClass is the class of the load balancer implementation this
    Service belongs to. If specified, the value of this field must be a
    label-style identifier, with an optional prefix, e.g. "internal-vip" or
    "example.com/internal-vip". Unprefixed names are reserved for end-users.
    This field can only be set when the Service type is 'LoadBalancer'. If not
    set, the default load balancer implementation is used, today this is
    typically done through the cloud provider integration, but should apply for
    any default implementation. If set, it is assumed that a load balancer
    implementation is watching for Services with a matching class. Any default
    load balancer implementation (e.g. cloud providers) should ignore Services
    that set this field. This field can only be set when creating or updating a
    Service to type 'LoadBalancer'. Once set, it can not be changed. This field
    will be wiped when a service is updated to a non 'LoadBalancer' type.

  loadBalancerIP        <string>
    Only applies to Service Type: LoadBalancer. This feature depends on whether
    the underlying cloud-provider supports specifying the loadBalancerIP when a
    load balancer is created. This field will be ignored if the cloud-provider
    does not support the feature. Deprecated: This field was under-specified and
    its meaning varies across implementations. Using it is non-portable and it
    may not support dual-stack. Users are encouraged to use
    implementation-specific annotations when available.

  loadBalancerSourceRanges      <[]string>
    If specified and supported by the platform, this will restrict traffic
    through the cloud-provider load-balancer will be restricted to the specified
    client IPs. This field will be ignored if the cloud-provider does not
    support the feature." More info:
    https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/

  ports <[]ServicePort>
    The list of ports that are exposed by this service. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies

  publishNotReadyAddresses      <boolean>
    publishNotReadyAddresses indicates that any agent which deals with endpoints
    for this Service should disregard any indications of ready/not-ready. The
    primary use case for setting this field is for a StatefulSet's Headless
    Service to propagate SRV DNS records for its Pods for the purpose of peer
    discovery. The Kubernetes controllers that generate Endpoints and
    EndpointSlice resources for Services interpret this to mean that all
    endpoints are considered "ready" even if the Pods themselves are not. Agents
    which consume only Kubernetes generated endpoints through the Endpoints or
    EndpointSlice resources can safely assume this behavior.

  selector      <map[string]string>
    Route service traffic to pods with label keys and values matching this
    selector. If empty or not present, the service is assumed to have an
    external process managing its endpoints, which Kubernetes will not modify.
    Only applies to types ClusterIP, NodePort, and LoadBalancer. Ignored if type
    is ExternalName. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/

  sessionAffinity       <string>
    Supports "ClientIP" and "None". Used to maintain session affinity. Enable
    client IP based session affinity. Must be ClientIP or None. Defaults to
    None. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#virtual-ips-and-service-proxies

    Possible enum values:
     - `"ClientIP"` is the Client IP based.
     - `"None"` - no session affinity.

  sessionAffinityConfig <SessionAffinityConfig>
    sessionAffinityConfig contains the configurations of session affinity.

  type  <string>
    type determines how the Service is exposed. Defaults to ClusterIP. Valid
    options are ExternalName, ClusterIP, NodePort, and LoadBalancer. "ClusterIP"
    allocates a cluster-internal IP address for load-balancing to endpoints.
    Endpoints are determined by the selector or if that is not specified, by
    manual construction of an Endpoints object or EndpointSlice objects. If
    clusterIP is "None", no virtual IP is allocated and the endpoints are
    published as a set of endpoints rather than a virtual IP. "NodePort" builds
    on ClusterIP and allocates a port on every node which routes to the same
    endpoints as the clusterIP. "LoadBalancer" builds on NodePort and creates an
    external load-balancer (if supported in the current cloud) which routes to
    the same endpoints as the clusterIP. "ExternalName" aliases this service to
    the specified externalName. Several other fields do not apply to
    ExternalName services. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types

    Possible enum values:
     - `"ClusterIP"` means a service will only be accessible inside the cluster,
    via the cluster IP.
     - `"ExternalName"` means a service consists of only a reference to an
    external name that kubedns or equivalent will return as a CNAME record, with
    no exposing or proxying of any pods involved.
     - `"LoadBalancer"` means a service will be exposed via an external load
    balancer (if the cloud provider supports it), in addition to 'NodePort'
    type.
     - `"NodePort"` means a service will be exposed on one port of every node,
    in addition to 'ClusterIP' type.
```
  - this is good because it gives you a detailed description of all of the 

  - `kubectl explain services.spec.type`
  - we can keep drilling down with dot notation to get the resource key:value you are looking for without everything else

```text
trestenp@PD-ITCADTEST6:~$ kubectl explain services.spec.type
KIND:       Service
VERSION:    v1

FIELD: type <string>

DESCRIPTION:
    type determines how the Service is exposed. Defaults to ClusterIP. Valid
    options are ExternalName, ClusterIP, NodePort, and LoadBalancer. "ClusterIP"
    allocates a cluster-internal IP address for load-balancing to endpoints.
    Endpoints are determined by the selector or if that is not specified, by
    manual construction of an Endpoints object or EndpointSlice objects. If
    clusterIP is "None", no virtual IP is allocated and the endpoints are
    published as a set of endpoints rather than a virtual IP. "NodePort" builds
    on ClusterIP and allocates a port on every node which routes to the same
    endpoints as the clusterIP. "LoadBalancer" builds on NodePort and creates an
    external load-balancer (if supported in the current cloud) which routes to
    the same endpoints as the clusterIP. "ExternalName" aliases this service to
    the specified externalName. Several other fields do not apply to
    ExternalName services. More info:
    https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types

    Possible enum values:
     - `"ClusterIP"` means a service will only be accessible inside the cluster,
    via the cluster IP.
     - `"ExternalName"` means a service consists of only a reference to an
    external name that kubedns or equivalent will return as a CNAME record, with
    no exposing or proxying of any pods involved.
     - `"LoadBalancer"` means a service will be exposed via an external load
    balancer (if the cloud provider supports it), in addition to 'NodePort'
    type.
     - `"NodePort"` means a service will be exposed on one port of every node,
    in addition to 'ClusterIP' type.
```
  - and if all else fails look at the api docs on the kubernetes site [api-docs](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.30/#servicespec-v1-core)

## diff
  - `kubectl diff -f app.yml`
  - looks at the specs that are currently running in k8 and what is in the file and print out the differences
```text
trestenp@PD-ITCADTEST6:/mnt/c/Users/trestenp/OneDrive - City of Corpus Christi/Udemy/udemy-docker-mastery-main/udemy-docker-mastery-main$ k diff -f k8s-yaml/app.yml
diff -u -N /tmp/LIVE-2663337493/apps.v1.Deployment.default.app-nginx-deployment /tmp/MERGED-1538727162/apps.v1.Deployment.default.app-nginx-deployment
--- /tmp/LIVE-2663337493/apps.v1.Deployment.default.app-nginx-deployment        2024-06-04 08:36:06.529521378 -0500
+++ /tmp/MERGED-1538727162/apps.v1.Deployment.default.app-nginx-deployment      2024-06-04 08:36:06.529521378 -0500
@@ -6,14 +6,14 @@
     kubectl.kubernetes.io/last-applied-configuration: |
       {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"name":"app-nginx-deployment","namespace":"default"},"spec":{"replicas":3,"selector":{"matchLabels":{"app":"app-nginx"}},"template":{"metadata":{"labels":{"app":"app-nginx"}},"spec":{"containers":[{"image":"nginx:1.17.3","name":"nginx","ports":[{"containerPort":80}]}]}}}}
   creationTimestamp: "2024-06-04T13:30:45Z"
-  generation: 1
+  generation: 2
   name: app-nginx-deployment
   namespace: default
   resourceVersion: "461022"
   uid: 66d8722b-d416-4b58-b30c-c3e88bdd0a2f
 spec:
   progressDeadlineSeconds: 600
-  replicas: 3
+  replicas: 2
   revisionHistoryLimit: 10
   selector:
     matchLabels:
diff -u -N /tmp/LIVE-2663337493/v1.Service.default.app-nginx-service /tmp/MERGED-1538727162/v1.Service.default.app-nginx-service
--- /tmp/LIVE-2663337493/v1.Service.default.app-nginx-service   2024-06-04 08:36:06.509520740 -0500
+++ /tmp/MERGED-1538727162/v1.Service.default.app-nginx-service 2024-06-04 08:36:06.509520740 -0500
@@ -24,7 +24,7 @@
     protocol: TCP
     targetPort: 80
   selector:
-    app: app-nginx
+    app: something-else
   sessionAffinity: None
   type: NodePort
 status:
```

## Labels & Label Selectors
  - Labels go under **metadata** 
  - key:value for identifying your resource later by selecting, grouping, or filtering for it
  - Common Examples
    - `tier:frontend`
    - `app:api`
    - `env:prod`
    - `customer:acme.co`
  - **Annotations** on the other hand are used for large, non-identifying info

## Filtering the get command with  labels
  - `kubectl get pods -l app=nginx`