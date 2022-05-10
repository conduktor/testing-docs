# Insights

When you execute tests from the Testing application or via the CI runner, metrics are collected for reporting purposes. We surface these metrics via the **Insights** tab from within a [Test Scenario](building-tests/test-scenarios.md).

**Collected metrics:**

| Metric                   | Dimensions                                  | Description                                                                                                                     |
| ------------------------ | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| Passed/Failed Executions | <ul><li>Total (%)</li><li>By Date</li></ul> | Details the number of passed/failed executions.                                                                                 |
| Scenario Duration        | <ul><li>By Date</li></ul>                   | Details the end-to-end duration for the test execution.                                                                         |
| Task Duration            | <ul><li>By Task</li><li>By Date</li></ul>   | Details the duration of each [Task](building-tests/tasks/) that makes up the [Test Scenario](building-tests/test-scenarios.md). |

{% hint style="info" %}
Note that when there are more than 1 executions for an interval, the **average** time across all executions will be shown for the session and task duration.
{% endhint %}

## View Insights

From within the editor view of a Test Scenario, navigate to the **Insights tab.**

**Hover** over the series to see more granular detail. &#x20;

![](<../.gitbook/assets/image (75).png>)
