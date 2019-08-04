# SQL Server Docker Image for Test

#### Run [Microsoft SQL Server](https://hub.docker.com/_/microsoft-mssql-server) Docker Image 

```sh
$ docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=Password@' -e 'MSSQL_PID=Developer' -p 1433:1433 -d mcr.microsoft.com/mssql/server:2017-latest-ubuntu
```
#### Check container_id

```sh
$ docker ps -a 
```

#### Test SQL Server Docker Image

```sh
$ docker exec -it <container_id|container_name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Password@ 
```
