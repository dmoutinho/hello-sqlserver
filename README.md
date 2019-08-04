# SQL Server Docker Image for Test

#### Run [Microsoft SQL Server](https://hub.docker.com/_/microsoft-mssql-server) Docker Image 

```sh
$ docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_PID=Developer' -p 1433:1433 -d dmoutinho/sqlserver
```
#### Check container_id

```sh
$ docker ps -a 
```

#### Test SQL Server Docker Image

```sh
$ docker exec -it <container_id|container_name> /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P Test@ndo 
```

#### [SQL Test](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker?view=sql-server-2017&pivots=cs1-bash)

```sh
USE TestDB
SELECT * FROM Inventory WHERE quantity > 152;
GO
```

#### Connection URL Sample [Microsoft SQL Server](https://docs.microsoft.com/en-us/sql/connect/jdbc/connection-url-sample?view=sql-server-2017)

```sh
String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
```

## Deploy on Kubernetes

#### Deployment

```sh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sqlserver-deployment
  labels:
    app: sqlserver
spec:
  replicas: 1
  selector:
    matchLabels:
      app: sqlserver
  template:
    metadata:
      labels:
        app: sqlserver
    spec:
      containers:
      - name: sqlserver
        image: dmoutinho/sqlserver
        ports:
        - containerPort: 1433 
```

```sh
kubectl apply -f deployment.yaml
```

#### Service [GCP](https://cloud.google.com/kubernetes-engine/docs/how-to/exposing-apps)

```sh
apiVersion: v1
kind: Service
metadata:
  name: sqlserver
spec:
  type: LoadBalancer
  selector:
    app: sqlserver
  ports:
  - protocol: TCP
    port: 1433
    targetPort: 1433 
```

```sh
kubectl apply -f sevice.yaml
```
