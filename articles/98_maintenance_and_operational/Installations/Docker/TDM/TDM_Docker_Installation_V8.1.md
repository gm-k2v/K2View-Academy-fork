## Docker Install Windows/MacBook/Linux

### Related Documents

[FABRIC V7.2.x DOCKER INSTALLATION](/articles/98_maintenance_and_operational/Installations/Docker/Fabric/Fabric_Full_Docker_Install_V7.2.0.md).

### Download Container Images 

Create a K2V_TDM directory and download the following into it: 

<ul>
    <li><a href="https://k2view.sharepoint.com/:w:/r/sites/KS/_layouts/15/Doc.aspx?sourcedoc=%7BAD4D11C5-FC8E-4794-AD25-B31ECE391ED4%7D&file=TDM%208.1.0_download_links.docx&action=default&mobileredirect=true">Download links</a></li>
</ul>




### Load the Images 

1. Open a CLI and navigate to the K2V_TDM directory you've created. 
2. Uncompress the files as shown (that is, load the images). 
3. Note that if the precise name of the specific image is different than shown, use the name that you downloaded. 

~~~bash
docker load -i D_K2V_PG15_MD5.tar.gz
docker load -i D_k2view_cassandra_4.1.3.tar.gz 
docker load -i D_k2view_fabric_7.2.0_218.tar.gz 
unzip compose_TDM_8.1.zip
~~~

You can see the image names by using the command **docker images**. 

### Run the Compose File 

1. Navigate to the compose folder as shown: 
~~~bash
    cd compose_TDM_8.1
~~~
Note that the TDM compose file has the following settings that are different than the regular Fabric docker compose file:

- Includes the PG docker
- Does not include the Kafka docker

2. Run the docker compose file as shown: 

~~~bash
    docker-compose up -d
~~~
3. Wait for approximately 3 minutes, then check that all the containers are up using this command
~~~bash
    docker ps
~~~


### Import and Deploy the TDM Library 

Download the TDM Library and import it to your Fabric project.

1. Define the TDM environments in Fabric studio and deploy them to Fabric.
2. Edit the Fabric project before deploying the TDM library to Fabric:
   - Edit the TDM deploy flow: edit the FabricSet actor of the Set Env stage. Populate the value of the environment key by the environment name from which the deploy.flow needs to get the Cassandra and Redis connection details.
   - New TDM  installation: edit the project as follows, to create the TDM tables on the PostgreSQL TDM DB:
     - Set the **BUILD_TDMDB Global to true** (default is false).
     - Set the  **POSTGRESQL_ADMIN interface to be active**.
     - Note that the TDM DB and user must be created in advance in the PostgreSQL DB. For more information see [TDM Installation and Initial Configuration](/articles/98_maintenance_and_operational/Installations/Linux/01_tdm_installation.md).
3. Note that the apps.json file in the TDM LU overrides the list of web applications. Edit the file in order to add additional web applications, if needed, before deploying the TDM LU. 
4. Deploy the TDM library to Fabric. The deployment of the TDM LU also deploys the TDM GUI web application to Fabric.



### Access the TDM Portal 

- You can now access TDM/Fabric from your browser using the host IP 
  http://localhost:3213
