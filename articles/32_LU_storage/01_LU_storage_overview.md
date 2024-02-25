# Logical Unit Storage Overview

A [Logical Unit (LU)](/articles/03_logical_units/01_LU_overview.md) is a blueprint holding a set of definitions / instructions used to create and maintain the data of a business entity like a customer.

Fabric can use the Cassandra DB as a default Logical Unit's [storage layer](/articles/02_fabric_architecture/01_fabric_architecture_overview.md#21-fabric-storage) where each business entity's instance is saved as a [MicroDB](/articles/01_fabric_overview/02_fabric_glossary.md#mdb--microdb) in an **entity** table (and in an **entity_chunks** table for [big LUs](03_big_lu_storage.md)) under the Cassandra ```k2view_[LU_name]_[cluster id if exists]``` keyspace.  

Below are described the additional storage types supported by Fabric.

### Storage Types

The location of a Logical Unit's permanent storage depends on the settings of the LU Schema's **Storage** property. The following storage types exist:

* **Default**, inherits storage settings in the **[fabric]** section of the **config.ini** file.
* **None**, does not store the instance in Cassandra after a GET retrieves instance data from the source DB. 
* **Cassandra**, stores LU instances in the Cassandra DB after the execution of the GET command.
* **S3**, stores LU instances in the AWS S3 Storage after the execution of the GET command. The storage connection details are defined in the **[s3_storage]** section of the **config.ini**. 
* **Azure Blob Store**, stores LU instances in the Azure Blob Store Storage after the execution of the GET command. The storage connection details are defined in the **[azure_blob_storage]** section of the **config.ini**. 
* **Google Cloud Storage**, stores LU instances in the Google Cloud Storage after the execution of the GET command. The storage connection details are defined in the **[gcs_storage]** section of the **config.ini**.

To display an LU's storage type, use the Fabric LIST command.

[Click for more information about the LIST command](/articles/16_deploy_fabric/01_deploy_Fabric_project.md#how-are-deployed-objects-reflected-in-the-fabric-server).

Note that Fabric uses the Cassandra DB as a default system management database. Therefore, changing the LU Storage from Cassandra DB to one of the above storage types doesn't replace the Fabric need for other persistent storage. 

[Click for more information about Fabric System Database](/articles/02_fabric_architecture/06_cassandra_keyspaces_for_fabric.md).

Starting Fabric 8.0 it is possible to store the business entities on PostgreSQL when the use case is mostly around querying cross entities data, you can read further here ...


[<img align="right" width="60" height="54" src="/articles/images/Next.png">](02_storage_management.md)













