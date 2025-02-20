# Tasks

## Add/Edit a Task

A Stage is composed of one or more Tasks. Each Task performs a specific action in the fulfilment process of a Customer Request. Examples of Tasks are:

- Validating the customer’s request.
- Sending an e-mail  to the customer acknowledging registration of the request.
- Gathering the requested customer data.
- Reviewing the gathered data.
- Sending the customer the data that was requested.

To add a new Task under a specific Stage, click the Stage name on the Stage bar and access the <img src="../images/Figure_12a_new_task_icon.png" width="10%" height="10%"> option from the right. 
The Task Configuration screen is displayed. This screen includes several tabs, each providing an aspect of Task configuration.

Tasks can be divided into two primary categories: Manually executed Tasks, and Tasks configured to run automatically. An automatic Task is performed by the DPM system, while a manual Task is allocated to the Steward role and teams. 

The following tabs constitute the Task Configuration screen:
- Tasks
- Reminders
- Operations 
- Additional Info 
- Steward Inputs

![image](/articles/DPM/images/Figure_12_Add_Edit_a_Task_screen.png)

The following sections describe the properties that should be configured when defining a Task, and the different configurations of automatic and manual tasks.

## Tasks Tab

The Tasks tab includes the following configuration of parameters (a detailed description is in the table below):

- Task Name
- Role of a group assigned to the Task
- Define the Task as mandatory, when applicable
- Task start time 
- Task order
- Task deadline
- Push succeeding tasks (see below for description)
- Allow a steward to reject a task

Once the parameters are set, click **Save**. 

The following table details the options for the Task tab.

<table>
<tbody>
<tr>
<td width="90">
<p><strong>Property</strong></p>
</td>
<td width="35">
<p><strong>M/O</strong></p>
</td>
<td width="775">
<p><strong>Description</strong></p>
</td>
</tr>
<tr>
<td width="90">
<p>Task Name</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="775">
<p>The Task name identifies the Task anywhere throughout the system.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Role</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="775">
<p>The defined role of a team representing a group assigned to the Task. For manual Tasks, the Role is assigned to one of the Data Stewards’ group. For automatic Tasks, the DPM system informs the assigned role when the process fails or the deadline of the Task expired without completing the task.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Mandatory</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="775">
<p>A Task indicated as mandatory signifies the associated flow will not proceed until this Task is completed.</p>
<p>&nbsp;</p>
<p>If the Mandatory property is not marked and the Task deadline is reached,  the flow continues even if the Task has not been completed. In this case, the system marks the Task as “waived”.  If there are no further Tasks in the Request, the Request is marked as &ldquo;completed&rdquo;.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Task Start Time</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="775">
<p>This property defines when the next task in the flow should be started. There are two options:  Start the task immediately after the preceding task has completed or start the task as defined by the configurable time lag, described next. </p>
<p>The time lag configuration:</p>
 <p><img src="/articles/DPM/images/Figure_14_task_schedule.png" alt=""/</p>
<p>The configuration depends on the selected time unit:</p>
<p>If &ldquo;hour&rdquo; was selected, the user defines the minute the task starts. Once the preceding task has completed, this task will start in the defined minute of the following hour.</p>
<p>If &ldquo;day&rdquo; is selected then the hour of the day is defined.</p>
<p>The configuration of other time unit choices of &ldquo;week&rdquo;, &ldquo;month&rdquo; and &ldquo;year&rdquo; follow the same logic.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Task Order</p>
</td>
<td width="35">
<p>O</p>
</td>
<td width="775">
<p>Task Order defines the execution of the task within the defined Stage. Tasks to be executed in parallel are assigned to the same order number. The default value is 1</p>
</td>
</tr>
<tr>
<td width="90">
<p>Task Deadline</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="775">
<p>The task deadline defines the maximum time the task is expected to complete. If the task execution exceeds this deadline, the task is defined as “past due”. If the task execution exceeds this deadline, then this task is defined as &ldquo;past due&rdquo;.</p>
<p>If a Task reaches its Deadline, an email will be sent to the email address registered for the Role of the task. The configuration of the email used for this purpose is set in the Role Management screen of the Admin module.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Push Succeeding Tasks</p>
</td>
<td width="35">
<p>O</p>
</td>
<td width="775">
<p>This property relates to the overall order definitions of the tasks in the Stage. It is useful when creating a new Task in an already existing Stage and configuring this new Task to be executed before Tasks that were previously defined (given “push succeeding Tasks” is switched on), or without changing the other tasks ( whereby “push succeeding Tasks” is switched off).</p>
<p>When a task is defined to an order number already assigned to another Task, then the “push succeeding Tasks” property defines whether to push the task with the same order to be set to after the new task (pushing succeeding tasks as well), or, to only add the new Task to the same order as existing Tasks.</p>
</td>
</tr>
<tr>
<td width="90">
<p>Conditional Dependent Task</p>
</td>
<td width="35">
<p>O</p>
</td>
<td width="775">
<p>When a task is marked as &ldquo;Conditional Dependent Task&rdquo;, the task is dependent on a previous task and should be executed only if the task it depends on was not completed within the predefined time period.  When this property is switched to &ldquo;on&rdquo;, the DPM will prompt the user to define the Task it depends upon and after how many hours from the parent Task starts execution, the dependent Task begins.</p>
<p>The parent Task can be any other task from the same Stage.</p>
<p>This property is presented only if there is more than one Task in the current Stage. When this property is switched “on”, the property of “order” and “Deadline” are not relevant. Instead, the user should populate two additional properties: “Conditional Parent Task” and: Start Task After X Hours” (See details in next section).</p>
</td>
</tr>
 <tr>
<td width="90">
<p>Allow Steward Reject Task</p>
</td>
<td width="35">
<p>O</p>
</td>
<td width="775">
<p>When the &ldquo;Allow Steward Reject Task&rdquo; is switched to &ldquo;on&rdquo;, it means that when this task is being executed as part of the fulfillment process for a specific customer, the data steward can decide to reject this task instead of completing it. 
<p> When this option is selected, the DPM will prompt the user with the following option: <img src="../images/Figure_12_Rejected_task_stops_case.png" width="25%" height="25%"> that allows to define if in the scenario of this task being rejected, should the Request flow proceed to the next tasks or should the Request be stopped as a whole. </p>
</td>
</tr>
</tbody>
</table>


## Conditional Dependent Task 

When the “Conditional Dependent Task” is switched on, the Tasks Tab changes to present the properties that should be configured in this case, as shown by the next image and its corresponding table. 

 ![image](/articles/DPM/images/Figure_15_Task_configuration_Task_tab.png)

The additional configurable properties when the “Conditional Dependent Task is switched on are described as follows.

<table>
<tbody>
<tr>
<td width="85">
<p><strong>Property</strong></p>
</td>
<td width="35">
<p><strong>M/O</strong></p>
</td>
<td width="780">
<p><strong>Description</strong></p>
</td>
</tr>
<tr>
<td width="85">
<p>Conditional Parent Task</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="780">
<p>Defines the parent Task on which this current Task depends. It can be any other task from the same Stage that precedes the dependent task.</p>
</td>
</tr>
<tr>
<td width="85">
<p>Start Task After X Hours</p>
</td>
<td width="35">
<p>M</p>
</td>
<td width="780">
<p>Indicates after how many hours should the dependent Task begin following the parent task start time.</p>
</td>
</tr>
</tbody>
</table>

When a Flow including a conditional Task is executed, the conditional Task will only be executed if the Task it depends on has been “in progress” for a longer duration than is defined for the conditional Task to start. If the parent Task was completed before the determined duration, then the conditional Task is marked as “skipped” and is not executed.



[![Previous](/articles/DPM/images/Previous.png)](/articles/DPM/02_Admin_Module/04_Stages.md)[<img align="right" width="60" height="54" src="/articles/DPM/images/Next.png">](/articles/DPM/02_Admin_Module/06_Reminders.md)
