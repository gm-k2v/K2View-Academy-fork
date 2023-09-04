# Fabric Smart Proxy

Fabric Web Services are REST APIs that, among other purposes, allow external access to Logical Unit's data. The Fabric Web Services are exposed through the Fabric Web Service layer. Fabric receives multiple requests concurrently, thus the Web Service response time is highly important. 

Fabric Smart Proxy mechanism allows to redirect the Web Service calls between multiple nodes based on the configuration of the web server filters. The logic behind establishing what node should be invoked is based on a built-in hash function, which is applied on the values of the Web Service input argument as well as the parameters of the web server filters. 

One of the most common reasons for using this mechanism is the need to optimize the LUI retrieval process, in order to reduce the Web Service response time. 
When LUI data is retrieved by the Web Service, Fabric uses the cache mechanism to load an instance into the memory. As the Fabric MDB cache files are stored on a server, it is more difficult to utilize the cache in a multi-node environment. This is due to the fact that each Web Service call might be redirected to a different node and consequently the cache will be stored on different servers. As a result, when the same Web Service is invoked again for the same instance ID, the cache is most likely not going to be reused. The Smart Proxy mechanism can solve this issue by redirecting the call to the same node when the same input is received and thus reduce the Web Service response time.

The Smart Proxy mechanism is off by default. It can be applied by the setting the Web Service annotations  as explained further in this article.

## How Do I Set Up Web Server Filters?

Start from adding the ```smartProxy=true``` parameter on the WS input:

~~~java
@webService(path = "", verb = {MethodType.GET, MethodType.POST, MethodType.PUT, MethodType.DELETE}, version = "1", isRaw = false, isCustomPayload = false, produce = {Produce.XML, Produce.JSON}, elevatedPermission = false)
public static Boolean ws1(@param(smartProxy=true) String in) throws Exception {
	UserCode.log.info("here" +in);
	fabric().execute("broadway k2_ws.pub value="+in);
	return true;
}
~~~





The web server filter parameters are defined as follows:

* fabric_redirect is the process of forwarding a client from the requested URL to another URL. 
  * A CLIENT side redirect is a direct forwarding to a destination URL. The browser itself is doing the redirection. 
  * A SERVER side redirect means that the server calls the WS and returns the response (back to back).
* fabric_retry allows to define a number of redirection retries in case of a failure.
* fabric_tokens is a list of argument names to be used for redirection.
* fabric_affinity allows to define a subset of the nodes in a cluster, so that a node for redirection will be chosen from this subset rather than from the whole cluster.
* read_timeout_sec is a timeframe that defines the read timeout on the HTTP URL connection.
* connect_timeout_sec is the connection timeout to be set on the HTTP URL connection.

All the parameters can keep their default values except for the fabric_tokens parameter, whose value - token1, token2 - must be replaced with the name(s) of the input argument(s) used by the Web Services. 

For example, when a Web Service has an input parameter called **ID**, the filter should be set to:

~~~json
WEBSERVER_FILTERS=[{"class":"com.k2view.cdbms.ws.ProxyAPI", "params":{"fabric_redirect":"SERVER", "fabric_retry":"1", "fabric_tokens":"ID", "fabric_affinity":"", "read_timeout_sec":"60", "connect_timeout_sec":"60"}}]
~~~

<img src="images/web-service-proxy.png" style="zoom:80%;" />

When a Web Service has several input arguments, all of them need to be listed as the fabric_tokens value.



[![Previous](/articles/images/Previous.png)](/articles/15_web_services_and_graphit/14_rest_api_additions.md)
