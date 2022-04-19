+++
title = "Task 2 - Kamelet example"
weight = 8
+++

[This example](https://github.com/nexus-Six/camelk-integration-workshop/tree/master/02-kamelets-examples/chuck-norris-example) demonstrates how to create a simple Chuck Norris Kamelet source and how to integrate it with telegram. Our goal is to receive some funny jokes on our Telegram channel.

> If you still don't have your Telegram account, bot or chat ID, please refer to the first chapter "Intro" for the instructions on how to get them. 

#### Let's get started

&#9744; `oc new-project kamelet-example` - create a new project for the second example \
&#9744; Create a yaml file called [chuck-norris-source.kamelet.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/02-kamelets-examples/chuck-norris-example/chuck-norris-source.kamelet.yaml) 
> <span style="color:red">!!!!Add more information about creation of camelets here.!!!!!</span>

As Kamelets look like any other Camel component, experienced developers will enjoy using them as much, and will quickly browse through all the already available predefined Catalog Kamelets.
It is possible to create your own kamelets
You can define your own library of reusable kamelets for your organisation. And desirebly, contribute them to the Camel community.
Kamelets have two kinds of connectors, **sources** and **sinks**. Sources produce the data and sinks consume the data and optionally produce a response.

 Camel provides more than 300 components out of the box, therefore we can create a Kamelet in a simple way, making use of one of the components already available. Most of the Kamelets available in the official catalog, are simple ones having only a remapping of the Kamelet properties into Camel endpoint parameters.

&#9744; `oc apply -f chuck-norris-source.kamelet.yaml` - use the `kamel` to create the chuck norris source kamelet 
> You can use `kamel init xxxx-source.kamelet.yaml / xxxx-sink.kamelet.yaml` to instantiate a kamelet template for creating your own custom kamelet. 

&#9744; `oc get kamelets` - check if the chuck norris source is ready \
&#9744; create a [chuck-norris-example.groovy](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/02-kamelets-examples/chuck-norris-example/chuck-norris-example.groovy) \
&#9744; `kamel run chuck-norris-example.groovy --dev`- run the integration using chuck norris kamelet in the "dev mode" 
> You should see the jokes appearing in the terminal. 
> [All the supported languages for Camel K integration](https://camel.apache.org/camel-k/1.8.x/languages/languages.html)

&#9744; Change the `.to('log:info')` to `.to("telegram:bots?authorizationToken=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&chatID=XXXXXXXXXXXXX")`  - run the integration with telegram, provide the bot Token and chat ID 
> You should be receiving jokes from your Telegram bot now.

&#9744; `oc delete project chuck-norris` - clean up the project
