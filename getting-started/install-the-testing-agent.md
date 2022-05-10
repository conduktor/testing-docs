# Install the Testing Agent

The Testing Agent is a micro-application that runs on your desktop, private network or CI environment. It ensures you can reach clusters that your host has access to securely and with isolation.

First, **register** the Testing Agent in your Workspace.

Then, **install** the Testing Agent to run [Test Scenarios](../features/building-tests/test-scenarios.md). ****&#x20;

{% hint style="success" %}
Testing Agent can be installed and used on GNU/Linux, macOS, FreeBSD, and Windows. You can install it:

* In a container.
* By downloading a binary manually.
{% endhint %}

## Agent Registration&#x20;

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

{% hint style="danger" %}
You will only be shown the token **once**, so ensure you store it somewhere securely.&#x20;
{% endhint %}

![](<../.gitbook/assets/image (73).png>)

**Copy** the token, as we will use it in the next step.

{% hint style="success" %}
A token can be used by **multiple** agents, allowing it to scale horizontally. \
However when running agents in different locations, with different access or different resources, you should create separate tokens.
{% endhint %}

## Agent Installation&#x20;

### Binary installation

**Java 8+** is required for running the Testing Agent.&#x20;

If you do not meet these requirements, please [download](https://www.oracle.com/java/technologies/downloads/) a more recent version.

Download the **latest version** of the Conduktor Testing Agent:

[https://github.com/conduktor/testing/releases/](https://github.com/conduktor/testing/releases/)

**Run** the below command via command line, populating the token parameter with your newly generated token.

```
java -jar conduktor-testing-agent-*.jar --token=<TOKEN>
```

### Container installation

{% hint style="info" %}
Using Docker introduces complexity when trying to reach clusters on localhost or reference certificates on your local file system. \
For these use cases, we recommend using the [binary distribution](install-the-testing-agent.md#binary-installation).
{% endhint %}

**Container image**: `ghcr.io/conduktor/testing-agent:latest`\
\
You will need to provide the agent token as well, through the **AGENT\_TOKEN** environment variable

**Run** with Docker:

```
docker run -e AGENT_TOKEN=<TOKEN> -d ghcr.io/conduktor/testing-agent:latest
```

**Run** with Docker Compose:

```
# docker-compose.yaml
services:
  testing-agent:
    image: ghcr.io/conduktor/testing-agent:latest
    environment:
      AGENT_TOKEN: <TOKEN>
```



### Running in the CI

The Testing Agent is a long-running process, and should not be used in a CI pipeline.

For CI workflows, please read [our dedicated documentation](../features/ci-cd-automation.md).

## Validate the Testing Agent

You should see `Started Agent` in the logs.&#x20;

{% hint style="info" %}
If you observe an error regarding the Java Runtime (class file version 55.0), please [download](https://www.oracle.com/java/technologies/downloads/) a more recent version of Java. The Agent supports **Java 8+**.
{% endhint %}

Navigate back **** to the Testing application and **refresh** the connection indicator. If installation was successful, you will see the green `CONNECTED` indicator next to your Agent.

![](<../.gitbook/assets/image (69).png>)

Now you have the Testing Agent installed, you will be able to reach clusters that your host has access to within the Testing application. Continue to [connecting a Kafka cluster](connect-to-a-kafka-cluster.md).
