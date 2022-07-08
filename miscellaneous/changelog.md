# Changelog

## 0.15.0 - 07/07/22

**Features:**

* HTTP task type added for use in Test Scenarios
* Enable retry of HTTP requests until conditions are met
* Check HTTP response data (Status code, Body, Headers, Response time, Response size)
* New 'Template (Mustache)' editor that improves the UX and also adds support for functions and contextual, macro-generated data. E.g. randomIp, randomEmail, randomTimestamp

**Bug fixes:**

* Fix bug impacting form display when resizing the slideout
* Fix bug causing environment/agent selection showing behind slideout form
* Fix bug causing newly created agent to not show in list
* Fix bug when returning from execution details
* Fix typo on command used to download agent on Windows that caused it to fail
* Onboarding module display bug

**Other notes:**

* Update send feedback link with new URL

## 0.14.0 - 20/06/22

**Features:**

* Add time & offset-based strategies for Consumer tasks (e.g. consume from yesterday, consume from offset x)
* Redesign of Test Suite details page
* Add navigation to run suite history via new 'Runs' tab from within a Test Suite
* Align schema preview header style with topic preview

**Bug fixes:**

* Fix issue impacting cluster configuration updates

**Other notes:**

* Fetch agent connectivity state for focused page only (i.e. restrict if a user has multiple tabs open) &#x20;

## 0.13.3 - 14/06/22

**Bug fixes:**

* Fix freezing of the clusters view introduced in 0.13.2

## 0.13.2 - 13/06/22

**Features:**

* Enable random data generation for Avro (Custom + Schema Registry), JSON, Protobuf and MessagePack

**Bug fixes:**

* Fix white screen on consumer DSL view
* Fix issue when trying to run Test Suites

**Known issues:**

* Release introduced an issue with cluster connections / freezing the cluster screen, so was  swiftly rolled back to issue fix

**Other notes:**

*   Reduce the number of notifications on network error

    ****

## 0.13.1 - 08/06/22

**Features:**

* Updated variable values are now visible in the execution details
* Produced records data can now be viewed in the execution details
* Improved the Agent creation flow drastically and provide commands to download on run on your OS&#x20;
* Add a log on the Agent when a new version is available

**Bug fixes:**

* Fix some cluster configuration error handling, where the Submit button would do nothing
* Fixed some issues with the Generator
* Fixed some issues when switching to and from DSL view
* Fixed Executions becoming unlisted when the relative agent token is deleted

## 0.13.0 - 01/06/22

**Features:**

* Add an Onboarding module to help you get started !
* Replace menu icons with some easier to recognize
* Disable Cluster refresh if no agent is selected
* Improve notification messages UI
* Migrate Test Suite run details to a dedicated page

**Bug fixes:**

* Fix the sorting of events on the Home view
* Fix JSON registry serde not validating the data

## 0.12.1 - 26/05/22

**Features:**

* Add helper for Schema Registry strategy field
* Check/Uncheck all scenarios when running Test Suite or obtaining CI/CD configuration
* Point releases link to public changelog
* Make agents more discoverable

**Bug fixes:**

* Fix cluster is shown as reachable when agent is disconnected
* Fix issue with cluster configuration form when empty properties are provided

**Other notes:**

* Disabled ability to edit task name in the node itself due to usability issues

## 0.12.0 - 23/05/22

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

## 0.11.0 - 16/05/22

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

## 0.10.0 - Public Beta - 09/05/22

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



