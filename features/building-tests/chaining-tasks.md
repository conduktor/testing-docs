# Chaining tasks

You can chain tasks by clicking on the start node or on a **task output port**, then selecting the task type to create.&#x20;

![Consumers have 2 output ports](../../.gitbook/assets/output-ports.png)

Consumers for example have 2 output ports.&#x20;

* **on record** will trigger the next task on each record consumed. The record data will be accessible in the next task
* **on end triggers** the next task when the consumer lifecycle ends. Consumed records are not accessible to subsequent tasks

Links can be deleted by clicking on the cross icon in the middle of a line

![Deleting a link](../../.gitbook/assets/delete-link.webp)



You can create new links by drawing a line (dragging) from the output port of a task to the input port of another task.

![You can join branches easily](../../.gitbook/assets/joining.png)

You can do joins simply by having multiple parents for a task. In this case, the child task will only be triggered when each parent emitted a new event



### Accessing the output

{% hint style="warning" %}
This features requires agent version >= 0.16.0&#x20;
{% endhint %}

You can access the parent events in the child task. For example, if you chain an HTTP Request task with a Producer task, you will be able to produce data coming from the HTTP response.

{% hint style="info" %}
Looking for how to access the **current** task data in Checks ? Here is the [documentation](test-checks/accessing-kafka-message-data/)
{% endhint %}

Using the previous task data is easy, but requires some documentations until we complete the integration in the UI.



Each task defines a reference. _You can modify it, but in the current version you will need to update manually the tasks referencing it, so proceed with caution._

![](../../.gitbook/assets/reference.png)

You can no use this reference in the direct children tasks, using our JQ or Javascript inputs.

![](../../.gitbook/assets/custom-input-access.png)

Template will be added soon, with an UI-friendly way to select the corresponding parent.



The event is accessible on the following paths :&#x20;

* in JQ: \
  `.source.the_task_reference.xx` \
  ``so with our producer example you can access the record key with `.source.awesome_producer.record.key`&#x20;
* in javascript: \
  `context.source.the_task_reference.xx`

For convenience, you can copy the reference of a task on the canvas at any time :&#x20;

![You can copy the a node reference directly from the canvas](<../../.gitbook/assets/copy-ref (1).png>)





### Accessible properties per node type &#x20;

#### Kafka Consumer and Producer&#x20;

* `record.key` : the key of the record. If it is a data structure (JSON, Avro, Proto etc), you can access sub-properties directly, ex: `record.key.some_property`
* `record.value` : the value of the record, works the same way as `record.key`\
  ``A full example of accessing a record data from a child task using JQ : `.source.awesome_producer.record.value.some_property`

Record metadatas are also accessible :&#x20;

* `record.partition`
* `record.offset`
* `record.headers` : a list of `{key: string, value: string}`
* `record.timestamp`

#### Http Call

* `httpResponse.body` : The body of the response. If JSON, you can access the properties directly.\
  For example, if your task reference is `my_http` and the response is `{ "order_id": 123 }` , you can access it in the child task using the following JQ :  `.source.my_http.httpResponse.body.order_id`&#x20;
* `httpResponse.code` : the status code of the HTTP response, example: 200

Some HTTP response metadatas are also accessible:&#x20;

* `httpResponse.headers` : a list of {key: string, value: string}
* `httpResponse.responseSizeBytes`
* `httpResponse.callDurationMillis`




