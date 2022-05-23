# Changelog

### 0.12.0

#### Features:

* Improve agent resiliency in case of server disconnection (resume executions)
* Add support for [Schema References](https://docs.confluent.io/platform/current/schema-registry/serdes-develop/index.html#schema-references)&#x20;
* Set execution status to Lost after some time (in case an agent was shut down for example)
* Allow renaming tasks from the Editor view
* Allow returning to configuration from CI/CD run modal

#### Bug Fixes:

* Assertions should not result in error when the value is null
* IsNull operator may fail with null JSON
* Mark executions as error if agent is not reachable
* Platform stability improvements
* Fix Cluster displayed as "connected" when no agent is up
* Fix a bug when converting Producer task DSL to form (causing `Error in Producter: No stop condition selected` on execution)
* Fix conversion from Producer Form to DSL losing schema details
* Fix some UI alignment issues on wide screens
* Remove confusing X in Topic Preview, closing the slideout

**Known issues:**

**Other notes:**

****

### 0.11.0

#### Features:

* Agent :&#x20;
  * Add Docker release
  * Accept both environment variables and arguments to start the agent
* UI improvements
  * new Tabs component
  * Scenario name in breadcrumb now leads to Editor
  * Agent selection is now scrollable
  * Add a Manage environment button in environment select

#### Bug Fixes:

* Scenario not using Registry should not fail if registry is unreachable
* Random bytes generation failed with "Illegal character"
* Fix an issue where an assertion failure would sometimes not trigger the execution failure
* Fix agent disconnecting after a period of inactivity
* Fix back navigation in execution always going to Insight view
* Prevent using special characters for variables and environment variables



**Known issues:**

**Other notes:**

###

###

### 0.10.0 - Public Beta - 09/05/22

Initial public release enabling E2E Kafka testing scenarios. Release inclusive of the Conduktor Testing UI, and the agent micro-application enabling users to reach clusters that the host has access to securely and with isolation.

**Features:**

* ****[**Test Scenarios**](../features/building-tests/test-scenarios.md)****
  * Kafka [Producer](../features/building-tests/tasks/producer-task.md) task
    * Apply headers
    * Stream messages with elapsed time/record conditions
    * Additional options: chunk size, force partition, compression, idempotence, acks
    * [Check](../features/building-tests/test-checks/) metadata: offset, partition, timestamp, topic
  * Kafka [Consumer](../features/building-tests/tasks/consumer-task.md) task
    * Apply filters: headers, jq, schema id
    * Lifecycle conditions: x records, elapsed time
    * Check data and metadata: key, value, offset, partition, topic, timestamp
  * &#x20;[Set Variable](../features/building-tests/tasks/set-variable-task.md) task
    * Set 1 or many variables
    * Pass value from a previous task into variable
  * Task [ports](../features/building-tests/tasks/task-ports.md)
    * Chain tasks when:
      * Task completes
      * For each record (event) associated with the task
* **Clusters**
  * Reach local, private and public clusters using the [agent](../getting-started/install-the-testing-agent.md)
  * Add additional properties in your configuration
  * Schema registry support
    * No auth, basic auth, bearer token
* [**Custom Inputs**](../features/custom-inputs.md)****
  * Plain
  * Field Selection (JSON Query 'jq')
  * Template (mustache)
  * JavaScript
* ****[**DSL**](../features/dsl.md)****
  * Export/Import DSL code
  * Versioning of DSL inside the application (with restore)
  * Switch between DSL/UI when editing a [task](../features/building-tests/tasks/) or [scenario](../features/building-tests/test-scenarios.md)
* ****[**Environments**](../features/environments/)****
  * Create environments
  * Attach [variables](../features/environments/using-environment-variables.md) (Types: Cluster, String)
  * [Use](../features/environments/using-environment-variables.md) variables
* [**Insights**](../features/insights.md)****
  * Scenario level insights available
  * Metrics: Pased/Failed executions, E2E execution duration, execution time of each task
* ****[**Agent**](../getting-started/install-the-testing-agent.md)****
  * Local agent for reaching local/private clusters
  * [CI Agent](../features/ci-cd-automation.md) for executing test scenarios in build pipeline
* **Collaboration**
  * Create an organisation
  * Invite your colleagues (Manage Team)
  * Workspace data in Home dashboard (recently viewed, what's happening, execution activity)

**Bug fixes:**



**Known issues:**

* High throughput scenario executions may fail or be slow, while we are calibrating the platform for the load
* Agents may go stale and become unreachable after some time
* The DSL view of a task is missing a few features relative to the UI view, we suggest that you rely on the UI view or on the Scenario DSL view while we fix this.

**Other notes:**



