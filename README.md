# HomeLab Starter

This guide will help you set up a home lab environment using Docker containers. We will configure several services including a reverse proxy, media server, download manager, and home automation system.

### Services
- **Nginx Proxy Manager**: A reverse proxy management system.
- **Home Assistant**: An open-source home automation platform.
- **Jellyfin**: A media server for managing and streaming your media.
- **Sonarr**: Automatically track and download all your shows episodes.
- **Prowlarr**: An indexer manager/proxy for Sonarr, Radarr, and other media managers.
- **Deluge**: A lightweight, Free Software, cross-platform BitTorrent client.
- **Bazarr**: A companion application to Sonarr and Radarr to manage and download subtitles.

## Basic Requirements
- Install ``docker`` and ``docker compose``.
- Install ``ssh`` for remote access.

Basic docker and network knowledge is recommended.

## 1. Start containers
- ``docker compose up -d``.
- see status with ``docker ps``.

### Local Ports
- nginx-proxy-manager ``81``
- homeassistant ``8123``
- jellyfin ``8096``
- sonarr ``8989``

## 2. Setup Domain and SSL
We are going to setup remote access to our homelab. If you want to use it locally, ignore these steps.
- Sign up and follow the instructions to setup your DNS on [duckdns.org](https://www.duckdns.org/).
- Open router ports ``40080`` and ``40443`` and point to server ip. If you want use others, edit the docker file.
- Open NPM with [localhost:40081](http://127.0.0.1:40081) and create SSL certs for ``yourdomain.duckdns.org`` and ``*.yourdomain.duckdns.org`` wildcard.

## 3. Setup NPM Proxy Hosts
Open nginx proxy manager admin dashboard and add proxy services by adding a ``domain``, ``forward hostname`` and ``port``. Hostname in this case are the container names because they are on the same docker network. If you decide to move services to other networks, inspect network to see the local ip.

For example domain ``jellyfin.yourdomain.duckdns.org``, hostname ``jellyfin`` and port ``8096``. Lastly Force SSL Certificate on SSL tab.

Repeat step for each service. If you want to add services outside the docker network use their local ip.
## Enjoy
Enjoy motherfucker


# Help
## Debug
### View Logs
To check logs for one service: ``docker logs -f jellyfin`` or ``docker compose logs -f jellyfin``
### Checking Docker Network Status
To inspect docker network: ``docker network inspect homelab_proxy-network`` or ``docker network ls``
### Check if a Container Can Reach Another
To enter a service container's shell: ``docker exec -it jellyfin bash`` and ``curl -I http://sonarr:8989``
### Viewing Container Resource Usage (CPU, RAM, Network, I/O)
To monitor your containers' resource usage live: ``docker stats``


## Docs and Guides
- General Tutorial of similar setup on [YouTube](https://youtu.be/qlcVx-k-02E).
- [Nginx Proxy Manager Docs](https://nginxproxymanager.com/guide/).
- [Jellyfin Docs](https://jellyfin.org/docs/). Common problems and configs.
- [Sonarr FAQ](https://wiki.servarr.com/en/sonarr/faq).
- [Deluge Guides](https://trash-guides.info/Downloaders/Deluge/) and [FAQ](https://deluge-torrent.org/faq/). Setup Labels and other configs.