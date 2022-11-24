## FABRIC v6.5.9_120-HF3 DOCKER INSTALLATION

### PREREQUISITES

These pre-requisites are for a development, training, demo, or a small Proof-of-Concept installation. You can use one of the following environments:

- **Docker CE/EE** over **CentOs/RedHat 7.9, Ubuntu 18.04** or higher
  or
- **Docker-Desktop** for Windows or Mac.

More detailed requirements for each are described below.

#### Docker over CentOs/RedHat

1. CentOS/RedHat 7.9, Ubuntu 18.04 (or higher) Operating System with latest patches, for each:

   - Modern Xeon Processor.
   - 8 Physical Cores.
   - 16 GB RAM.
   - HDD, 200GB must be available.

   **Note**: Minimum 10G RAM is required for running 1x Fabric, 1x Cassandra. We recommend that the Docker host be a physical server and not a virtual machine.
2. Install the latest Docker CE/EE version (https://docs.docker.com/engine/install/centos/ )

   **Note**: The /var/lib/docker should have at list 200GB of free memory.
3. Docker-compose must also be installed (see Docker documentation online https://docs.docker.com/compose/install/ ).
4. Enable NTP/chronyc (see https://access.redhat.com/documentation/enus/red_hat_enterprise_linux/7/html/system_administrators_guide/sect-using_chrony ).
5. Assign appropriate privileges to the k2view user, and allocate to this user at least 50GB of space as follows:

   ```bash
   ## update the k2view user home directory and password!! 
   useradd -m -d /<update the path>/k2view/ k2view passwd k2view 
   ```
6. Give the k2view user privileges to run docker & docker-compose via **SUDO**.

#### Minimum hardware requirements for Docker-Desktop

1. Windows or Mac machine with an 8 core CPU.
2. Windows or Mac machine with a minimum of 16G RAM.
3. Windows or Mac machine with minimum 120G of hard disk space.

### USING THE CONTAINER

#### Load the Container Image

1. Retrieve the latest versions of Fabric and Cassandra.
2. Retrieve the latest version of Kafka. The Kafka and configuration files can be retrieved from the following locations:

   <table style="border-collapse: collapse; width: 100%;">
   <tbody>
   <tr>
   <td style="width: 50%; height: 18px;"><strong>cassandra </strong></td>
   <td style="width: 50%; height: 18px;">https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/cassandra/3.11.12/D_k2view_cassandra_3.11.12.tar.gz 
   <br>md5: 5674945c399c58bc32b5aa49c381131fcd<br></td>
   </tr>
   <tr>
   <td style="width: 50%; height: 18px;"><strong>kafka </strong></td>
   <td style="width: 50%; height: 18px;">https://owncloud-bkp2.s3.amazonaws.com/adminoc/fabricint/kafka/5.5.1/D_k2view_kafka_5.5.1_2.tar.gz
   <br>md5: ad2c6b145e6b117ac3993b8bdbc50984</br></td>
   </tr>
   <tr>
   <td style="width: 50%; height: 18px;"><strong>fabric </strong></td>
   <td style="width: 50%; height: 18px;">https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/fabric_6.5/6.5.9/Server/fabric-6.5.9_100-HF2/D_k2view_fabric_6.5.9_100.tar.gz
   <br>md5: 4e6fcfcbe085d88341e060022fec056e</br></td>
   </tr>
   <tr>
   <td style="width: 50%; height: 18px;"><strong>docker-compose </strong></td>
   <td style="width: 50%; height: 18px;">https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/fabric_6.5/6.5.9/Server/fabric-6.5.9_100-HF2/compose_fabric_6.5.9_100-HF2.tar.gz
   <br>md5: d22d81e11a786509c7fdbb8c11c20275</br></td>
   </tr>
   </tbody>
   </table>
3. Copy all files to the k2view directory as follows:

   ```bash
   cd ~/ 
   wget https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/cassandra/3.11.12/D_k2view_cassandra_3.11.12.tar.gz
   wget https://owncloud-bkp2.s3.amazonaws.com/adminoc/fabricint/kafka/5.5.1/D_k2view_kafka_5.5.1_2.tar.gz  
   wget https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/fabric_6.5/6.5.9/Server/fabric-6.5.9_120-HF3/D_k2view_fabric_6.5.9_120.tar.gz
   wget https://owncloud-bkp2.s3.us-east-1.amazonaws.com/adminoc/fabricint/fabric_6.5/6.5.9/Server/fabric-6.5.9_120-HF3/compose_fabric_6.5.9_120-HF3.tar.gz
   ```
4. Load the Docker images as follows:

   ```bash
    docker load -i D_k2view_cassandra_3.11.12.tar.gz 
    docker load -i D_k2view_kafka_5.5.1_2.tar.gz
    docker load -i D_k2view_fabric_6.5.9_120.tar.gz 
   ```

   You can see the images names by using the command `docker image`
5. untar the Config archives as follows:

   ```bash
   tar -zxvf compose_fabric_6.5.9_120-HF3.tar.gz 
   ```

   !!! Note: open the “.env” file and update the names of the images as needed.

### RUN SINGLE FABRIC, CASSANDRA INSTANCES:

**Note:** this compose file doesn't include Kafka. if you need you can open the docker-compose.yml and un-remark it.

1. Run docker-compose as follows:

   ```bash
   cd compose_fabric_6.5.9_120-HF3
   # run:  
   docker-compose up -d 

   # or  
   sudo /usr/local/bin/docker-compose up -d  
   ```

   Cassandra and Fabric will start automatically.

## Stopping Services

1. To stop the Docker-Compose, do the following:

   ```bash
   cd compose_fabric_6.5.9_120-HF3
   #run: 
   docker-compose stop
   ```
2. To stop the Cassandra service, do the following:

   ```bah
   docker exec -u=cassandra -it cassandra bash su - cassandra 

   ## stop cassandra  
   stop-server

   ## restart cassandra  
   stop-server && cassandra
   ```
3. To stop or restart Fabric, do the following:

   ```bash
   docker exec -it fabric bash -l  
   k2fabric stop / restart  
   ```
