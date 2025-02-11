# HomeLab Starter

## Basic Requirements
- Install ``docker`` and ``docker compose``.
- Install ``ssh`` for remote access.

If you want to use it locally, just do step 1.

## 1. Start containers
- ``docker compose up -d``.
- see status with ``docker ps``.
- see logs with ``docker logs -f <container-name>``.

to restart a container use ``docker restart <container-name>``. 
### Local Ports
- nginx-proxy-manager ``81``
- homeassistant ``8123``
- jellyfin ``8096``
- sonarr ``8989``

## 2. Setup Domain and SSL
- Sign up and follow the instructions to setup your DNS on [duckdns.org](https://www.duckdns.org/).
- Open router ports ``40080`` and ``40443`` and point to server ip. If you want use others, edit the docker file.
- Open NPM with [localhost:40081](http://127.0.0.1:40081) and create SSL certs for ``yourdomain.duckdns.org`` and ``*.yourdomain.duckdns.org`` wildcard.

## 3. Setup NPM Proxy Hosts
Proxy services by adding a ``domain``, ``forward hostname`` and ``port``. hostname in this case are the container names because they are on the same docker network.

For example domain ``jellyfin.yourdomain.duckdns.org``, hostname ``jellyfin`` and port ``8096``. Lastly Force SSL Certificate on SSL tab.

Repeat step for each service. If you want to add services outside the docker network use their local ip.
## Enjoy