# Docker OracleDB for Beginners

Some backend engineers like Oracle DB engineers be troubled to studying DevOps. I think the build and run Dockerfile is the first step.
 #oracledatabase  #devops #docker

Ref: https://github.com/oracle/docker-images.git

1. Install Docker
1. Download LINUX.X64_193000_db_home.zip from 
https://www.oracle.com/database/technologies/oracle-database-software-downloads.html
1. Donwload code from git repogitry
    ```bash
    git clone https://github.com/oracle/docker-images.git
    cd docker-images/OracleDatabase/SingleInstance/dockerfiles/19.3.0
    ```
1. Copy downloaded install file
    ```bash
    cp "~/Downloads/LINUX.X64_193000_db_home.zip" .
    ```
1. All build informaion is described in Dockerfile
    ```bash
    cat Dockerfile
    ```
1. Build the container image
    ```bash
    docker build -t oracle/database:19.3.0-se2 --build-arg DB_EDITION=se2 .
    ```
1. List container images
    ```bash
    docker images
    ```
1. Create local directory for the container volume mount
    ```bash
    mkdir -p ~/oradata
    ```
1. run container
    * Windows
    ```powersehll
    docker run --name oracle -itd `
    -p 11521:1521 -p 15500:5500 `
    -e ORACLE_PWD=password `
    -e ORACLE_CHARACTERSET=AL32UTF8 `
    -v c:/Users/USERNAME/oradata:/opt/oracle/oradata `
    oracle/database:19.3.0-se2
    ```
    * Linux
    ```bash
    docker run --name oracle -itd \
    -p 11521:1521 -p 15500:5500 \
    -e ORACLE_PWD=password \
    -e ORACLE_CHARACTERSET=AL32UTF8 \
    -v ~\oradata:/opt/oracle/oradata \
    oracle/database:19.3.0-se2
    ```
1. List docker container processes
    ```bash
    docker ps
    ```
1. Show container information
    ```bash
    docker inspect oracle
    ```
1. Show logs
    ```bash
    docker logs oracle -f
    ```
1. If you want to jumping in  the "oracle" container, please run below command:
    ```bash
    docker exec -it oracle bash
    ```
1. Add Net service name: ORCLCDB (HOST = localhost)(PORT = 11521) to tnsnames.ora
1. Connect DB
    ```bash
    sqlplus sys@orclcdb as sysdba
    ```
1. Cleanup
    ```bash
    docker rm -f oracle
    docker rmi oracle/database:19.3.0-se2
    ```
