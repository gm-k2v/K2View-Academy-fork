# Data Viewer

The Data Viewer enables you to view a [Logical Unit Instance](/articles/03_logical_units/01_LU_overview.md) database (MicroDB) tables' content, which is useful for testing and defect resolutions. As an LUI is associated to an LU, the viewing of its data is accessible from the LU context within the Studio.

<studio>

## How Do I View Data in a Logical Unit?

![image](images/Logical_Units_Tree.png)

1. Go to the **Project Tree**, click **Logical Units** and verify that the LU has a green icon, indicating that it is deployed to the debug server. If the LU has a white icon, deploy it to the debug server before running the Data Viewer on it. Do either:

   - Right-click the **LU** > **Deploy To debug**.
   - Click the **Deploy** icon, located at the top of [Fabric's Debug Panel](/articles/04_fabric_studio/01_UI_components_and_menus.md#fabric-studio-debug-panel).

2. Click on <img src="images/13_01_02%20icon%201.jpg" alt="drawing" width="25"/> next to the selected LU to open the **Data Viewer** window.

3. Set the [Sync Mode](/articles/14_sync_LU_instance/02_sync_modes.md) in the top left pane; the default Sync Mode is **ON**.

4. In the **Instance ID** field (top central pane) - enter an Instance ID (IID). 

5. Click ![image](images/13_01_02%20icon%202%20Play.jpg) **Play** to generate a new **Data Viewer file**. 
    Fabric runs the [GET LUI command](/articles/02_fabric_architecture/04_fabric_commands.md#get-lui-commands) on the debug server of the selected Instance ID. Each [sync of an LUI](/articles/14_sync_LU_instance/01_sync_LUI_overview.md) creates a new *.db SQLite file for the LU instance. The LU Instance is displayed in the Instances Tree. 

  	Note that if you set the Sync Mode to **OFF** and the Instance ID does not exist in the debug server, the following error message is displayed:
  	
  	 *Instance '[LU Name]:[Instance ID]' was not found and sync is disabled.*

6. Double-click the **Instance ID** to open the **Instances Tree** drop-down list.

<img src="images/13_01_03_Instances_tree.jpg" alt="drawing" width="225"/>

7. Click the **Instance DB file** to display its **tables** under the **Instance DB Tree**.

<img src="images/13_01_04_Instance_DB_tree.jpg" alt="drawing" width="225"/>

8. Double-click a **table** to display its data and then right-click the **table** to open a context menu with the following options: 

   a. **Show Data**, displays the table’s data.
   
   b. **Show Schema**, displays the table’s structure.
   
   c. **Show Indexes**, displays the table’s indexes, if defined.

[Click for more information about Logical Units.](/articles/03_logical_units/01_LU_overview.md)

## What Are the Data Viewer Components?

The Logical Unit Data Viewer contains the following areas and components:
* Sync Mode and Instance ID
* Instances Tree
* Instance DB Tree
* Scripting Area
* Results Pane and Toolbar

![image](images/data_viewer_window.png)

### Sync Mode and Instance ID

This area has the following components:

#### Import DB File ![image](images/13_01_06%20IMPORT%20DB%20FILE%20icon.jpg)

When clicked, it allows you to browse to an external Data Viewer file and load it. 

#### Sync Mode

Set the [Sync Mode](/articles/14_sync_LU_instance/02_sync_modes.md) for the [GET LUI command](/articles/02_fabric_architecture/04_fabric_commands.md#get-lui-commands), initiated by the execution of the Data Viewer. The options are **On**, **Off** and **Force**. The default mode is **On**.

#### Instance ID

To complete this field, do either:
* Enter a specific Instance ID value.
* Select a previously stored Instance ID from the drop-down list.
* Write a [project (java) function](/articles/07_table_population/08_project_functions.md) to generate the Instance ID. Note that this function must return a string as an output. Once you have created such function, use the function name in the Instance ID field (that is, do not enter the code that contains the function). 


  For example:


  Create an Instance ID by using the function: **fnCreateInstID**. This function takes an input value and adds 10:

  ```java
  if (i_id!=null && !i_id.isEmpty()){
	 return Integer.sum(Integer.valueOf(i_id),10)+"";
   }
  return "0";
  ```
  More complex functions can be written, of course, such as generating a random Instance ID or an Instance ID that complies with other criteria (such as certain values). 


#### Play

When the ![image](images/13_01_07%20play%20icon.jpg) icon is clicked, the data file of the Instance ID is retrieved and saved for debugging.
	
### Instances Tree
The Instance Tree area (top left) displays a tree of available data files in the following order: 
* LU
* Instance 
* Dated file name

### Instance DB Tree

The Instance DB Tree area (bottom left) displays the Table Tree, which includes: 
* **k2_delta_errors** - holds information on errors, including when each error occurred.
* **k2_main_info** - holds basic information about the LU, like the LU Name and its Instance ID.
* **k2_objects_info** - holds information for each of the objects in the selected instance.
* **k2_transactions_info** - holds basic information about each transaction (ID and timestamp).

* **Reference tables under k2_Ref** - these are displayed only as part of the Instance DB Tree, when the [reference object](/articles/03_logical_units/15_LU_schema_edit_reference_tab.md) is enabled in the LU Schema's properties.

To display the values of a table in the Tree, right-click the table and select either:
* **Show Data**, to display the table or view it in the Results pane.
* **Show Schema**, to display the table structure in the Results pane.
* **Show Indexes**, to display the table indexes in the Results pane.

### Results Pane and Toolbar
(Bottom right) Displays the data or schema requested with the row count.
 <table>
<tbody>
<tr>
	<td width="60"><p><img src="images/13_01_08%20PANE%20AND%20TOOLBAR%20icon%201.jpg" alt="" /></p></td>
<td width="274">
<p>Print results</p>
</td>
</tr>
<tr>
	<td width="60"><p><img src="images/13_01_08%20PANE%20AND%20TOOLBAR%20icon%202.jpg" alt="" /></p></td>
<td width="274">
<p>Export results as an Excel file</p>
</td>
</tr>
<tr>
	<td width="60"><p><img src="images/13_01_08%20PANE%20AND%20TOOLBAR%20icon%203.jpg" alt="" /></p></td>
<td width="274">
<p>Filter results by one or more columns</p>
</td>
</tr>
<tr>
	<td width="60"><p><img src="images/13_01_08%20PANE%20AND%20TOOLBAR%20icon%204.jpg" alt="" /></p></td>
<td width="274">
<p>Toggle groupings</p>
</td>
</tr>
<tr>
	<td width="60"><p><img src="images/13_01_08%20PANE%20AND%20TOOLBAR%20icon%205.jpg" alt="" /></p></td>
<td width="274">
<p>Toggle summaries</p>
</td>
</tr>
        <td width="60"><p><img src="images/13_01_08 PANE AND TOOLBAR icon 6.png" alt="" /></p></td>
<td width="274">
<p>Refresh view</p>
</td>
</tr>	
</tbody>
</table>



### Scripting Area
The SQL Scripting Area (upper-right pane) is used for writing and running SQL statements on a selected LUDB.

![image](images/data_viewer_scripting_area.png)


The following options are supported:
<table>
<tbody>
<tr>
<td width="200pxl" valign="top">
<p><strong>Run or Run on New Tab</strong></p>
<p><strong>&nbsp;</strong></p>
</td>
<td width="650pxl" valign="top">
<ul>
<li>Click Run to execute the given SQL statement.</li>
<li>Click Run on New Tab to open a new Results tab.</li>
</ul>
</td>
</tr>
<tr>
<td width="236" valign="top">
<p><strong>Explain query</strong></p>
</td>
<td width="368" valign="top">
<p>Description of the strategy/plan that the SQLite uses to implement a specific SQL query (e.g. SCAN TABLE).</p>
</td>
</tr>
<tr>
<td width="236" valign="top">
<p><strong>Drop-down menu of special Run options</strong></p>
</td>
<td width="368" valign="top">
<ul>
<li>On current DB file: The SQL is executed on the currently selected instance file.</li>
<li>On newest DB file for each instance: The SQL is executed on the newest instance file of each instance in the Instances Tree.</li>
<li>On selected DB files: The SQL is executed on the selected instance's files. Click and press <strong>CTRL </strong>to select the required files.</li>
<li>On all existing DB files: The SQL is executed on all files in the Instances Tree.</li>
</ul>
<p>Note that when <strong>On Newest DB file</strong> or <strong>On All Existing DB files </strong>are selected, the Rows Limit drop-down list opens, where you can define the number of results to be displayed.</p>
</td>
</tr>
<tr>
<td width="236" valign="top">
<p><strong>Save SQL to File</strong></p>
</td>
<td width="368" valign="top">
<p>Saves the current SQL statement to a file.</p>
</td>
</tr>
<tr>
<td width="236" valign="top">
<p><strong>Load SQL from File</strong></p>
</td>
<td width="368" valign="top">
<p>Retrieves an SQL statement from a file previously created in the Scripting Area.</p>
</td>
</tr>
</tbody>
</table>

### How Do I Run an SQL Statement in the Data Viewer? 

Run and execute the SQL statement from the Scripting Area on the selected DB file:
1. Enter the **SQL statement** using **SQLite syntax** into the Scripting Area. 
2. Select the **DB file** to be used to run the statement from the drop-down list. 
3. Do the following:\
    a. Click **Run** or **Run on New Tab** under the **Scripting Area**.\
    b. Press **F5** or **Ctrl + Enter**. Separate multiple queries with ‘;’.
4. View results in the **Results pane**.

### How Do I Export a Logical Unit Data File?
1. Go to the **Instances Tree** and right-click the **DB File**. 
2. Click **Export Selected DB Files** and select the **Location** and **File Name** of the exported file (LUDB format). 
3. **Save** your changes. 

### Additional (Right-Click) DB File Options
* **Open DB** - opens the **Instance DB Tree** of the selected DB files. 
* **Delete Selected DB Files** - deletes the selected **Instance DB files** from the **project folder**:
   Fabric\\[project name]\Implementation\LogicalUnits\\[LU name]\VirtualDB_Data.

**Notes**

The latest Data Viewer file can be used in the following components:

* New functions / Web Services - the latest Data Viewer is displayed in the Database's drop-down list, whereby the LU table can be invoked on the code. 
[Click for more information on How to Create a New Project Function.](/articles/07_table_population/10_creating_a_project_function.md)
* LU Schema - create a new table, based on SQL Options, to open the DB query where you can select the latest Data Viewer file. [Click for more information about Adding a Table to a Schema.](/articles/03_logical_units/09_add_table_to_a_schema.md)
* Population object / DB query - to display the latest Data Viewer file in the Database's drop-down list. [Click for more information about Creating a New Table Population.](/articles/07_table_population/03_creating_a_new_table_population.md)
* Debugging population objects. [Click for more information about Debugging a Table Population.](/articles/07_table_population/01_table_population_overview.md#debug-toolbar) 



</studio>

<web>

## How Do I View Data in a Logical Unit?

The Data Viewer is accessible via the LU Schema:

1. Go to **Project Tree** > click on **Logical Units / Data Products** 
2. Expand the relevant LU and open its **Schema**.



Studio provides 2 methods to view an LUI's data:

1. **Table Data Viewer** - provides an insight into each table's content data, easily and quickly, by navigating between the LU tables that are shown in the schema diagram.
2. **Data Viewer** - allows to build queries and execute them. This can be useful in case of a cross-table queries creation.



### Table Data Viewer

To open the Table Data Viewer, click on ![](../03_logical_units/images/web/data-viewer.svg), which appears at the Schema Editor's Toolbar. Once clicked, a panel opens at the bottom of the Schema's window.

![](images/web/01_table_data_viewer1.png)

The panel is divided into 3 main areas:

* Top bar - displays the selected table's name on the left side (the root table is displayed by default, but any table can be selected). In the middle, there are 3 action elements - the Sync Mode determines when syncing occures, the Instance ID field is for entering the unique LUI identifier, and the Execute button triggers the retrieval of the specified LUI based on the selected table, including any transformation logic, if applicable. Clicking the Execute button activates the Fabric [GET command](/articles/02_fabric_architecture/04_fabric_commands.md#get-commands), which follows the behavior of the defined Sync method.

  When the LUI is retrieved and all of its the table content is shown in the main area, additional action elements appear on the right side - filter columns and export table content to CSV. These capabilities are similar to those enabled in the [Query Builder results window](/articles/11_query_builder/03_building_and_running_an_sql_query.md#results-window).

* The main area - where the table's data are shown. This area and its capabilities - like filtering, sorting or grouping - are the same as those enabled in the [Query Builder results window](/articles/11_query_builder/03_building_and_running_an_sql_query.md#results-window).

* Bottom information bar - presents the execution status, and whether succeeded, and the number of entries/rows that are shown for the selected table (up to 1000 rows).

![](images/web/01_table_data_viewer3.png)

To view another table's content data of this LUI, simply click on it in the schema. 



The panel's height can be adjusted according to user's preferences and needs, by moving the mouse to the horizontal line that separates the Schema's window. You will then see the 4-dots symbol and the cursor will turn into a *resize* mode.

![](images/web/01_table_data_viewer2.png)

> NOTES:
>
> * Clicking on the Execute button will first save the Schema and deploy the LU, in case it was changed.
> * If you have made changes in the Schema, you should click on the Execute button again, in order to view how they affected the LUI content.
> * When changing the Sync Mode or cleaning the Instance ID field - the window is reset and the displayed content is cleared. This is done in order to avoid confusion of what is currently being displayed.



To close the Table Data Viewer panel, click on the X in its upper-right corner.



### Data Viewer

To open the Data Viewer, click on <img src="../03_logical_units/images/web/schema_data_viewer.png" style="zoom:80%;" />, which appears at the Schema Editor's Toolbar. Once clicked, a Data Viewer popup window appears.

This is similar to other Query Builder popup windows, whereas here the interface - fabric - and the schema - the current LU - are preselected and are read-only. 

The list of LU tables is already expanded within the DB Explorer on the left side. 

> The LU tables' list also includes several [built-in LU tables](/articles/06_LU_tables/01_LU_tables_overview.md#built-in-platform-lu-tables/articles/06_LU_tables/01_LU_tables_overview.md#built-in-platform-lu-tables) that contain statistical information about the specific LUI. These built-in tables are not displayed in the LU Schema. For example: 
>
> * **k2_main_info** - holds basic information about the LU, like an LU Name and an Instance ID.
> * **k2_objects_info** - holds information for each of the objects (=tables) in the selected instance. For example, what populations are used for each table, how much time it has taken to populate each table, how many records have been retrieved for each table, and how much time it has taken to load the data into Fabric.

A Sync Mode drop-down list and an Instance ID field appear in the upper-right corner.

 ![](images/web/01_table_data_viewer4.png)

Similar to the Table Data Viewer:

* The data results area, has the same capabilities as enabled in the [Query Builder results window](/articles/11_query_builder/03_building_and_running_an_sql_query.md#results-window), like filtering, sorting and grouping. 
* Bottom information bar, presents the execution status and whether succeeded, and the number of entries/rows that are shown for the selected table (up to 1000 rows).

> NOTES:
>
> * Clicking on the Execute button will first save the Schema and deploy the LU, if it was changed, before a popup is opened.
> * When changing the Sync Mode or cleaning the Instance ID field - the main results area is reset and the displayed content is cleared. This is done in order to avoid confusion of what is currently being displayed.



### Get & Sync Modes

To get information about an Instance ID, you shall specify the retrieval *mode*.

Set the [Sync Mode](/articles/14_sync_LU_instance/02_sync_modes.md) for the [GET LUI command](/articles/02_fabric_architecture/04_fabric_commands.md#get-lui-commands), initiated by the execution of the Data Viewer. The 3 Sync Mode options are **On**, **Off** and **Force**. The default mode is **On**.

Moreover, the Data Viewer provides a fourth Sync Mode, named "New", that when selected, the LU Instance is first deleted and then it is retrieved again from scratch. (Such an option also appears in Broadway Debug Population *Mode*).



</web>



[<img align="right" width="60" height="54" src="/articles/images/Next.png">](02_fabric_studio_log_files.md)

