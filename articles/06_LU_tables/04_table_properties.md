# LU Table Properties

<web>

The Table Properties tab is displayed in the right pane of the Schema window, when a table is selected, or when opening a table through the Project Tree and then open its properties pane.

![](images/web_table_properties.png)



It displays a list of properties, by sections, that shall be defined for each LU table, as follows:

<table width="900pxl">
<tbody>
<tr>
  <td><h3>Section</h3>
  <td><h3>Property</h3>
  <td><h3>Description</h3>
</tr>
<tr>
<td style="vertical-align: top;"><p><strong>Query Statements Settings</strong></p></td>
<td style="vertical-align: top;">Columns Collation</td>
<td style="vertical-align: top;">
  <p>There are 3 options for getting and handling the retrieved data:</p>
    <ul>
     <li>BINARY - (default) compares the exact string in the field with the SQL statement.</li>
     <li>NOCASE - enables the Select statement to ignore upper/lower case letters when comparing text fields. For example: <br /> Select TYPE from tblExample where NAME = &lsquo;value&rsquo; returns records when the NAME field is set to either &lsquo;VALUE&rsquo; or &lsquo;value&rsquo;.</li>
     <li>RTRIM - enables the Select statement to ignore white space characters on the right side of the string when comparing text fields. For example:<br /> Select TYPE from tblExample where the NAME = &lsquo;value&rsquo; returns records that match both &lsquo;value&rsquo; and &lsquo;value&lsquo;.</li>
   </ul>
</td>
</tr>
<tr>
<td style="vertical-align: top;"></td>
<td style="vertical-align: top;">Full Text Search</td>
<td style="vertical-align: top;">
<p>When set to True, it enables the use of the MATCH Sqlite command as part of the WHERE clause of a Select statement that reads data from a Fabric table. Default = False.</p>
<p>Click for more information about the Match command:</p>
<p><a href="http://www.sqlite.org/fts3.html#section_3">http://www.sqlite.org/fts3.html#section_3</a></p>
</td>
</tr>
<tr>
<td style="vertical-align: top;"><p><strong>Sync</strong></p></td>    
<td style="vertical-align: top;"><p>Sync Method</p></td>
<td style="vertical-align: top;">
<p>There are 4 <a href="/articles/14_sync_LU_instance/04_sync_methods.md">Sync methods</a>:</p>
<ul>
<li>None</li>
<li>Inherited (default)</li>
<li>Time Interval</li>
<li>Decision Function</li>
</ul>
</td>
</tr>
<tr>
<td style="vertical-align: top;"></td>    
<td style="vertical-align: top;">Delete Mode</td>
<td style="vertical-align: top;">
    <p>This property defines the delete policy of the previous records in the LU table (populated prior to the current sync). The values are <strong>All</strong> (default value), <strong>Off</strong> or <strong>NonUpdated</strong>: </p>
        <li>All - the entire LU table is truncated before the populations are executed.</li>
        <li>Off - the previous records are not deleted.</li>
        <li>NonUpdated - deletes the previous records (created by the earlier sync) if the data no longer exists for the LUI in the source. 
       <p></p>
       <p>Click <a href="/articles/14_sync_LU_instance/04_sync_methods.md#delete-mode-and-truncate-before-sync-properties">here </a> for more information about the Delete Mode.</p>  
   <p>Notes:</p>
   <ul>
    <li>It is recommended to set the <strong>NonUpdated</strong> value when the LU table has <a href="/articles/18_fabric_cdc/01_change_data_capture_overview.md">CDC fields</a> in order to send <a href="/articles/18_fabric_cdc/03_cdc_messages.md">CDC messages</a> only for the updated records. If the Delete Mode is set to All, Fabric sends delete messages for all the truncated records and inserts messages for the newly inserted records.</li>
    <li>If the Delete Mode is NonUpdated, it is recommended to define a PK on the LU table and to set the LU table population mode to Upsert or Update in order to delete only the old data. If the LU table does not have a PK, new records are added to the LU table and all previous records are deleted.</li>
 </ul>
</td>
</tr>
<tr>
<td style="vertical-align: top;"><p><strong>Indexes</strong></p></td>    
<td style="vertical-align: top;"><p>Indexes List</p></td>    
<td style="vertical-align: top;"><p>Set table's indexes, as explained <a href="/articles/06_LU_tables/03_table_indexes.md">here </a></p></td>
</tr>
<tr>
    <td style="vertical-align: top;"><p><strong>Triggers</strong></p></td>    
    <td style="vertical-align: top;">Trigger List</td>
    <td style="vertical-align: top;"><p>Refers to <a href="/articles/07_table_population/11_4_creating_a_trigger_function.md">Trigger functions</a> that are executed when there is a change in LU table's data.</p>
<p>To add a Trigger function, click the "+" button and select the function name. Only Trigger functions are displayed.</p>
</td>
</tr>
<tr>
    <td style="vertical-align: top;"><p><strong>Data Change Indexes</strong></p></td>    
    <td style="vertical-align: top;">Columns' definitions per CDC Consumer</td>
    <td style="vertical-align: top;"><p>Refers to <a href="/articles/18_fabric_cdc/05_cdc_consumers_implementation.md">CDC Implementation Steps</a> to learn how to edit this list</p>
</td>
</tr>
</tbody>
</table> 



</web>

<studio>

The Table Properties tab is displayed in the right pane of the Table's window.


![image](images/06_04_table_properties.png)


The Properties tab displays a list of properties that must be defined for each LU table, as follows:

<table width="900pxl">
<tbody>
<tr>
<td width="200pxl">
<p><strong>Main</strong></p>
</td>
<td width="700pxl">
<p>Uneditable fields:</p>
<ul>
<li>Name - LU table name.</li>
<li>ID - generated by Fabric.</li>
</ul>
</td>
</tr>
<tr>
<td width="200pxl">
<p><h4>Instance ID Column</h4></p>
</td>
<td width="700pxl">
<p>A unique field that is used as the LU table Instance ID.</a></p>
</td>
</tr>
<tr>
<td width="200pxl">
<p><h4>Columns Collation</h4></p>
</td>
<td width="700pxl">
<p>There are 3 options:</p>
<ul>
<li>BINARY - (default) compares the exact string in the field with the SQL statement.</li>
<li>NOCASE - enables the Select statement to ignore upper/lower case letters when comparing text fields. For example: <br /> Select TYPE from tblExample where NAME = &lsquo;value&rsquo; returns records when the NAME field is set to either &lsquo;VALUE&rsquo; or &lsquo;value&rsquo;.</li>
<li>RTRIM - enables the Select statement to ignore white space characters on the right side of the string when comparing text fields. For example:<br /> Select TYPE from tblExample where the NAME = &lsquo;value&rsquo; returns records that match both &lsquo;value&rsquo; and &lsquo;value &lsquo;.</li>
</ul>
</td>
</tr>
<tr>
<td width="200pxl">
<p><h4>Full Text Search</h4></p>
</td>
<td width="700pxl">
<p>When set to True, it enables the use of the MATCH Sqlite command as part of the WHERE clause of a Select statement that reads data from a Fabric table. Default = False.</p>
<p>Click for more information about the Match command:</p>
<p><a href="http://www.sqlite.org/fts3.html#section_3">http://www.sqlite.org/fts3.html#section_3</a></p>
</td>
</tr>
<tr>
<td width="200pxl">
<p><h4>Sync Method</h4></p>
</td>
<td width="700pxl">
<p>There are 4 <a href="/articles/14_sync_LU_instance/04_sync_methods.md">Sync methods</a>:</p>
<ul>
<li>None</li>
<li>Inherited (default)</li>
<li>Time Interval</li>
<li>Decision Function</li>
</ul>
</td>
</tr>
<tr>
<td width="200pxl">
<p><h4>Delete Mode</h4></p>
</td>
<td width="700pxl">
    <p>Fabric 6.5.9 adds the Delete Mode property to the LU table. This property replaces the previous Truncate Before Sync LU table's property and defines the delete policy of the previous records in the LU table (populated prior to the current sync). The values are <strong>All</strong> (default value), <strong>Off</strong> or <strong>NonUpdated</strong>: </p>
        <li>All - the entire LU table is truncated before the populations are executed.</li>
        <li>Off - the previous records are not deleted.</li>
        <li>NonUpdated - deletes the previous records (created by the earlier sync) if the data no longer exists for the LUI in the source. 
       <p></p>
       <p>Click <a href="/articles/14_sync_LU_instance/04_sync_methods.md#delete-mode-and-truncate-before-sync-properties">here </a> for more information about the Delete Mode.</p>  
   <p>Notes:</p>
   <ul>
    <li>It is recommended to set the <strong>NonUpdated</strong> value when the LU table has <a href="/articles/18_fabric_cdc/01_change_data_capture_overview.md">CDC fields</a> in order to send <a href="/articles/18_fabric_cdc/03_cdc_messages.md">CDC messages</a> only for the updated records. If the Delete Mode is set to All, Fabric sends delete messages for all the truncated records and inserts messages for the newly inserted records.</li>
    <li>If the Delete Mode is NonUpdated, it is recommended to define a PK on the LU table and to set the <a href="/articles/07_table_population/04_table_population_properties_tab.md#target-lu-table-properties">LU table population mode</a> to Upsert or Update in order to delete only the old data. If the LU table does not have a PK, new records are added to the LU table and all previous records are deleted.</li>
 </ul>
</td>
</tr>
<tr>
<td width="200pxl">  
<p><h4>Enrichment Functions</h4></p>
</td>
<td width="700pxl">
<p>Refers to <a href="/articles/10_enrichment_function/01_enrichment_function_overview.md">Enrichment Functions</a> that are executed after all LU tables are populated.</p>
<ul>
<li>The execution order is determined on an LU level and is based on the Sync policy of the attached table. When no Enrichment function is attached - the display is &lsquo;Empty&rsquo;.</li>
<li>When one or more Enrichment functions are attached - the display is &lsquo;&lt;x&gt; enrichments&rsquo; (where &lt;x&gt; is the number of attached Enrichment functions).</li>
</ul>
<p>To select an Enrichment function, click the 3 dots next to the Enrichment functions property and select the function name. Only functions without input and output parameters are displayed.</p>
</td>
</tr>
</tr>
<tr>
<td width="200pxl">  
<p><h4>On Change</h4></p>
</td>
<td width="700pxl">
<p>Refers to <a href="/articles/07_table_population/11_4_creating_a_trigger_function.md">Trigger functions</a> that are executed when there is a change in LU table's data.</p>
<p>To select a Trigger function, click the 3 dots next to the On Change property and select the function name. Only Trigger functions are displayed.</p>
</td>
</tr>
</tbody>
</table>    


[![Previous](/articles/images/Previous.png)](03_table_indexes.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](05_business_tables.md)
