# TDM Environments Overview

The TDM can create tasks that are executed in TDM environments. Each environment reflects a physical environment such as a production environment or a testing environment. In addition, the TDM has a **dummy environment** named **Synthetic** to support the generation of [synthetic entities](16a_generate_task.md) by TDM tasks. 
Each environment must be defined in the following TDM components:

- Fabric - set the [interfaces connection details and Globals values](/articles/25_environments/01_environments_overview.md) for each environment. 
- TDM Portal - set the following for each environment:

  - [General information](08_environment_window_general_information.md) such as environment name, contact person, environment type (source, target or both).
  - [Environment owners](08_environment_window_general_information.md#environment-owners) - add environment owners to set up and maintain an environment.
  - [Environment systems](11_environment_products_tab.md) - attach [TDM systems (products)](05_tdm_gui_product_window.md) to each environment.
  - [Environment permissions](10_environment_roles_tab.md) - define the permission sets with TDM permissions for environments and attach [users](02_tdm_gui_user_types.md) to an environment, enabling them to create TDM tasks for it.
  - [Environment Variables](12_environment_globals_tab.md) - override Fabric Globals' values in a TDM environment.

The TDM environments created in the TDM portal are saved in the TDM DB. 
Note that the Synthetic environment is automatically created in the TDM DB by the create/upgrade TDM DB scripts.  

Click to read more about [TDM environment setup in Fabric](/articles/TDM/tdm_implementation/tdm_fabric_implementation_environments_setup.md).



## Environments List Window

The **Environments** window displays a list of all environments defined in the TDM. Only **Admin users** can create, add or remove environment owners or delete an environment. Environment owners can edit their environment. Other users can open environments for viewing purposes only.

-   To create a new environment, click **New Environment**.
-   To open a selected environment, click the environment's **Name**.
-   To delete an environment, click<img src="images/delete_icon.png" alt="delete" style="zoom:80%;" />in the Environment window.



## Environment Window

The Environment window has the following sections:

- [General Information](08_environment_window_general_information.md)

- [Environment Summary](09_environment_window_summary_section.md)

- Environment tabs, [Permission Sets](10_environment_roles_tab.md), [Systems](11_environment_products_tab.md) and [Environment Variables](12_environment_globals_tab.md)

 The following image is an example of an Environment window:

  ![environment](images/tdm_environment_window.png)



  [![Previous](/articles/images/Previous.png)](06_be_product_tdmdb_tables.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](08_environment_window_general_information.md)
