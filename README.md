# Home Assistant - Docker mod for code-server

This mod adds Home Assistant related add-ons to code-server, to be installed/updated during container start.

In code-server docker arguments, set an environment variable `DOCKER_MODS=ghcr.io/aneisch/code-server-home-assistant:code-server-home-assistant`

Full docker-compose:

```yaml
    vscode:
        container_name: vscode
        image: linuxserver/code-server:3.12.0 # old version required as of 12/24/2022
        ports:
          - '8443:8443'
        restart: always
        volumes:
          - '/opt/vscode:/config'
          - '/opt/homeassistant/:/ha_config/homeassistant'
          - '/opt/appdaemon/:/ha_config/appdaemon'
          - '/opt/docker-compose/:/ha_config/docker-compose'
          - '/opt/github:/ha_config/github_projects'
          - '/home/aneisch/.backup:/ha_config/homeassistant-git'
        environment:
          - 'DOCKER_MODS=ghcr.io/ddyer/code-server-home-assistant'
          - 'HOMEASSISTANT_URL=http://10.0.1.22:8123'
          - PUID=1000
          - PGID=1000
          - HOMEASSISTANT_TOKEN=TOKEN_HERE
```
