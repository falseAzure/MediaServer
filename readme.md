## Instructions to setup a media server on Debian 12 with Jellyfin and the Servarr stack.

### Jellyfin

1. ssh into the Debian server you want to install Jellyfin on

```
ssh xxx@192.168.100.10
```

```
sudo apt install extrepo
sudo extrepo enable jellyfin
sudo apt update
sudo apt install jellyfin
sudo service jellyfin status
sudo service jellyfin start
```

Open a Browser and go to `http://192.168.100.10:8096`
