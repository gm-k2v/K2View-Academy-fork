# Graphit Parameters

Graphit allows you to define input parameters whereby the generated documents are executed using various settings like LUIs, LU table columns and other specific parameters that require processing.

Parameters can be set when:
- Running Graphit in Debug mode in the Fabric Studio.
- Invoking Graphit directly from Swagger or another http link.
- Calling Graphit from a Web Service whereby parameters are parsed as a mapped object. 

## Graphit Window - How Do I Configure Graphit Parameters?
Click **://** in the **Graphit window** to open the **Graphit Parameters** dialog box. 

![](/articles/15_web_services_and_graphit/17_Graphit/images/38_graphit_with_parameters.PNG)

Graphit Parameters are added to support the following:
- Running Graphit from the Fabric Studio in Debug mode. The debug server on which the Graphit Web Service runs has been selected in the **User Preferences** panel, under the [**server configuration**](/articles/04_fabric_studio/04_user_preferences.md#what-is-the-purpose-of-the-server-configuration-tab) section.  
- Running a GET request for the Graphit file according to the parameters defined in the Graphit Parameters dialog box. The parameters are added to the [URL](/articles/15_web_services_and_graphit/12_Supported_Verbs_Get.md#get-based-on-graphit-file). In addition, the input parameters are displayed when invoking the Graphit file using [Swagger](/articles/15_web_services_and_graphit/09_swagger.md).

Note that if the parameters have not been added to the Graphit Parameters dialog box, you can create a POST request for the Graphit file and add the parameters in the Request body. Alternatively, you can wrap the Graphit file using a Web Service and send the parameters to the Graphit file via the Web Service. 

## How Do I Configure Parameters When Running Graphit From Fabric Studio?
When creating a Graphit file, parameters can be defined using the **${}** symbols to refer to the value that is set in the Parameters window. In this specific case, you must also define a **Debug** value in the Parameter window. If not, the response is empty.


**Example**: 
 
 The **grSql.graphit** file generates a JSON file that returns the values of the following fields:
- Customer_ID, SSN, first_name and last_name of a customer whose Instance ID = 547.  
- Date and status of Case ID = 1394.
- Generic SELECT statement that retrieves Instance 547: get Customer.${customer_id}.

The queries for the SELECT statements are:
- Select customer_id,ssn,first_name,last_name From Customer.CUSTOMER where CUSTOMER_ID = ${customer_id}.
- Select * from CASE_NOTE where case_id = ${case_id}

The following screenshot displays the Graphit file:

![](/articles/15_web_services_and_graphit/17_Graphit/images/35_graphit_with_parameters.PNG)

Before running the file, a **Debug** value is assigned to the **${customer_id}** and **${case_id}** input parameters.

![](/articles/15_web_services_and_graphit/17_Graphit/images/38_graphit_with_parameters.PNG)  

Click **Run** to see the results on the right side of the output window.

![](/articles/15_web_services_and_graphit/17_Graphit/images/39_graphit_with_parameters.PNG)

## How Do I Configure Parameters When Calling Graphit Directly From Swagger?
Add the parameters to the Parameters window to create a GET request for the Graphit file and populate the parameters in Swagger. 

Note that to execute the Graphit file, first populate the parameter's value in Swagger. The Debug values are only taken as input in Debug mode.

Example:

Using the same **grSql.graphit** Graphit file as in the previous example, in the following screenshot the **customer_id Debug** value has been left empty intentionally.

![](/articles/15_web_services_and_graphit/17_Graphit/images/40_graphit_with_parameters.PNG)

As indicated below, the two Parameters fields are marked as required.

![](/articles/15_web_services_and_graphit/17_Graphit/images/42_graphit_with_parameters.PNG)

The **customer_id=547** and **case_id=1394** values are filled in the Parameters fields. 

![](/articles/15_web_services_and_graphit/17_Graphit/images/43_graphit_with_parameters.PNG)

Note that when deleting all parameters in the Parameters dialog box together, the values in the GET section in the Swagger GUI cannot be specified but can be injected in the POST section, with a successful response upon execution.

![](/articles/15_web_services_and_graphit/17_Graphit/images/44_graphit_with_parameters.PNG)

## How Do I Configure Parameters When Invoking Graphit From a Web Service?
A Graphit file can be invoked directly or be wrapped by a WS. When wrapped by a WS, the WS sends the parameters to Graphit which then parses them accordingly when generating the XML, JSON or CSV documents. The input parameters for the Graphit file can be populated by a parameter name or by a map object.

Example:

<pre><code>Map&lt;String, Object&gt; temp = new HashMap&lt;&gt;();
temp.put("input1",1000);
temp.put("input2",2463);
return graphit("grSql2.graphit", temp);</code></pre>


This code calls the following Graphit file which uses **${input1}** and **${input2}** as parameters for the **customer_id** and **subscriber_id** to populate the JSON output with relevant invoices:
![](/articles/15_web_services_and_graphit/17_Graphit/images/46a_graphit_with_parameters.PNG)
        
        
## How Do I Parse Metadata Parameters Such as Table Names or Fields Names in Graphit SQL ?

Let's suppose you need to write a graphit file that retrieves data from a table and/or a field with dynamic names parsed from variables.
In that case you can invoke the field name as a parameters in a Graphit node defined as non-prepared SQL statement. 

For example, let's consider the following:

Parameters declaration window:
**customer_id** is defined as string and is given the value 39.

Node defined as a function:

``` var fieldName = 'customer_id' ```

Node defined as SQL non-prepared:

```select SSN from customer where ${fieldName} = ${customer_id}```


In this case, the ```${fieldName}``` variable will be given the (string) value ```'customer_id'``` while the variable ```${customer_id}``` will be given the value ```39```.
In that way, variables may be used in a graphit file (from a javascript function node) and hold the name of the field and the value to be processed to the WHERE statement.

See example in screenshot:
![](/articles/15_web_services_and_graphit/17_Graphit/images/46b_graphit_with_parameters.PNG)


In addition, rather than defining the variable ```fieldName``` within the javascript function node of your graphit file, you can define it in the java webservice that invokes the graphit file itself, and parse it as a map object as was shown in the [previous section](/articles/15_web_services_and_graphit/17_Graphit/06_using_graphit_files_with_parameters.md#how-do-i-configure-parameters-when-invoking-graphit-from-a-web-service) of this article.   





[![Previous](/articles/images/Previous.png)](/articles/15_web_services_and_graphit/17_Graphit/05_graphit_debugging.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/articles/15_web_services_and_graphit/17_Graphit/07_invoking_graphit_files.md)









