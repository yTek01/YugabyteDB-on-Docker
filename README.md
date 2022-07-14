# Yugabyte Cluster Database Deployment using Docker Compose file
This is a repository that shows you how to set up your Yugabyte Database using Docker Compose file.

![alt text](https://github.com/yTek01/YugabyteDB-on-Docker/blob/main/YugabyteDB.png)

1. Clone the Github repo with the docker-compose file.
```bash
git clone https://github.com/yTek01/YugabyteDB-on-Docker.git
```

2. Start the Cluster
I have included a single node in the YAML file, but you can include another node/container in the same YAML to make this a two node cluster. 

```bash
docker-compose -f ./docker-compose.Yugabyte.yaml up -d
```

3. Test the APIs
Clients can now connect to the YSQL API at localhost:5433 and the YCQL API at localhost:9042. The yb-master admin service is available at http://localhost:7000.


4. Connect to YSQL
YCQL and YSQL APIs are enabled by default on the cluster.
```bash
docker exec -it yb-tserver-n1 /home/yugabyte/bin/ysqlsh -h yb-tserver-n1
```

5. Connect to YCQL
```bash
docker exec -it yb-tserver-n1 /home/yugabyte/bin/ycqlsh yb-tserver-n1
```

6. Create Keyspaces and Tables with the CQL API. 
```bash
CREATE KEYSPACE Cassandrakeyspace; \
CREATE TABLE Cassandrakeyspace.foo(bar INT PRIMARY KEY); \
DESCRIBE Cassandrakeyspace.foo;
```

7. Copy and load the sample data into YugabyteDB
docker cp load_data.sql yb-tserver-n1:/home/yugabyte/


8. Connect to the YSQL
```bash
docker exec -it yb-tserver-n1 /home/yugabyte/bin/ysqlsh -h yb-tserver-n1
```

9. Load the data into the database.
```bash
\i load_data.sql
```

10. Connect to YSQL, with the new user and database connection. 
```bash
docker exec -it yb-tserver-n1 /home/yugabyte/bin/ysqlsh -h yb-tserver-n1 -U postgres -d dvdrental
```

* List all the tables in the dvdrental database. 
```bash
\dt
```

* Check the actors table.
```bash
SELECT * FROM public.actor;
```

