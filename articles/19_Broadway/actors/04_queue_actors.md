# Pub / Sub Actors

Broadway has a group of [built-in Actors](../04_built_in_actor_types.md) that manage Pub / Sub asynchronous message handling. 
These Actors belong to the **queue** category and they are:

- **Publish** Actor, publishes messages using a message provider.
- **Subscribe** Actor, subscribes to messages provided by a message provider.
- **SubscribeBatch** Actor, subscribes to messages and reads them in batches. 

Message provider types supported in Broadway are:
* Apache Kafka.
* JMS Queue and Topic by any JMS provider (for example, RabbitMQ or Active MQ).
* Broker memory (in-memory queue), a Fabric internal queue without partitions that manages messages using a key.  

### Pub / Sub Input Arguments

The **queue** category Actors enable the Pub / Sub services functionality of the supported message providers, whereby their input arguments correspond to the functionality of these message providers. Some input arguments are relevant only for Kafka and some only for JMS. For example:
-  The **key** input argument of the **Publish** Actor is relevant only for Kafka and is the key commonly used for partitioning. 
-  The **correlation_id** input argument is only used by JMS publishers. This is a unique identifier that correlates the request message and its reply. When left empty, the server generates a reply. 

Publisher and Subscriber applications must be defined in Fabric as an [Interface](/articles/05_DB_interfaces/01_interfaces_overview.md) and then be set in the Actor's **interface** input argument. 

The **topic**, **group_id** and few other input arguments have a default configuration on the interface level, thus they can be left empty in the **Subscribe** Actor. However when a value is defined in the Actor, it is used in the flow instead of the value defined in the interface. 

The **Subscribe** Actor should always listen to the same topic. The **Publish** Actor can send messages to different topics thus the **topic** argument of the Actor can be overridden during the flow.
Since Fabric 6.4.2, **Subscribe** Actor can listen to multiple topics by using regex in the **topic** argument.

Arguments not supported by the message provider can be left empty and be ignored. For example, the batch size is set by the **max_batch_records** input argument. This parameter is ignored by interfaces that do not support batches (such as JMS) which consider all batches to have a size of 1.

The message type to be processed by the Broadway Pub / Sub functionality must be aligned with the **Data type** defined on the [Interface](/articles/05_DB_interfaces/01_interfaces_overview.md) and is limited to: String, byte[], JSON, long. The message type of an in-memory broker is not limited to any specific types.

### Timeout Setting

The timeout must be defined for the **Subscribe** Actor to indicate the time to wait for a new message. If the timeout elapses, the collection ends.

The **Subscribe** Actor has two timeout related settings:
* **poll_timeout**, the time to wait for a new message or the first message in a batch. If the timeout elapses, the collection ends. If set to -1, it waits forever.
* **batch_timeout**, the duration the system waits to accumulate messages in a batch. After the first message, the system accumulates additional messages until the batch_timeout is reached or the batch is full (max_batch_records). If the timeout elapses, the system returns a batch with at least one available message and no more than the max_batch_records).

When debugging the flow, the **Subscribe** Actor waits only 1 sec to prevent the [Debug run](../25_broadway_flow_window_run_and_debug_flow.md) from getting stuck.
In a regular run, timeout can be controlled by setting it to the required elapsed time. It can also be set to -1, meaning an infinite wait for messages.

### Acknowledgement in Broadway Pub / Sub

The **Subscribe** Actor sends an acknowledgement to the Pub / Sub service for each message received:
- In a [Transaction](../23_transactions.md), the acknowledgment is performed during the Commit. 
- When not in Transaction, the acknowledgement is performed during the next received message. If the server fails after reading the message, the same message is processed again.  

### Kafka Transaction Mode

Starting from Fabric 6.4.5, the **group_id** argument can be set on the **Publish** Actor and it defines the consumer group for Kafka Transaction mode only. Thus, when the Publish Actor is a part of the transaction and its group_id argument is populated, the messages are not published to the consumer's topic with the same group_id until the transaction is completed or committed. 

It is important to make sure that the consumer's topic with the same group_id is active (up and listening) before the commit is executed on the Publisher application. Otherwise, if the consumer is activated after the transaction is committed, the consumer will receive only the last published message. 

### Pub / Sub Examples 

Check out **message-broker-pubsub.flow** for Pub / Sub examples. To do so, go to **Actions** > **Examples** in the [Main menu](../18_broadway_flow_window.md#main-menu).

The following section of the example flow shows how to publish messages to an in-memory queue using a **Publish** Actor and then reading them from a queue using the **Subscribe** Actor.

![image](../images/99_actors_04_1.PNG)



To read messages in batches, use the **SubscribeBatch** Actor and set **max_batch_records** to the required batch size.

The following example shows a Subscribe flow which includes a transaction. If a failure occurs, all messages from the beginning of the transaction are rolled back. The **Subscribe** Actor reads all the messages again when a server is up again. If the same flow does not include a transaction, only the last message is repeated after the server fails and starts again.

![image](../images/99_actors_04_3.PNG)


[![Previous](/articles/images/Previous.png)](03_parsers_actors.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](05_db_actors.md)
