# Shared Objects

Shared Objects can be used in all components of a Fabric project. For example, [Logical Units](/articles/03_logical_units/01_LU_overview.md), References, Web Services or processes. 

### Which Objects Can be Shared in a Fabric Project?

The following components can be shared in a Fabric project:
* [Interfaces](/articles/05_DB_interfaces/01_interfaces_overview.md) - a list of source connection details defined for the project.  
* [Java files](/articles/04_fabric_studio/09_logic_files_and_categories.md) and resource files:
  * SharedLogic.java, (default) containing all shared [Functions](/articles/07_table_population/06_table_population_transformation_rules.md#functions) from all categories, except for Product functions.
  * SharedLogic.java, per category, containing all shared [Functions](/articles/07_table_population/06_table_population_transformation_rules.md#functions) for a defined physical category. Each SharedLogic.java file is positioned under the relevant Category folder.
  * SharedGlobals.java, containing all shared [Globals](/articles/08_globals/01_globals_overview.md) in a set of global parameters. 
    Note: If a Global is defined in both a Shared Object and a specific Logical Unit, the one used is the one defined in the specific Logical Unit. Other Logical Units use the definitions in the Shared Object.
  * Resources, various files that can be saved both as part of a project and in version control.
* [Broadway](/articles/19_Broadway/01_broadway_overview.md) - set of flows that can be used for the data movement, its transformation and orchestration. A Broadway flow, defined at a Shared Objects level, may be used in any LU included in the project. 
* [Database Types/Custom Interface Types](/articles/05_DB_interfaces/10_database_types.md ) - where you can define a new database type that has a JDBC driver, which is not a part of the Product package. Additionally, you can edit product-supported database types that are used when defining interfaces.

<studio>

* [Environments](/articles/25_environments/01_environments_overview.md) - where you can define the number of environments according to your needs and also switch between environments in the same Fabric project.
* [Translations](/articles/09_translations/01_translations_overview_and_use_cases.md) - sets of translations that can be used for data transformation. A Translation defined in a Shared Objects level may be used in any LU, which is included in the project. 

</studio>

**Notes** 
* If either a function <studio>, a translation </studio> or a Broadway flow is defined both under Shared Objects and under a Logical Unit with the same name and parameters, the [Logical Unit](/articles/03_logical_units/01_LU_overview.md) function code gets priority.
* Since Shared Objects **are not** self-deployed, changes made to an item under a Shared Object, used by several components, require redeployment in order to become available.

[Click for more information about Project Structure and Creating a New Project in Fabric.](/articles/04_fabric_studio/05_creating_a_new_project.md)





<div class="studio">
<a href="/articles/04_fabric_studio/11_fabric_studio_exporting_and_importing%20a_fabric_project..html"><img onclick="popupimg(this)" src="/articles/images/Previous.png" alt="Previous"></a>
<a href="/articles/04_fabric_studio/04a_IntelliJ/01_intelliJ_overview.html"><img onclick="popupimg(this)" align="right" width="60" height="54" src="/articles/images/Next.png"></a>
</div>

<div class="web">
<a href="/articles/04_fabric_studio/09_logic_files_and_categories.html"><img onclick="popupimg(this)" src="/articles/images/Previous.png" alt="Previous"></a>
<a href="/articles/04_fabric_studio/26_web_basic_code_editing.html"><img onclick="popupimg(this)" align="right" width="60" height="54" src="/articles/images/Next.png"></a>
</div>

