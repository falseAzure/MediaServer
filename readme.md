## Instructions to setup a media server on Debian 12 with Jellyfin and the Servarr stack.

The following applications will be installed (ports):

- Jellyfin: *8096*
- Jellyseerr: *5055*
- Prowlarr: *9696*
- Sonarr: *8989*
- Radarr: *7878*
- Sabnzbd: *6789*
- qBittorent: *8080*
- Homepage: *3000*
- Gluetun

### 1. Folder structure
create shared folder: 
- create directory `downloads`:
```
mkdir -p downloads/qbittorrent/{completed,incomplete,torrents} && mkdir -p downloads/sabnzbd/{completed,intermediate,nzb,queue,tmp}
```
- create directory `movies`, `music` and `shows` under a shared folder (e.g. `mnt/nfs/media`):
```
mkdir -p /media/{movies, music shows}
```
- if you don't have permission to create a directory:
  1. check for current permissions: `ls -ld /mnt/`
  2. set ownership: `sudo chown <user>:<user> /mnt/`

### 2. Jellyfin

1. ssh into the Debian server you want to install Jellyfin on
(if ssh is not enabled install it via `sudo apt install openssh-server`).

```
ssh xxx@192.168.100.10
```

2. install Jellyfin
```
sudo apt install extrepo
sudo extrepo enable jellyfin
sudo apt update
sudo apt install jellyfin
sudo service jellyfin status
sudo service jellyfin start
```

3. initial setup (wizard)
Open a browser and go to `http://192.168.100.10:8096`
(`http://192.168.120.12:8096/web/#/wizardstart.html`)

4. log into Jellyfin to check wheter initial setup was successfull
5. setup Jellyfin
    - add libraries: movies, shows and music (under dashboard -> libraries)

### 3. Servarr Stack

#### 3.1 Docker
Install Docker using the convenience script
(if curl is not available install it via `sudo apt install curl`).

``` bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
```

Manage Docker as non root user:

```
sudo usermod -aG docker $USER
newgrp docker
```

Create and run Portainer
```
docker volume create portainer_data
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:2.21.5
```

#### 3.2 Docker Compose
move the `servarr.yaml` file into the `~/docker` folder and run:

```
docker compose -f servarr.yaml up -d
```

#### 3.3  gluetun
Check if gluetun is running:
```
docker run --rm --network=container:gluetun alpine:3.20 sh -c "apk add wget && wget -qO- https://ipinfo.io"
```
The given ip address should be different from your own.

#### 3.4 qbittorent
Check the logs in portainer for the credentials.
Login to qbittorent: `http://192.168.100.10:8096` and create a new login under options - WebUI.


#### 3.5 radarr and sonarr



