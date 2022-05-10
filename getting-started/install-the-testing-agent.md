# Install the Testing Agent

The Testing Agent is a micro-application that runs on your desktop, private network or CI environment. It ensures you can reach clusters that your host has access to securely and with isolation.

**You must install** the Testing Agent to run [Test Scenarios](../features/building-tests/test-scenarios.md). **** Setup takes only a minute using a single command.

The general **** flow **** for utilization of the Agent is:

* User downloads the Testing Agent
* User registers an Agent inside the Testing application and obtains a token
* User runs a command on their host to start the Agent
* The Agent is now installed
* The Testing application can now reach clusters that your host has access to

## Download the Testing Agent

Download the **latest version** of the Conduktor Testing Agent:

### [https://github.com/conduktor/testing/releases/](https://github.com/conduktor/testing/releases/)

### Java Requirements

**Java 8+** is required for running the Testing Agent.&#x20;

If you do not meet these requirements, please [download](https://www.oracle.com/java/technologies/downloads/) a more recent version.\


### Using Docker

We also provide a docker image of the agent. For local agents we suggest using the jar release, as reaching local clusters and using local certificate stores on docker will require some configuration.\
\
**Container image**: `ghcr.io/conduktor/testing-agent:latest`

The versions correspond to those listed in [https://github.com/conduktor/testing/releases/](https://github.com/conduktor/testing/releases/) \
\
You will need to provide the agent token as well, through the **AGENT\_TOKEN** environment variable

`docker run -e AGENT_TOKEN=YourToken -d ghcr.io/conduktor/testing-agent:latest`



### Running in the CI

The Testing Agent is long-running, and should not be used in a CI.

For CI workflows, please read [our dedicated documentation](../features/ci-cd-automation.md).



## Register an Agent&#x20;

From within the Conduktor Testing UI, navigate to the **Tokens** tab. Note you may need to create a [Workspace](../features/workspace.md) first.

![](<../.gitbook/assets/image (137).png>)

Select **Create a token** to begin the registration process.

Provide a **Name** to identify your agent, and confirm if it will be personal, organisational, or used in your CI environment.

* **Personal Agent:** Only you will have access to this. For example, running locally on your own machine or server.
* **Organisation Agent**: Your colleagues or team-mates will also have access to this. For example, running inside a company server or network.
* **CI Agent:** You will use this token for executing tests in CI/CD jobs.
  * __[_Learn more_](../features/ci-cd-automation.md) _about using the CI Agent_

![](<../.gitbook/assets/image (31).png>)

Select **Create token** to generate your token on the next screen.&#x20;

{% hint style="info" %}
You will only be shown the token **once**, so ensure you store it somewhere securely.&#x20;
{% endhint %}

![](<../.gitbook/assets/image (73).png>)

**Copy** the token, as we will use it in the final step.\
\
A single token can be used by multiple agents, allowing it to scale horizontally. \
However when running agents in different locations, with different access or different resources, you should create separate tokens.

## Start the Testing Agent

**Run** the below command via command line. populating the token parameter with your newly generated token.

```
java -jar conduktor-testing-agent-0.10.0.jar --token=<token>
```

You should see `Started Agent` in the logs.&#x20;

{% hint style="info" %}
If you observe an error regarding the Java Runtime (class file version 55.0), please [download](https://www.oracle.com/java/technologies/downloads/) a more recent version of Java. The Agent supports **Java 8+**.
{% endhint %}

Navigate back **** to the Testing application and **refresh** the connection indicator. If installation was successful, you will see the green `CONNECTED` indicator next to your Agent.

![](<../.gitbook/assets/image (69).png>)

Now you have the Testing Agent installed, you will be able to reach clusters that your host has access to within the Testing application. Continue to [connecting a Kafka cluster](connect-to-a-kafka-cluster.md).
