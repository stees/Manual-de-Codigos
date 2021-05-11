# Docker

## Configurações gerais
### Mudando o drive do Docker logo depois de instalar
 - Fonte: https://stackoverflow.com/a/63752264
 - Mudando para a pasta `D:\Docker\wsl\data`
  
    `wsl --list -v`\
    `wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"`\
    `wsl --unregister docker-desktop-data`\
    `wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2`

## Containers
### PostGIS
 - Fonte: https://www.alexurquhart.com/post/set-up-postgis-with-docker/

    `docker volume create pg_data`\
    `docker run --name=postgis -d -e POSTGRES_USER=user -e POSTGRES_PASS=password -e POSTGRES_DBNAME=gis -e ALLOW_IP_RANGE=0.0.0.0/0 -p 5432:5432 -v pg_data:/var/lib/postgresql --restart=always kartoza/postgis:13`
    
### Jupyter Notebook
 - Fonte: https://hub.docker.com/r/jupyter/scipy-notebook
 
    `docker pull jupyter/scipy-notebook`
