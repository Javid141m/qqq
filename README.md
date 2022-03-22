# ATTSW application

## Development setup

### Compile

```
./mvnw compile
```

### Run unit tests

```
./mvnw test
```

Unit testing uses h2 in-memory database. This is done to speed up the unit testing phase.

### Run integation test

```
./mvnw -Pprod veriy
```

Integration testing runs the same unit tests (at this point in time) but against Postgres database. The lifecycle of postgres database as a docker container is managed by maven.

### Run application with H2

```
./mvnw spring-boot:run
```

### Run application with Postgres database

There will be scenarios to test manually  against a postgres database. If there is already Postgres database running elsewhere then configure the *application-**prod**.properties* in *src/main/resources* directory. Properties to change are jdbc-url, username and password.

### Start database

If you want to bring up a fresh Postgres database server then you have two easy options using docker. 

-  Using docker 
```
docker run -d -p5432:5432 -ePOSTGRES_DB=attsw -ePOSTGRES_USER=attsw -ePOSTGRES_PASSWORD=attsw postgres:10
```
*Warning: Above command binds postgres to port 5432 on the local machine. It is possible that this port is in use already. In such a case, find the process using this port and stop the process.*

- Using docker-compose

Fire the following command from the workspace directory.
```
docker-compose up -d db
```
*Warning: Above command binds postgres to port 5432 on the local machine. It is possible that this port is in use already. In such a case, find the process using this port and stop the process.*

### Start the application

```
./mvnw -Pprod spring-boot:run
```

> Option *-Pprod* is configured in maven

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=adexam&metric=alert_status)](https://sonarcloud.io/dashboard?id=adexam)

Details:

Jenkins - http://16.170.128.41:8080/job/attsw_exam/  (Username: admin/Password: admin123)
Postgres - 16.170.128.41:5432  (Username: postgres/Password: postgress)
