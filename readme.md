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

3. Initial Setup (Wizard)
Open a Browser and go to `http://192.168.100.10:8096`
(`http://192.168.120.12:8096/web/#/wizardstart.html`)

4. Log into Jellyfin
5. Create Folder
  1. movie
7. Setup Jellyfin
  1. bla
