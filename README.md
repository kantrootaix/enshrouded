# Enshrouded

## Installation

This tutorial is a quick note for a basic installation of an enshrouded server from scratch on Rhel9 or Centos Stream 9. [This image](https://github.com/kantrootaix/enshrouded) released by mornedhels with use of **proton** or **wine**.

### Prerequisites

```bash
sudo yum update -y

sudo timedatectl set-timezone  Europe/Paris

sudo yum install -y yum-utils

sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y 
```

### Main install

```bash
sudo usermod -aG docker ${USER}
```

```bash
# Create main dir
mkdir -p ./enshrouded
```

```bash
# Write docker-compose file
vi docker-compose.yml
```

```bash
# For rootless execution of container
sudo yum -y install docker-ce-rootless-extras
```

```bash
# Add exposed ports to public zone
sudo firewall-cmd --add-port 15636-15637/udp --zone=public --permanent
```

```bash
# make container run in background while user is disconnected
loginctl enable-linger $UID
```

```bash
# Launch once to create directory tree
docker compose up -d
```

```bash
# Restart container
docker compose down && docker compose up -d
```

## Personnal customizations :

```bash
# Used for restart of container due to low profile of virtual machine
0 4 */4 * * docker compose down && docker compose up -d
```
:bangbang: Either wine or proton use a huge amount of ressources. A low profile of virtual machine (1 cpu, 4GB ram) will be enough for two simultaneous connected players, but probably not much more...