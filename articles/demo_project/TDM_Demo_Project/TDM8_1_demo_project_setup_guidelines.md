# TDM 8.1 Demo Project - Setup and Implementation Guidelines

## Databases Setup

The TDM demo project is aligned with TDM 8.1 and is based on PostgreSQL databases:

<table>
<tr>
<td><strong>Database</strong></td>
<td><strong>Source DBs (populated)</strong></td>
<td><strong>Target DBs (empty)</strong></td>
</tr>
<tr>
<td>CRM</td>
<td>CRM_DB</td>
<td>TAR_CRM_DB</td>
</tr>
<tr>
<td>Billing</td>
<td>BILLING_DB</td>
<td>TAR_BILLING_DB</td>
</tr>
<tr>
<td>Ordering</td>
<td>ORDERING_DB</td>
<td>TAR_ORDERING</td>
</tr>
<tr>
<td>Collection</td>
<td>COLLECTION_DB</td>
<td>TAR_COLLECTION</td>
</tr>
</table>

The target DBs are empty and the source DBs are populated with customers.

### Creating the Demo DBs in the Local PostgreSQL DB

There are two options:

I.

1. Download and extract **TDM_Demo_DBs.zip** file. This file contains the SQL script and the DB backup files from the **Demo DBs** directory.

2. Create the demo databases in PostgreSQL: 

   **Windows PostgreSQL Installation**

   - Go to the script's directory and open a **powershell** window. 
   - Then run the following command to run the script and create the CRM, Billing, Orders and Collection DB users and schemas on the PostgreSQL DB:

     & "[PostgreSQL DB exe file full path]" -Upostgres --host [PG ip address] --port [DB port] -f "create_resources.sql"

     **Example:** 

   ```
   & "C:\Program Files\PostgreSQL\913\bin\psql.exe" -Upostgres --host localhost --port 5432 -f "create_resources.sql"
   ```

   **Docker PostgreSQL Installation**

   - Copy the **create_resources.sql** script to the docker container:

     ```
     docker cp create_resources.sql [docker name]:path 
     ```

     - Run the script to create the Demo DBs and DB users: 	

     ```
     psql -h localhost -p 5432 -U postgres -d postgres -f /usr/local/create_resources.sql
     ```


3. Open **pgAdmin 4** and start restoring the databases from the backup files. It is recommended to check the **Clean before restore** option when restoring the backup file.

Note that TDM DB must be created in PostgreSQL as a part of the [TDM Installation](/articles/TDM/tdm_configuration/01_tdm_installation.md#create-the-tdm-postgresql-db-in-case-of-new-installation).



II.

Open the TDM demo project:

- Set the POSTGRESQL_ADMIN interface to be active.
- Open and redeploy environments to Fabric local debug server to include the **POSTGRESQL_ADMIN** interface. Set the active environment in the local debug server to the **SRC** environment.  
- Run the **createPGDBS** flow in the TDM LU in the TDM LU on Fabric local debug server. The flow creates the demo DB and Users in the PG DB. Set the **is_first_deploy** input variable to **true**.
- Run the **createAndPopulateDbs** flow in the TDM LU on Fabric local debug server. The flow creates and populates the demo DBs (CRM, Billing, Ordering and Collection). Set the **Debug** to **OFF** before running this flow. 



## Fabric Implementation

1. Open the Fabric Studio and create a new project.
2. Download the TDM Demo project export file (format **.k2export**) and import it to your project. All of the characteristics of the TDM Demo project will appear. 
3. The TDM Demo project's interfaces might need some modification, edit them if required (you might be working locally or remotely, for example).  Note that the **Server** setting must be populated by **localhost** when using local DBs or dockers for the DBs.
4. Open the DB_CASSANDRA interface, and check if the **k2masking** keyspace exits. If it does not exist, it can be created by the TDM LU deployment (deploy.flow). 
5. Edit the SRC and TAR environments: 
   - If you use a Fabric docker and a **local PG DBs**, populate the **Server** setting of the PG interfaces with **host.docker.internal**.
   - If you use a **docker** for the PG and Cassandra DBs, populate the **Server** setting with the **docker's internal IP address** (run **hostname -I** command in the docker to get the internal IP address), or **host.docker.internal**.
   - Note: if you run processes on the **local fabric debug** server and **docker DBs**, you need to populate the **Server** with **localhost**.
6. Deploy the Environments to Fabric.
7. Deploy the LUs and Web Services to Fabric. Note that you must deploy the Environments *before* running Data Viewer on the LUs since the main Target LU table sets the target ("TAR") environment to be the active environment.

##  TDM GUI Definitions

2 Options:

I.

1. Create a Customer Business Entity (BE) that includes the following LUs:
   - Customer
   - Billing
   - Orders
   - Collection

   Below is the BE's structure:

   ![Customer BE](images/Customer_demo_BE.png)

2. Create the following Systems (products):  

   - **CRM**. Attach the Customer LU to this system. You can populate the version by any String.
   - **BILLING**. Attach the Billing LU to this system. Note that the PAYMENT table of **TAR_BILLING_DB** has an additional column: PAYMENT_METHOD.  The load flow of the PAYMENT table supports two system versions - PROD and DEV - and populates a default value in PAYMENT_METHOD when the system version is 'DEV'. Add two versions to the BILLING system - PROD and DEV - to test this implementation.
   - **ORDERS**. Attach the Orders LU to this system. You can populate the version by any String.
   - **COLLECTION**. Attach the Collection LU to this system. You can populate the version by any String.

3. Create the following environments:

   - SRC:

     - Set  **Environment Type** setting to **Source**.
     - Set  **TDM Environment Name** setting to **SRC**.
     - Add the system to this environment.
     - Set the version of the BILLING system to PROD.

   - TAR:

     - Set  **Environment Type** setting to **Both** to enable running Data Versioning tasks on this environment.
     - Set  **TDM Environment Name** setting to **TAR**.
     - Add the systems (products) to this environment.
     - Set the version of the BILLING system to DEV.

​    See instructions on how to work with the TDM GUI in the following [link](/articles/TDM/tdm_gui/README.md).

II. 

Open the TDM demo project and run the **PopulateTDMDBForTesters** flow in the TDM LU in the demo project. The flow creates and populates the demo DBs and inserts records in the TDM DB to create the TDM GUI definitions.

Note: the **Synthetic** environment is automatically created by the TDM DB scripts. Attach all Systems to this environment and set the Systems version  to **synthetic**.


Now you are ready to create and execute TDM tasks based on the TDM Demo implementation.

