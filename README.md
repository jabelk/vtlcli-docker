# Velocity Template Language (VTL) CLI in Docker
Simple Docker wrapper for the [vtl-cli](https://github.com/plavjanik/vtl-cli)
project built by [Petr Plavjanik](https://github.com/plavjanik). It uses
existing [OpenJDK](https://openjdk.java.net/) containers on
[Dockerhub](https://hub.docker.com/_/openjdk) to create a runtime environment
for the Java app, increasing portability.

> Contact information:\
> Email:    njrusmc@gmail.com\
> Twitter:  @nickrusso42518

## Purpose
I create this wrapper mostly for network engineers who interact with
[Cisco's Digital Network Architecture Center (DNAC)](
https://www.cisco.com/c/en/us/products/cloud-systems-management/dna-center/index.html)
as it uses [VTL](https://velocity.apache.org/) for its templating system.
Not everyone has immediate write access to DNAC, and this tool is meant to
eliminate that barrier. However, the tool can be used for any other purpose.

## Installation
You have two options. In both cases, you'll need `docker` installed.

### Pull from Dockerhub
*Option not yet available, but coming soon*

Download image from dockerhub: `docker pull nickrusso42518/vtlcli-docker`

### Build from source
You'll need `git` and `docker-compose` installed as well.

1. Perform `git clone` using SSH or HTTPS.
2. Navigate to the directory: `cd vtlcli-docker`
3. Build the container: `docker-compose build`

## Usage
Follow these steps to start using the tool.

1. Create bind mount directory: `mkdir vtimount`
2. Populate `vtimount/` with files you want to access within the container.
   Normally this would be `*.yml` and `*.vtl` files.
3. Run a container and enter its shell: `docker-compose run vtlcli-docker sh`
4. View README from within the container: `cat sample/README.md`

## Sample
I've included a simple NTP configuration sample, which you can explore
here on GitHub. It generates a Cisco IOS NTP configuration based on some
simple variables, using simple VTL constructs like `if/else`, `for`, and
basic variable substitution.

```
/ # ./vtl -y sample/vars.yml sample/ntp.vtl
ntp authenticate
no ntp logging
ntp authentication-key 1 md5 secretKey111
ntp authentication-key 2 md5 secretKey222
ntp server 192.0.2.1 key 1
ntp server 192.0.2.2 key 2
```