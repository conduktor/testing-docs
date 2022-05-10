# Task Ports

When you add a task to a scenario, you will notice there are **two ports** which can be used for **chaining** tasks together. They act as event triggers that behave in two different ways.

| Port        | Definition                                                                                                                                                                                                                                                                                                                                                      |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `END`       | <p>Chained tasks will be triggered <strong>once,</strong> when the entire task <strong></strong> has <strong>finished executing</strong>.<br><br>For example, tasks chained to the <code>END</code> port of a <a href="producer-task.md">Producer</a> that's producing x10 messages will only be executed once (when all x10 messages have been produced). </p> |
| `ON RECORD` | <p>Chained tasks will be executed <strong>for each record</strong> that's either produced or consumed. <br><br>For example, a task chained to the <code>ON RECORD</code> port of a <a href="consumer-task.md">Consumer</a> that's consuming x10 messages will be executed x10 times (for each record).</p>                                                      |

