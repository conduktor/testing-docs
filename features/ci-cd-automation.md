# CI/CD Automation

Conduktor Testing supports automated execution of Test Scenarios via the CI Agent. This process enables you to run a [Test Suite](building-tests/test-suites.md) from within your build pipeline.

**Why automated testing in CI/CD?**

* Reduce manual efforts when tests need to be run repetitively
* Ensure builds are stable before they are released
* Helps compute test results and identify regressions

## Configuring the CI Agent

The pre-requisite for executing tests in your CI environment is configuring the CI Agent.&#x20;

> A single agent token can be used in multiple CI process in parallel. However for audit purposes, we recommend creating new agents when the scope or access changes.

This can be obtained from the **Agents** tab by selecting **Create an agent.**

![](<../.gitbook/assets/image (8).png>)

Select **CI Agent** and click **Create.**

### **Download the Token**

**Download** the newly generated token and store it somewhere secure.&#x20;

{% hint style="danger" %}
Careful, as **you will only be shown the token once!** So make sure you download it and store it somewhere secure
{% endhint %}

![](<../.gitbook/assets/image (34).png>)

### Example Github Action

Select the **Github Action** tab to see an example command for executing test scenarios in your CI/CD environment.

Note you can use this template,  but you will need to replace the **'CONFIG'** dependency.&#x20;

To obtain the config, see [obtaining the CI configuration](ci-cd-automation.md#obtaining-the-ci-configuration).&#x20;

![](<../.gitbook/assets/image (27) (1).png>)

## Obtaining the CI Configuration

To obtain the CI configuration for executing your tests in an automated manner, you must first have a [Test Suite ](building-tests/test-suites.md)created.

From within the test suite, select the **Integrate with CI/CD** button.

![](<../.gitbook/assets/image (162).png>)

Configure your options, such as which scenarios to include, and the [data storage](../miscellaneous/data-security.md) settings. Then, select **Generate CI configuration.**

![](<../.gitbook/assets/image (98).png>)

On the next screen, you will be displayed the **CI configuration.** This will be used when automating execution in your code pipeline.

**Copy** the JSON to the clipboard.

![](<../.gitbook/assets/image (8) (1).png>)

## Using the CI Configuration

Below shows an example Github action, utilising the CI agent to automate execution of tests.

Note the parameters:

* **Container image**: `ghcr.io/conduktor/testing-agent-ci:latest`
* **Token**: _Replace with your CI token_
* **CI Configuration:** The CI configuration obtained in the prior step

> If you copied the Base64 version of the configuration, you should use the _CONFIG\_BASE64_ environment variable instead.&#x20;

```yaml
name: Example github action

on:
  push:
    branches:
      - testing-runner-ci

jobs:
  tests:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/conduktor/testing-agent-ci:latest
    steps:
      - name: Run Testing Scenario
        env:
          TOKEN: <YOUR CI TOKEN>
          CONFIG: |
              {
                "scenarios": [
                  {
                    "id": "6C1MLj8jFqHAfzdvDFCW4rx"
                  },
                  {
                    "id": "b8SNLtyWdWmPfc6Mt33fYr"
                  },
                  {
                    "id": "7e7AQMPoLjqSfvZ9W9yoGF"
                  }
                ],
                "iterations": 1,
                "dataRedactionConfig": {
                  "redactRecordData": false,
                  "redactCheckData": false
                }
              }
        run: /opt/docker/bin/conduktor-testing
```
