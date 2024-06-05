# Task Execution

A task can be executed multiple times. A [Task Execution process](/articles/TDM/tdm_architecture/03_task_execution_processes.md) can be initiated either from the TDM Portal by clicking ![task execution icon](images/execute_task_icon.png), a direct call to the [start of a task execution API](/articles/TDM/tdm_gui/TDM_Task_Execution_Flows_APIs/04_execute_task_API.md), or via a TDM Scheduling process if the task's [Scheduler](22_task_execution_timing_tab.md) is defined.

The TDM Scheduling process checks the **End Date** of the task's scheduling parameters. If the End Date is earlier than the current date, the process cleans the task's **Scheduled Execution** parameters and skips the task execution. 

## Who Can Execute a Task via the TDM Portal?

The following users can execute a TDM task:

- **Admin users**
- **Environment owners** of the task's environment:
  - **Extract tasks**, the environment owner of the source environment.
  - **Generate tasks**, the environment owner of the Synthetic environment.
  - **Load, Reserve, or Delete tasks**, the environment owner of the target environment.

- **Testers**:
  - The task's creator.
  - Other testers that are related to the same TDM Environment permission set as the task's creator:
    - **Load, Reserve, or Delete tasks**, testers that are related to the same TDM Environment permission set in the target environment as the task's creator.
    - **Extract and Generate tasks**, testers that are related to the same TDM Environment permission set in the source environment as the task's creator. 

## Task Execution Order

A TDM task can include multiple LUs with a flat or hierarchical structure and post-execution processes.

The execution of the related task's components runs in the following order:

1. [Pre-execution processes](21_task_pre_and_post_execution_processes.md), if they are added to the task. The pre-execution processes are executed according to their [execution order](04_tdm_gui_business_entity_window.md#pre-and-post-execution-processes-tabs) as defined in the task's BE. 

2. LUs - run the LUs from parent to child.  

   Click for more information about the [execution order of hierarchical LUs](/articles/TDM/tdm_overview/03_business_entity_overview.md#task-execution-of-hierarchical-business-entities).

3. [Post-execution processes](21_task_pre_and_post_execution_processes.md), if they are added to the task. The post-execution processes run after the execution of the LUs ends. The post-execution processes are executed according to their [execution order](04_tdm_gui_business_entity_window.md#pre-and-post-execution-processes-tabs) as defined in the task's BE. 

## Monitoring Task Execution

The TDM Portal displays a list of the task's LUs and pre and post-execution processes, as well as the status of the currently running processes.


**Example:**

- Execute and extract the task with the following LUs:
  - Customer - the root LU.
  - Billing - this is the children LU of the Customer LU.

- The Customer LU is executed before the Billing LU:

  ![monitor execution](images/extract_task_execution_monitor.png)

- The Billing LU is executed after the execution of the Customer LU has ended:

  ![monitor execution](images/extract_task_execution_monitor_2.png)

- The **Logical Units Execution Summary** window displays the summary execution details of each LU, pre-execution processes, and post-execution processes.



###  Open the Batch Monitoring Window

Click the information icon next to each LU to open the [Batch Monitor](/articles/20_jobs_and_batch_services/18_batch_monitor.md) window for the execution in order to get additional information and have a better tracking of the task execution. 

## Stop and Resume a Task Execution

A task can be stopped if the processed entities fail due to an error; the task can be resumed from the same point once the error has been fixed. 

- Click ![stop](images/stop_execution_icon.png)in the right corner of the **Running Execution** window to stop the execution of the running or pending task's LUs or post-execution processes, and to set the status of the task to **stopped**.

- Click ![resume](images/resume_execution_icon.png) next to a record in **stopped** execution status in the **Logical Unit Summary** to resume the execution of **all** stopped task's LUs and post-execution processes:

  

## Set a Task Execution to be On Hold

Occasionally, you may need to temporarily hold a task (i.e., set it 'On Hold'). This status can be used - for example, if the testing environment is temporarily down - for holding all task executions on an environment until the testing environment is up again, and to then reactivate the tasks for this environment.

The Hold or Activate task activities are enabled only for Active tasks. When a task is deleted (set to  'Inactive'), its task execution status cannot be modified.

Tasks on a **Hold** task-execution-status, cannot be executed.  

The Hold and Activate task buttons are displayed on the Tasks screen of each task:

- To hold a task (i.e., set it 'On Hold'/pause), click ![hold task](images/hold_task_icon.png).
- To activate a task execution status, click ![activate task icon](images/activate_onhold_task_icon.png).

### Who Can Hold or Activate a Task?

- Admin user, can hold or activate all active tasks.
- Environment owner user, can hold or activate all active tasks in their environment.
- Testers, can hold or activate their active tasks.



**Notes:**

- To execute a scheduled task on demand, click ![task execution icon](images/execute_task_icon.png). 

- Both - the TDM Portal and the TDM Scheduling process - initiate an execution request in the TDM DB. The TDM task execution process gets pending execution requests and executes the tasks.

  Click for more information about the [TDM task execution process](/articles/TDM/tdm_architecture/03_task_execution_processes.md).

- A task cannot be executed several times in parallel. An additional execution can be initiated only if the previous execution has ended.

- The TDM Scheduling process skips running tasks.

- The TDM Scheduling process skips tasks that are 'On Hold'.



  [![Previous](/articles/images/Previous.png)](25_task_tdmdb_tables.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](27_task_execution_history.md)

