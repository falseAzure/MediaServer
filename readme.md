## Instructions to setup a media server on Debian 12 with Jellyfin and the Servarr stack.

### Jellyfin

1. ssh into the Debian server you want to install Jellyfin on

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
5. create shared folder: 
  - create directory `movies`, `music` and `shows` under a shared folder (e.g. `mnt/nfs/media`): `mkdir -p mnt/nfs/media/shows mnt/nfs/media/movies mnt/nfs/media/music`
  - if you don't have permission to create a directory:
    - check for current permissions: `ls -ld /mnt/`
    - set ownership: `sudo chown <user>:<user> /mnt/`
6. setup Jellyfin
  1. add libraries: movies, shows and music (under dashboard/libraries)
