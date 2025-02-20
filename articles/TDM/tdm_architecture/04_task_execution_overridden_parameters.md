# Task Execution - Overriding Parameters

A task execution can override execution parameters by:

- setting the active environment based on the task's environments.
- setting key-value parameters on a session level.
- overriding [Globals'](/articles/08_globals/01_globals_overview.md) values on a session level.
- overriding the [Sync Mode](#overriding-the-sync-mode-on-the-task-execution) of the task execution.
- overriding additional execution parameters without changing the task itself.

### Setting Active Environments

#### Extract Tasks

The [task execution process](03_task_execution_processes.md#main-tdm-task-execution-process-tdmexecutetask-job) sets the task's environment as the [active environment](/articles/25_environments/05_set_and_list_commands.md) on the executed task.

#### Load Tasks

The [task execution process](03_task_execution_processes.md#main-tdm-task-execution-process-tdmexecutetask-job) sets the [active environment](/articles/25_environments/05_set_and_list_commands.md) as follows:

1. It first sets the task's source environment as the active environment and gets the LUI from Fabric.
2. After the LUI sync, it sets the task's target environment as the active environment and runs the delete and/or load flows on the target environment.



### Overriding Globals' Values 

A project's Global can be overridden on either a [TDM environment](/articles/TDM/tdm_gui/12_environment_globals_tab.md) or a [TDM task](/articles/TDM/tdm_gui/23_task_globals_tab.md) level.

The task execution process sets the values on the Globals on a [session level](/articles/08_globals/03_set_globals.md#how-do-i-use-the-set-command).

Note: Task-level variables have a higher priority than TDM environment-level variables. That is, if a variable (Global) is set on both - the task and the related environment levels - the task's Global value gets the higher priority.

### Overriding the Sync Mode on the Task Execution 

When executing a TDM task, set the Sync mode according to the following table:

<table width="900pxl">
<tbody>
<tr>
<td valign="top" width="150pxl">
<p><strong>Source env -&nbsp; Override Sync Mode</strong></p>
</td>
<td valign="top" width="300pxl">
<p><strong>Task - Source env - policy for fetching data</strong></p>
</td>
<td valign="top" width="150pxl">
<p><strong>Execution Sync Mode</strong></p>
</td>
<td valign="top" width="300pxl">
<p><strong>Results</strong></p>
</td>
</tr>
<tr style="height: 64px;">
<td style="height: 64px; width: 120.094px;" valign="top">
<p>Empty</p>
</td>
<td valign="top" width="300pxl">
<ul>
<li>Available data from the Test data store, new data from &lt;source env&gt;&nbsp;</li>
</ul>
</td>
<td style="height: 64px; width: 121.688px;" valign="top">
<p>On</p>
</td>
<td valign="top" width="300pxl">
<p>LUIs are synced according to their sync method. See the <a href="/articles/14_sync_LU_instance/10_sync_behavior_summary.md">Sync Behavior Summary table</a>.</p>
</td>
</tr>
<tr style="height: 64px;">
<td style="height: 64px; width: 120.094px;" valign="top">
<p>Empty</p>
</td>
<td valign="top" width="300pxl">
<ul>
<li>All data from &lt;source env&gt;</li>
</ul>
</td>
<td style="height: 64px; width: 121.688px;" valign="top">
<p>Force</p>
</td>
<td valign="top" width="300pxl">
<p>LUIs are synced from the source.</p>
</td>
</tr>
<tr>
<td style="width: 120.094px;">
<p>Empty</p>
</td>
<td style="width: 120.797px;">
<ul>
<li>Available &lt;source env&gt; data in the Test data store&nbsp;</li>
<li>Selected snapshot (version)&nbsp;</li>
</ul>
</td>
<td style="width: 121.688px;">
<p>If the task includes a delete =&gt; On</p>
<p>Else =&gt; Off</p>
</td>
<td style="width: 384.422px;">
<ul>
<li>If this is the first sync, return an error.</li>
<li>If the LUIs exist in Fabric:
<ul>
<li>Source LU tables:</li>
Get the data from Fabric.
<li>Target LU tables (populated for a delete activity):</li>
Sync the data from the target environment.</ul>
</li>
</ul>
</td>
</tr>
<tr style="height: 64px;">
<td style="height: 64px; width: 120.094px;" valign="top">
<p>Always sync</p>
</td>
<td valign="top" width="300pxl">
<ul>
<li>Available data from the Test data store, new data from &lt;source env&gt;&nbsp;</li>
</ul>
</td>
<td style="height: 64px; width: 121.688px;" valign="top">
<p>Force</p>
</td>
<td valign="top" width="300pxl">
<p>LUIs are synced from the source.</p>
</td>
</tr>
<tr style="height: 64px;">
<td style="height: 64px; width: 120.094px;" valign="top">
<p>Always sync</p>
</td>
<td valign="top" width="300pxl">
<ul>
<li>All data from &lt;source env&gt;</li>
</ul>
</td>
<td style="height: 64px; width: 121.688px;" valign="top">
<p>Force</p>
</td>
<td valign="top" width="300pxl">
<p>LUIs are synced from the source.</p>
</td>
</tr>
<tr style="height: 155px;">
<td style="height: 155px; width: 120.094px;">
<p>Do Not Sync</p>
</td>
<td style="height: 155px; width: 120.797px;">
<ul>
<li>Only the following options are available in the task:
<ul>
<li>Available &lt;source env&gt; data in the Test data store&nbsp;</li>
<li>Selected snapshot (version)&nbsp;</li>
</ul>
</li>
</ul>
</td>
<td style="height: 155px; width: 121.688px;">
<p>If the task includes a delete =&gt; On</p>
<p>Else =&gt; Off</p>
</td>
<td style="height: 155px; width: 384.422px;">
<ul>
<li>If this is the first sync, return an error.</li>
<li>If the LUIs exist in Fabric:
<ul>
<li>Source LU tables:</li>
Get the data from Fabric.
<li>Target LU tables:</li>
Sync the data from the target environment.</ul>
</li>
</ul>
</td>
</tr>
</tbody>
</table>





# Overriding Additional Task Execution Parameters

The TDM API that [starts a task execution](/articles/TDM/tdm_gui/TDM_Task_Execution_Flows_APIs/04_execute_task_API.md) can get a list of parameter-value pairs to **override the original values** of these parameters on the task execution **without changing the task data**. 

This way, various users can **use a task as a template** and change (override) the execution parameters without changing the task itself: Each user can run the task on their environment and update the execution parameter according to their needs.

TDM supports overriding the following parameters:

<table width="900pxl">
<tbody>
<tr>
<td width="225pxl">
<p><strong>Parameter Name</strong></p>
</td>
<td width="325pxl">
<p><strong>Parameter Description</strong></p>
</td>
<td width="200pxl">
<p><strong>Task Actions</strong></p>
</td>
<td width="150pxl">
<p><strong>Data Versioning </strong></p>
</td>
</tr>
<tr>
<td width="225pxl">
<p><a href="/articles/TDM/tdm_architecture/03a_task_execution_building_entity_list_on_tasks_LUs.md#entity-list">entitieslist</a></p>
</td>
<td width="225pxl">
<p>Populated by a list of <a href="/articles/TDM/tdm_overview/03_business_entity_overview.md"> Business Entity IDs </a>separated by a comma. This list can contain only one Business Entity ID when executing a task that clones a Business Entity.</p>
</td>
<td width="200pxl">
<p>All task actions except a Generate task</p>
</td>
<td width="150pxl">
<p>True/False</p>
</td>
</tr>
<tr>
<td width="225pxl">
<p><strong>sourceEnvironmentName</strong></p>
</td>
<td width="225pxl">
<p>Source environment name</p>
</td>
<td width="200pxl">
<p>Load or Extract tasks</p>
</td>
<td width="150pxl">
<p>True/False</p>
</td>
</tr>
<tr>
<td width="225pxl">
<p><strong>targetEnvironmentName</strong></p>
</td>
<td width="225pxl">
<p>Target environment name</p>
</td>
<td width="200pxl">
<p>Load, Delete, or Reserve tasks</p>
</td>
<td width="123">
<p>True/False</p>
</td>
</tr>
<tr>
<td width="223">
<p><strong>taskGlobals</strong></p>
</td>
<td width="185">
<p>A list of Global variables (task variables) and their values</p>
</td>
<td width="99">
<p>All tasks</p>
</td>
<td width="123">
<p>True/False</p>
</td>
</tr>
<tr>
<td width="223">
<p><strong>numberOfEntities<strong></p>
</td>
<td width="185">
<p>Populated with a value that limits the number of entities to be processed by the task. This parameter is relevant only if an explicit entity list was not set.</p>
</td>
<td width="99">
<p>All tasks</p>
</td>
<td width="123">
<p>False</p>
</td>
</tr>
<tr>
<td width="223">
<p><strong>dataVersionExecId</strong></p>
</td>
<td width="185">
<p>Populated with the task execution id of the selected data version. The parameter can be set on Data Versioning load tasks.</p>
</td>
<td width="99">
<p>Load task</p>
</td>
<td width="123">
<p>True</p>
</td>
</tr>
<tr>
<td width="200pxl">
<p><strong>dataVersionRetentionPeriod</strong></p>
</td>
<td width="250pxl">
<p>Populated with the retention period of the extracted data version. This parameter contains the unit (Hours, Days, Weeks&hellip;) and the value.</p>
</td>
<td>Extract task</td>
<td>True</td>
</tr>
<tr>
<td width="223">
<p><strong>reserveInd</strong></p>
</td>
<td width="185">
<p>Populated with True or False. Set to True if the task execution needs to reserve the entities on the target environment.</p>
</td>
<td width="99">
<p>Load or Reserve tasks</p>
</td>
<td width="123">
<p>Load task: True/False</p>
<p>&nbsp;</p>
<p>Reserve task: N/A</p>
</td>
</tr>
<tr>
<td width="223">
<p><strong>reserveRetention</strong></p>
</td>
<td width="185">
<p>Populated with the reservation period of the task's entities. This parameter contains the unit (Hours, Days, Weeks.) and the value.</p>
</td>
<td width="99">
<p>Load or Reserve tasks</p>
</td>
<td width="123">
<p>Load task: True/False</p>
<p>&nbsp;</p>
<p>Reserve task: N/A</p>
</td>
</tr>
<tr>
<td width="223">
<p><strong>executionNote</strong></p>
</td>
<td width="185">
<p>Free text. Adds a note to the execution.</p>
</td>
<td width="99">
<p>All tasks</p>
</td>
<td width="123">
<p>True/False</p>
</td>
</tr>
</tbody>
</table>



Note:
- TDM supports overriding the task execution parameters only when invoking the start task execution API outside the TDM Portal. **Currently, this option is not supported when executing the task using the TDM Portal.**


### Validate the Task Execution Parameters

This API validates the overridden parameters with the user's permissions on the task's environments:

#### Validate the Task Execution Parameters

- Verify that the TDM task execution processes are up and running. If the TDM task execution processes are down, the API returns an error message.
- Test the connection details of the source and target environments of the task execution if the **forced** parameter is **false**.  
- Do not enable an execution when another execution, with the same execution parameters, is already running on the task.
- Validate the task's BE and LUs with the [systems](/articles/TDM/tdm_gui/11_environment_products_tab.md) of the task execution's source and target environment.
- Verify that the user is permitted to execute the task on the task execution's source and target environment. For example, a user cannot run a [Load task](/articles/TDM/tdm_gui/17_load_task_regular_mode.md) with a [sequence replacement](/articles/TDM/tdm_gui/10_environment_roles_tab.md#replace-sequences) on environment X if he/she does not have permissions to run such a task on this environment.

##### Data Versioning (snapshot) Validations

- Data versioning extract tasks - validate the retention period to verify that it does not exceed the maximum days allowed for the tester.

##### Entity Reservation Validations

- Validate the number of reserved entities - this validation runs if the task reserves the entities whether the reservationInd parameter is set to True in the task itself or in the overridden parameters. The validation accumulates the number of entities in the task to the total number of reserved entities for the user on the target environment. If the accumulated number of reserved entities exceeds the user's permissions on the environment, the API returns an error. 
  - For example, if a user is allowed to reserve up to 70 entities in ST1 and there are 50 entities already reserved for him in ST1, he can reserve up to additional 20 entities in ST1.
- Validate the retention period to verify that the number of days does not exceed the maximum number of days allowed for the tester.

If at least one of the validations fails, the API does not start the task and returns validation errors. 

### Task Execution Process

Overriding task execution parameters does not update the task itself, but rather impacts the given task execution:

The [task execution process](/articles/TDM/tdm_architecture/03_task_execution_processes.md) gets the overridden parameters from [task_execution_override_attrs](/articles/TDM/tdm_architecture/02_tdm_database.md#task_execution_override_attrs) TDM DB table and executes the task based on the overridden parameters.




[![Previous](/articles/images/Previous.png)](03_task_execution_processes.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](06_tdmdb_cleanup_process.md)

