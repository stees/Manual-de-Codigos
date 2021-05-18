- [Docker Windows](#docker-windows)
  - [Configurações gerais](#configurações-gerais)
    - [Mudando o drive do Docker logo depois de instalar](#mudando-o-drive-do-docker-logo-depois-de-instalar)
    - [Reduzindo uso de memória do processo `vmmem`](#reduzindo-uso-de-memória-do-processo-vmmem)
  - [Operações gerais](#operações-gerais)
    - [Copiando arquivo de/para container](#copiando-arquivo-depara-container)
    - [Instalando bibliotecas novas em imagem puxada pronta do Dockerhub sem editar o Dockerfile](#instalando-bibliotecas-novas-em-imagem-puxada-pronta-do-dockerhub-sem-editar-o-dockerfile)
  - [Containers](#containers)
    - [PostGIS](#postgis)
    - [Jupyter Notebook](#jupyter-notebook)

# Docker Windows
## Configurações gerais
### Mudando o drive do Docker logo depois de instalar
 - Fonte: https://stackoverflow.com/a/63752264
 - Mudando para a pasta `D:\Docker\wsl\data`
  
    ```
    wsl --list -v
    wsl --export docker-desktop-data "D:\Docker\wsl\data\docker-desktop-data.tar"
    wsl --unregister docker-desktop-data
    wsl --import docker-desktop-data "D:\Docker\wsl\data" "D:\Docker\wsl\data\docker-desktop-data.tar" --version 2
    del "D:\Docker\wsl\data\docker-desktop-data.tar"
    ```

### Reduzindo uso de memória do processo `vmmem`
 - Fonte: https://dev.to/tallesl/vmmen-process-consuming-too-much-memory-docker-desktop-273p

 - Criar arquivo `C:\Users\<username>\.wslconfig`:\
    ```
    [wsl2]
    processors=1
    memory=1GB
    ```

## Operações gerais
### Copiando arquivo de/para container
 - Fonte: https://jtemporal.com/copying-files-into-a-container/
 - Arquivo `dados.csv` para a pasta `/home/jovyan/work/` dentro do container `relaxed_hypatia`

    ```
    docker cp dados.csv relaxed_hypatia:/home/jovyan/work/dados.csv
    ```

### Instalando bibliotecas novas em imagem puxada pronta do Dockerhub sem editar o Dockerfile
 - Fonte: https://bobcares.com/blog/edit-docker-image/ (2. Create a modified image)

 - Com o container rodando, pega nome e roda:
    ```
    docker exec -it container-name bash
    ```

 - Instalar bibliotecas que estão faltando (no caso abaixo, geopandas e [dependências](https://geopandas.org/getting_started/install.html) dentro do `scipy-notebook`)
    ```
    conda install pandas fiona shapely pyproj rtree
    pip install geopandas
    pip install psycopg2
    pip install GeoAlchemy2
    pip install openpyxl
    ```

 - Sair do bash e salvar mudanças no container, depois de pegar seu ID por `docker container ls`
    ```
    exit
    docker commit container-ID image-name
    ```

## Containers
### PostGIS
 - Fonte: https://www.alexurquhart.com/post/set-up-postgis-with-docker/

 - Instalando

    ```
    docker volume create pg_data`
    docker run --name=postgis -d -e POSTGRES_USER=user -e POSTGRES_PASS=password -e POSTGRES_DBNAME=gis -e ALLOW_IP_RANGE=0.0.0.0/0 -p 5432:5432 -v pg_data:/var/lib/postgresql --restart=always kartoza/postgis:13
    ```
    
 - Adicionando extensão SFCGAL no QGIS > DB Manager > SQL Window com a [base acima já conectada](https://hub.packtpub.com/adding-postgis-layers-using-qgis-tutorial/)
    ```
    CREATE EXTENSION postgis_sfcgal;
    ```

### Jupyter Notebook
 - Fontes: 
   - https://hub.docker.com/r/jupyter/scipy-notebook
   - https://github.com/jupyter/docker-stacks

 - Rodando no diretório `G:\`
   ```
   docker run -p 8888:8888 -v "G:/":/home/jovyan/work jupyter/scipy-notebook
   ```
   
### R
 - Fonte:
  - https://hub.docker.com/r/rocker/rstudio

   ```
   docker run --rm -p 8787:8787 -e PASSWORD=yourpasswordhere rocker/rstudio
   ```
