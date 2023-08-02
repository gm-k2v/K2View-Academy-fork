# TDM - Reference Implementation

<a href="https://www.k2view.com/products/test-data-management/" target="_blank">TDM</a> enables users to extract Reference tables from several source environments. TDM 7.6 stores the Reference tables in a dedicated LU: TDM_Reference. Each Reference table is stored as a separate LUI. The LUI contains the following:

[LU name]|[source environment name]|[version id]|[table name]

For example:  Customer|SRCLocalDebug|ALL|DEVICESTABLE2017

This pattern enables saving different versions of a Reference table and source environment to Fabric. Lastly, TDM enables the creation and execution of TDM load tasks in order to get the Reference data from Fabric and load them into the target environment. 

Notes: 

- The TDM Reference solution is not based on [Fabric Reference tables](/articles/22_reference(commonDB)_tables/01_fabric_commonDB_overview.md).
- Previous TDM versions saved the Reference tables in Cassandra. 

A TDM implementation has the following steps:

### Step 1 - Deploy the TDM_Reference LU

Import the TDM_Reference LU and load it to Fabric.

Note **that the [Sync method](/articles/14_sync_LU_instance/04_sync_methods.md) LU property is set by default to None**, i.e. each LUI (Reference table) is synced only once. You need to edit this property in order to enable a recurring sync of the Reference table from the source environment. 

### Step 2 - Populate RefList MTable Object

The list of Reference tables available for TDM tasks is populated in the [RefList](04_fabric_tdm_library.md#reflist) MTable object. Populate the **RefList** with the list of available Reference tables for each LU. The following settings should be populated for each record:

- **lu_name** - populated by the LU name to enable a selection of the related Reference table in a TDM task based on the task's LUs.

- **ID** - populated by an auto-increment number.

- **reference_table_name** - populated by the Reference table in the source environment.

- **schema_name** - populated by the source DB schema's name that stores the Reference table.

- **interface_name** - the Reference table's source interface.

- **target_ref_table_name** - This is an optional parameter. It can be populated when the Reference table names are different in the source and target. If empty, the target table name will be taken from the **reference_table_name** field.

- **target_schema_name** - populated by the target DB schema's name that stores the Reference table.

- **target_interface_name** - the name of the Reference table's target interface. 

- **table_pk_list** - an optional setting. Populated by the list of the target's PK fields in the RefList object. These fields can be later used to customize the load flow to run an Upsert on the target Reference table.

- **truncate** - by default, the TDM runs a delete on the Reference table in the target environment before loading it. If you have permission to run a truncate on the target Reference table and you need to use the truncate instead of the delete (e.g., the target DB is Cassandra), set this indicator to true.

- **count_indicator** - is set to true, by default, for counting the number of records in the source or target, in order to monitor the task execution. Set the indicator to false, if required, in order to avoid counting the records in the target.

- **count_bf** - an optional setting. Populate this setting to run a project Broadway flow to get the count (number of records) in the source or target. 

 Click [here](/articles/09_translations/06_mtables_overview.md) for more information about MTable objects. 

### Step 3 - Create and Execute TDM Tasks

From TDM 7.6 onwards, TDM supports running a **single** task - comprised of extract and load acts - on Reference tables, i.e., the task extracts data from the source environment into Fabric and loads it into the target environment.

Note that in previous TDM versions, the extract from the source environment was not executed by the load task. The load task copied the table from Cassandra. Therefore, there was a need to run an extract task on a given table before running the load task in order to load the table into the target environment (i.e., 2 separate tasks).

[![Previous](/articles/images/Previous.png)](08_tdm_implement_delete_of_entities.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](10_tdm_generic_broadway_flows.md)





