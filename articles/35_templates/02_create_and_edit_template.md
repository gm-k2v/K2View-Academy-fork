# Creating and Editing Templates

Templates are displayed in the Fabric Studio projects tree and can be created either per LU or be part of a shared object. 

![image](images/templates_01.png)

To create a new template:

1. Go to the project tree, right click Templates and select New Template File.
2. Create the template in the working area. A best practice is to copy / paste an existing object from the project tree and to edit it as a template.
3. When saving the template, type in the template's Name and in the Target Ext. dropdown list select either: 
   -  [Broadway flow](/articles/19_Broadway/02a_broadway_flow_overview.md)
   -  [Broadway actor](/articles/19_Broadway/03_broadway_actor.md)
   -  [Graphit](/articles/15_web_services_and_graphit/17_Graphit/01_graphit_overview.md)
   -  Java
   

The Template file, saved with "template" extension, is shown in the Fabric Studio project tree and can be used to create new objects.

To edit a template open it from the Fabric studio project tree. Note that changes take affect on objects that will be created after that do not affect on existing objects that already created based on the edited template. 

 

### Expressions and Helpers

Fabric Templates are supported by the powerful [handlebarsjs](https://handlebarsjs.com/) template engine that provides numerous features including expressions and helpers: 

-  **Expressions** are used as placeholders in the template and are populated as input when creating an object. To embed an expression into a template use the `{{<expression-name>}}` syntax, for example `{{<firstname>}}`. Fabric templates offer the built-in  \_\_LU_NAME and \_\_FILE_NAME expressions that are populated by Fabric according to context.

-  **Helpers** are functions that can be used when creating objects. A number of built-in helpers are useful for applying if-else conditions and iterations within templates.  

For example:

A common TDM task is to load data from an LU into a target DB using Broadway flows. Having several tables to load, a template is used since it already contains the required stages and actors to implement this task and uses placeholders to populate the LU table and the target interface, schema and table. 
The following is part of a TDM DbLoad Actor template that contains several placeholders:

```json
{
  "name": "interface",
  "const": "{{TARGET_INTERFACE}}"
},
{
  "name": "schema",
  "const": "{{TARGET_SCHEMA}}"
},
{
  "name": "table",
  "const": "{{TARGET_TABLE}}"
}
```

When this template is used, the user populates the expressions / placeholders to create an entire flow with all required settings.




[![Previous](/articles/images/Previous.png)](01_templates_overview.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](03_using_templates.md)  

