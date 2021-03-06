**Note:** I do not condone piracy; there are many sources of torrent-downloadable media in the [public domain](https://www.publicdomaintorrents.info/)!

# make-plex-server-pi4
Repository to store scripts and docker compose files used to set up a Plex media server on my Raspberry Pi 4. Media is downloaded to the server through a torrent client that routes traffice through a VPN.

Assumed set-up is a Pi 4 (with Pi OS installed), with external drive to store media. Plex is run from a Docker container. Another Docker app holds 2 containers; a NordVPN container that routes all traffic through VPN, and a transmission container that uses this VPN container's network; downloading media to the external drive.

**Note:** A NordVPN client is assumed here, but the but the torrent client in no way relies on it - the torrent app as written here just uses the vpn container's network. Lots of images exist for openvpn clients, so feel free to fork and substitute!

## scripts

Shell scripts.

**drive-config.sh** configures the pi to automatically mount an external drive to a mount point; with the appropriate ownership for use with the docker containers.

The script assumes the mount directory must be created.

To use, amend the **MOUNTPOINT** variable to the desired directory, and replace **[UUID]** with the UUID of the external hard drive.

**install-docker.sh** installs Docker and docker-compose for building images and running containers. This uses docker's helper script, so should just run without any amendment.

## plex-app & torrent-app
2 docker compose apps.

Both compose files use the ${} syntax to substitute variables defined in a '.env' file in the same directory as the .yml file. This is to avoid sharing passwords or other information publicly (hence the .gitignore contents).

See [this guide](https://vsupalov.com/docker-arg-env-variable-guide/#the-dot-env-file-env) for more on this syntax.

## Docker Images Used
[linuxserver/transmission](https://hub.docker.com/r/linuxserver/transmission)

[linuxserver/plex](https://hub.docker.com/r/linuxserver/plex)

[bubuntux/nordvpn](https://hub.docker.com/r/bubuntux/nordvpn)
