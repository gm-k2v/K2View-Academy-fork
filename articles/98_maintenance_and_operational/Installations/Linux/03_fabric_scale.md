# Fabric scale
Fabric cluster, during its lifecycle, may experience a higher load, and based on metrics like CPU usage, available memory or storage you should consider to scale out the cluster. 

By design, Fabric is built to enable a horizontal scaling out by adding more fabric nodes. Each starting-up node knows to autonomously add itself to the cluster; for example:

* Register itself to join the cluster's node list, for start getting the cluster's workload like jobs handling.
* Obtain the project deployment code.
* Obtain the master key for data encryption.

This article describes how to scale Fabric cluster on-prem, within bare-metal or virtual machine environments. Read [here](/articles/98_maintenance_and_operational/Installations/Linux/04_fabric_scale_kubernetes.md) about scaling methodology for Kubernetes deployment.

> Note: Scaling guidelines for Fabric's accompanying components, like Cassandra, are not included in this article scope. These components' scaling guidelines shall be applied according to their methodologies.



## Fabric Setup 

### Prerequisite

* Deploy the Fabric server on a VM with a network connectivity to the other servers within the cluster.
* Fabric server Installation package is the same as the one used for other existing nodes.

### Install the Package 

The following steps are similar to the standard Fabric server [installation instructions](/articles/98_maintenance_and_operational/Installations/Linux/02_Fabric_7.x.x_Setup.md).

1. Log in with the previously created user for the Fabric installation.
2. Download the package from the provided links.
3. Untar the package in the user's home folder (/opt/apps/fabric):

    ~~~bash
    tar -zxf [package name].tar.gz -C /opt/apps/fabric && source .bash_profile
    ~~~

## Configuration
Configure the new fabric node the same way you have configurated the other nodes.

### Basic configurations
Run the following command to set up the base configuration. Replace the parameters with your own environment, where IPs must be the same as the ones used for other existing nodes.

~~~bash
/opt/apps/fabric/fabric/scripts/fabric-setup.sh --cassandra_user k2admin --cassandra_password changeit --cassandra_ips 10.0.0.1,10.0.0.2,10.0.0.3  --kafka_ips 10.0.0.4,10.0.0.5,10.0.0.6 
~~~

> If the Cassandra & Kafka are hardened with SSL, add  `--ssl` to the command.

### Additional configuration

When setting up a node, you shall either configure it from scratch or duplicate the configuration files from another node. When copying the configuration files from an existing node, please consider the following:
* config.ini and iifConfig.ini: Ensure accurate passwords are inserted. Post the initial Fabric execution, passwords are encrypted, making them indecipherable to other nodes.
* jvm.options and jvm.iid_finder.options: Verify that both the keystore and truststore are present, and that their respective paths and passwords are accurate.
* node.id: If the node.id is configured, verify that the UUID is distinct or comment it out to prevent conflicts.


### Certificates
Ensure all necessary certificates are imported into the keystore and truststore as needed, according to your deployment, including:
* Cassandra SSL certificate
* Kafka SSL certificate
* SAML certificate
* Source/target data Interface certificates

## Project Files

As mentioned above, Fabric nodes obtain the project deployment from the system DB when they start up. Nevertheless, if you are using additional files in your project, such as JAR libraries, copy them to the node's Fabric home folder (e.g. $K2_HOME/ExternalJars).

## Start Fabric

To start Fabric - run:
~~~bash
/opt/apps/fabric/fabric/bin/k2fabric start
~~~

After a short while, the following message will be displayed: 
~~~
++++ Fabric is READY
~~~



## Scale In

When Fabric cluster experiences a reduction in load, you may consider to scale it in, by removing or stopping the working Fabric cluster nodes.

You can just stop the relevant node, although it is in the midst of processing jobs, as Fabric knows to reconcile, where other nodes will process these jobs. Since Fabric operates on a stateless architecture, all interactions, like web services, will function seamlessly.



For more information about an advanced setup, read below:

<ul>
   <li><a href="/articles/98_maintenance_and_operational/Installations/Linux/02_Fabric_7.x.x_Setup.md">Fabric Installation</a></li>
   <li><a href="/articles/02_fabric_architecture/05_fabric_main_configuration_files.md">Fabric main configuration files</a></li>
   <li><a href="/articles/26_fabric_security/13_user_IAM_configiration.md">SAML configiration</a></li>
   <li><a href="/articles/98_maintenance_and_operational/Hardware/2_All_Environments/03_hardware_req_for_prod.md">Hardware requirements</a></li>
</ul>
