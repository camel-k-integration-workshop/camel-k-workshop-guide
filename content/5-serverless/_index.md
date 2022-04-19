+++
title = "Task 3 - Serverless integration with Camel K"
weight = 10
+++


In [this example](https://github.com/nexus-Six/camelk-integration-workshop/tree/master/03-knative-example/telegram-example/printer-example), we will create a simple telegram source `Kamelet` and use `KameletBinding` to bind the source to a Knative channel. Then we will create a **Printer** that prints out the messages sent to the telegram source. 

In the previous example, we've talked about the concept of `Kamelet`. So what is a `KameletBinding`? A `KameletBinding` lets you tell a `Kamelet` source to send events to a destination that can be represented by a Knative channel or a Kafka topic, the same mechanism lets a `Kamelet` sink consume events from a destination. Therefore, you can use `KameletBindings` to define the high-level flows of an event-driven architecture, as you can see in the following picture, we will create all the components in the architecture together in this example. 

{{< figure src="../images/camelk_workshop03_arch.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}

First let's create a new project on the OpenShift cluster:

&#9744; `oc new-project userX-message-printer` - this command will create a new project for the message printer example, alternatively you can use OpenShift web console to create a new project.

&#9744; `oc get csv` - to make sure the Camel K and OpenShift Serverless operators are running in the namespace 

OpenShift Serverless provides Kubernetes native building blocks that enable us to create and deploy serverless, event-driven applications on OpenShift. It is based on the Knative project. But what is Knative? What is Serverless?

Serverless is a cloud-native development model that allows developers to build and run applications without having to manage servers. Serverless offerings are usually metered on-demand through an event-driven execution model. Serverless applications are deployed in containers that automatically launch on demand when needed.

Knative is an open source project that helps us deploy, run, manage serverless applications on Kubernetes or OpenShift. For serverless applications, Your code only runs when it needs to, with Knative starting and stopping instances automatically. How does it achieve this? Now we need to talk about the two important components of Knative: Serving and Eventing.

-  Serving - Enables rapid deployment of containers and automatic scaling of pods through a request-driven model for serving workloads based on demand.
- Eventing - An infrastructure for consuming and producing events to stimulate serverless apps. Apps can be triggered by a variety of sources, e.g. AMQ Streams, events from your own apps.

&#9744; Create both instances of Knative Serving and Eventing via OpenShift Serverless operator on the web console

&#9744;  `oc apply -f telegram-simple-source.kamelet.yaml` - create a [telegram-simple-source.kamelet.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-simple-source.kamelet.yaml) 
```
spec:
  definition:
    title: "Telegram Source"
    description: |-
      Receive all messages that people send to your Telegram bot.
      To create a bot, contact the @botfather account using the Telegram app.
      The source attaches the following headers to the messages:
      - `chat-id` / `ce-chat-id`: the ID of the chat where the message comes from
    required:
      - authorizationToken
    type: object
    properties:
      authorizationToken:
        title: Token
        description: The token to access your bot on Telegram. You you can obtain it from the Telegram @botfather.
        type: string
        format: password
        x-descriptors:
        - urn:alm:descriptor:com.tectonic.ui:password
```
This section is a simple definition of the Telegram source, it will retrieve all the messages sent to the Telegram bot. Importantly, we want to configure the source correctly by specifying the required property which is `authorizationToken`, which allows us to access the bot.

```
flow:
    from:
      uri: telegram:bots
      parameters:
        authorizationToken: "{{authorizationToken}}"
      steps:
        - convert-body-to:
            type: "java.lang.String"
            charset: "UTF8"
        - filter:
            simple: "${body} != null"
        - log: "${body}"
        - to: "kamelet:sink"
```
The `flow` section defines the integration flow. In this case, it goes from the Telegram bot, and will go through the steps defined in the `steps`, finally ends up in the `kamelet:sink`.


&#9744; `oc get kamelets` - check if the source kamelet is ready \
&#9744; `oc apply -f telegram-channel.yaml` - create a [Knative InMemory Channel](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-channel.yaml) on the cluster \
&#9744; `oc apply -f telegram-source-binding.yaml`  - create a [telegram-source-binding.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-source-binding.yaml) that binds the Knative channel to the telegram source
> Please replace the `<your-bot-token>` to your actual bot token!
```
source:
  ref:
    kind: Kamelet
    apiVersion: camel.apache.org/v1alpha1
    name: telegram-simple-source
  properties:
    authorizationToken: "<your-bot-token>"
```
This `source` section shows us how to refer the `Kamelet` source using the property `authorizationToken`, this makes sure that messages produced by the Telegram source are forwarded to the Knative InMemoryChannel named "telegram", which is referred in the `sink` section (see the following code block).
```
sink:
  ref:
    apiVersion: messaging.knative.dev/v1
    kind: InMemoryChannel
    name: telegram
```

&#9744; `oc get integrations` - check the status of the KameletBinding 


&#9744; kamel run [printer.groovy](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/printer.groovy) - create the integration that prints out the messages sent to the telegram bot 
```
from('knative:channel/telegram')
  .convertBodyTo(String.class)
  .to('log:info')
```
Here we create the simple event consumer that takes the messages from the Knative Channel and then print them out in the log. 

&#9744; Send some messages to your telegram bot \
&#9744; `kamel logs printer` - check the logs of the printer
> You can also go to the OpenShift web console and check the logs of Printer pod.
> knative Serving enables autoscaling of the applications and it is event driven, so if we don’t send any messages from now on, you should see the pod scale down to 0 automatically, maybe we need to wait for a bit.

&#9744; Stop sending messages to the telegram bot 
> Printer pod autoscales to zero 
> If you want to trigger the printer running again, you can simply send the message to the bot again, and after a few second, you should see the printer pod will start scaling up again.

&#9744; `oc delete project userX-message-printer` - clean up the namespace

Congrats!! We’ve achieved the final example! 