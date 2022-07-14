# Producer Task

Use the **Producer** task to produce data to a Kafka topic.&#x20;

You can produce data to Kafka in multiple ways.&#x20;

| Method             | Description                                                                       |
| ------------------ | --------------------------------------------------------------------------------- |
| Single Record      | Produce a single message to a Kafka topic                                         |
| Batch (Chunk Size) | Produce a batch (chunk) of messages to a Kafka topic                              |
| Stream             | Produce an automated stream of messages with configurable timer options.          |
| Stream & Batch     | Produce an automated stream of batched messages with configurable timer options.  |

**Quick Links:**

* [Serialization support](producer-task.md#serialization-support)
* [Adding headers as metadata](producer-task.md#adding-headers-as-metadata)
* [Create a simple producer task](producer-task.md#create-a-simple-produce-task)
* [Create an advanced producer task](producer-task.md#create-an-advanced-produce-task)
* [Additional producer options](producer-task.md#additional-options)

## Serialization support

When you produce data to Kafka you must specify the serialization format for the record keys and values.&#x20;

Currently supported SerDes formats:

* String
* JSON
* Long
* Float
* Double
* Bytes (base64)
* Avro (Custom)&#x20;
* Avro (Schema Registry)
* Protobuf (Schema Registry)
* JSON (Schema Registry)
* MessagePack

## Create a simple producer task&#x20;

When inside the editor for a new scenario, select the **Scenario Start** button and select **Producer** from the dropdown menu.

![](<../../../.gitbook/assets/image (53).png>)

Give your task an appropriate **name**, and select the **Cluster** and **Topic** that you want to produce data to. If you do not have a Cluster configured, [add one ](../../../getting-started/connect-to-a-kafka-cluster.md)first.&#x20;

{% hint style="success" %}
**Pro Tip!** After selecting a Cluster and Topic, use **Topic Preview** to fetch the latest records from your topic
{% endhint %}

![](<../../../.gitbook/assets/image (21).png>)

Navigate to the **Data** tab to define the data you wish to produce to your Kafka topic.

Select the `Key format` and enter a key value (or leave it null).&#x20;

Select the `Value format` (for example, **JSON**) and enter your message value.

![](<../../../.gitbook/assets/image (134).png>)

Select **Save** once you have configured your message.&#x20;

Your task will now be visible on the scenario canvas.

![](<../../../.gitbook/assets/image (169).png>)

## **Adding headers as metadata**

When producing data to Kafka, you can add headers to your message.&#x20;

This can be useful if data is constantly being produced into your topic, and you want to identify messages produced via Conduktor Testing specifically.

From the **Data** tab of a Producer task, scroll down to the **Headers** section. Add your properties as key and value pairs using this module.

![](<../../../.gitbook/assets/image (170).png>)

Read more about how to use **header filters** in [Consumer](consumer-task.md) Tasks.

## Create an advanced producer task

There are additional, advanced options for producing data with special conditions.&#x20;

In this example, we will demonstrate how to produce a **stream** of **randomly generated messages**.

Add a **Producer** task to a new scenario and navigate to the **Data** tab.

Define the message value as **String,** and toggle the **Generate random data** switch.

Use the conditions:

* **Charset**: Alphanumeric
* **Length**: 10 to 20

![](<../../../.gitbook/assets/image (19).png>)

Next, scroll down and toggle the **Stream messages** button to activate streaming.

* Under **Timer Options**, enter an **Interval (ms)** value of **1000**
* Under **Stop Conditions**, enter the value **10**

{% hint style="info" %}
Under these conditions, our task will produce a record to Kafka **every second until 10 records** have been produced.&#x20;
{% endhint %}

![](<../../../.gitbook/assets/image (155).png>)

## Additional producer options

There are additional, advanced options available under the **Options** heading.&#x20;

| Option          | Description                                                                                                                                                 |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Force partition | Force producing data to a specific partition                                                                                                                |
| Compression     | <p>Compress the Kafka messages configured in your Producer task.<br><br>Compression types available:<br>- none<br>- gzip<br>- snappy<br>- lz4<br>- zstd</p> |
| Idempotence     | The producer will ensure that **exactly one** copy of each message is written in the stream                                                                 |
| Acks            | <p>Denotes the brokers that must receive the record before the write is considered successful.<br><br>Options:<br>- none<br>- leader<br>- all</p>           |

Continue to read more about [Consumer](consumer-task.md) tasks.



