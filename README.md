## Basic Requirements
- Install ``docker`` and ``docker compose``.

If you want to use it just locally, do only step 1.

## 1. Start containers
``docker compose up -d``

see status with ``docker ps``

to restart use ``docker restart name-of-container``

## 2. Setup SSL with NPM
- Sign up and follow the instructions to setup your DNS on [duckdns.org](https://www.duckdns.org/).
- Open router ports ``40080`` and ``40443`` and point to server ip (NPM ports) you can change them if you want use others.
- Open NPM with [localhost:40081](http://127.0.0.1:40081) and create SSL certs for ``yourdomain.duckdns.org`` and ``*.yourdomain.duckdns.org`` wildcard.

## 3. Setup NPM Proxy Hosts
Proxy all your homelab services adding a ``domain``, ``forward hostname`` and ``port``. hostname in this case are the container names because they are on the same docker network.

For example domain ``jellyfin.yourdomain.duckdns.org``, hostname ``jellyfin`` and port ``8096``. Lastly Force SSL Certificate on SSL tab.

## Enjoy