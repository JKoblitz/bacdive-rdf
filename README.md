# BacDive Knowledge graph

## R2RML Mappings
This can be done locally or on the cluster.

Download and install [ONTOP](https://github.com/ontop/ontop/releases/download/ontop-5.2.0). Download the `.jar` file from [here](https://mvnrepository.com/artifact/org.mariadb.jdbc/mariadb-java-client/3.4.1) and drop it into the `jdbc` folder.

Prepare the `.properties` file:
```ini
jdbc.url = jdbc:mariadb://localhost:3306/bacdive_full
jdbc.user = username
jdbc.password = *****
jdbc.driver = org.mariadb.jdbc.Driver

ontop.inferDefaultDatatype=true
```

Extract the Metadata:
```bash
./ontop extract-db-metadata -p .properties -o metadata
```

Write mappings and save them into a mapping file (`mapping.ttl`).

Test your mappings by providing an [endpoint](http://localhost:8080).

```bash
./ontop endpoint -p .properties -m ../../mapping.ttl
```

## Deploying the Knowledge graph

Materialize the ONTOP Graph:

```bash
./ontop materialize -p .properties -m ../../mapping.ttl -f turtle -o ../../BacDive.ttl
```

The resulting turtle file can now be exposed (work in progress).
<!-- 
Install QLever:

```bash
pip install qlever
qlever index  
qlever start                   
qlever ui                      
``` -->
