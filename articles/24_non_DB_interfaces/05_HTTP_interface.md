# HTTP Interface

The HTTP interface type defines the connections to an HTTP/HTTPS host and it can be used by Broadway Actors.

To create a new HTTP interface, take the following steps:

<studio>

1. Go to **Project Tree** > **Shared Objects**, right-click **Interfaces**, select **New Interface** and then select **HTTP** from the **Interface Type** drop-down list to open the **New Interface** window.


   ![image](images/03_http_1.png)

2. Populate the connection's settings and click **Save**.

</studio>

<web>

1. Go to **Project Tree** > **Shared Objects**, right-click **Interfaces**, select **New Interface** and then select **HTTP** from the **Others** section to open the **New Interface** window.

2. Enter a suitable name for your new HTTP Interface and then click **Create**:

   ![image](images/03_http_1WEB.png)
   
3. Populate the connection's settings and click **Save**.
   
   ![image](images/03_http_2WEB.PNG)

</web>


### Connection Settings

<table>
<tbody>
<tr>
<td width="300pxl">&nbsp;<strong>Parameter</strong></td>
<td width="600pxl">&nbsp;<strong>Description</strong></td>
</tr>
<tr>
<td>&nbsp;<strong>Protocol Type</strong></td>
<td>&nbsp;Select between HTTP and HTTPs</td>
</tr>
<tr>
<td>&nbsp;<strong>Host</strong></td>
<td>&nbsp;Hostname or IP address of the HTTP server</td>
</tr>
<tr>
<td>&nbsp;<strong>Port</strong></td>
<td>&nbsp;Port of the HTTP server</td>
</tr>
<tr>
<td>&nbsp;<strong>Path</strong></td>
<td>&nbsp;(Optional) A specific path on the Host endpoint</td>
</tr>
<tr>
<td>&nbsp;<strong>Authentication Type</strong></td>
<td>Access authentication type. Default value = Basic.<br/>When Basic is selected, the properties shown in this window are the same as those shown in the above figure. If a different access authentication type is selected (Basic, Bearer, etc), then different properties would be shown. These differences are detailed in the below section. </td>
</tr>
<tr>
<td>&nbsp;<strong>Test Connection Valid Status</strong></td>
<td>List of HTTP response codes that can successfully pass the test connection activity. e.g. 401,404. <br/> Added for Release 6.5.3 </td>
</tr>
</tbody>
</table>


### Authentication Settings

The Fabric HTTP Interface supports various standard authentication and authorization types (aka schemas) that can be used to access external protected resources. 

Each Authentication Type (except for the **None** type) requires specific security credentials (provided by the resource provider) that are populated by the implementor into the HTTP Interface Properties and used by Fabric to authenticate remote vendor servers.  

Fabric supports the following: 

* ***Basic* HTTP Authentication** - built into the HTTP protocol. Fabric (the client) sends HTTP requests with the `Authorization` header that contains the word `Basic` followed by  \<user:password\> in base64-encoded form. This interface requires the following properties:

  * User name
  * Password

  Note: This mechanism does not provide confidentiality, hence it is usually used over HTTPS and not over HTTP.

* ***Bearer* Authentication** (aka token authentication) - an HTTP Authentication Type/schema that uses cryptic string security tokens called Bearer Tokens. Fabric (the client) sends this token in the `Authorization` header when sending requests to a resource. This interface requires the following properties:

  * token

* **OAuth Authentication** methods - the Fabric HTTP Interface supports various OAuth authentication methods. Following are their common properties:
  
  * Access Token URL - address of the authorization server providing the access token.
  * Client ID - provided by the external resource/authorized vendor. 
  * Client Secret - provided by the external resource/authorized vendor. Note that although the Client Server is encrypted and saved, it is displayed in a clear text in the Fabric Studio.
  * Scope (optional) - validates that the required actions are permitted by the authenticating server, which returns the access token's scope to the client. 
  The value of the scope parameter is expressed as a list of space-delimited, case-sensitive strings.
  * Token Timeout - requests timeout to the authorization server.
  * Access Token Additional Body Parameters - parameters that will be added to the body of the token request. Use URL standard pattern for concatenating parameters (e.g., param1-name=value1&param1-name=value2).

  Below are the supported OAuth Authentication methods and their additional properties, other than the common that are mentioned above:

    * **OAuth 2.0 Password Credentials** - an OAuth grant type flow. Fabric (the client) first interacts with an authorization server, provides a user name and password and gets an access token, which is then used for the resource server's calls. This interface requires the following properties:

       * User name 
       * Password

    * **OAuth 2.0 Password Credentials - Basic Auth Headers** - an OAuth grant type flow. It is similar to "OAuth 2.0 Password Credentials" but in this type, Fabric provides the User name and Password to the authorization server in the request header, rather than in the request body. This type is more recommended and is considered as best practice.

    * **OAuth 2.0 Client Credentials** - an OAuth grant type flow. Fabric provides the client-ID and Client-Secret to the authorization server, which returns the access token used by Fabric for the resource's server calls. This interface requires only the above base properties.

    * **OAuth 2.0 Client Credentials - Basic Auth Headers** - an OAuth grant type flow. It is similar to "OAuth 2.0 Client Credentials", however, in this type, Fabric provides the client-ID and Client-Secret to the authorization server in the request header, rather than in the request body. This type is more recommended.

If the service provider does not require authentication, select **None** in the Authentication Type.



### Example of Calling a WS via HTTP Interface in a Broadway Flow

![image](images/03_http_3.PNG)

The above Broadway flow uses an **Http** Actor to connect to the HTTP server that populates the predefined HTTP interface into the **interface** input argument. The **path** input argument must be populated by the relative path to the interface. The **params** input argument must be populated when relevant. The **format** input argument must be populated with the required output format, e.g. JSON.

For example, in order to invoke a Fabric Web Service, take the following steps:

1.  Define the HTTP interface with the relevant authentication type, e.g. *Bearer*, and set the Token value.

   ![image](images/03_http_4.PNG)

2. In a Broadway flow, use either **Http** or **HttpJson** Actor to invoke a WS. Populate the input arguments as follows:

   * Set **interface** to the predefined Http interface.

   * Set **path** to the WS, relative to the interface. For example:

     ~~~
     /api/isAlive
     ~~~

   * When the interface receives input parameters, they can be sent using the **params** input argument. Then the path will look like this:

     ~~~xml
     /api/wsCustomerSSN?
     ~~~

   * When using **Http** Actor, set **format** input argument to be the required output format, e.g. JSON.

3. Use a **JsonParser** Actor to parse the WS output.



[![Previous](/articles/images/Previous.png)](04_JMS_interface.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](06_local_file_sys.md) 
