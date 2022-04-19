+++
title = "Task 3 - serverless"
weight = 10
+++

In [this example](https://github.com/nexus-Six/camelk-integration-workshop/tree/master/03-knative-example/telegram-example/printer-example), we will create a simple telegram source `Kamelet` and use `KameletBinding` to bind the source to a Knative channel. Then we will create a **Printer** that prints out the messages sent to the telegram source. 

&#9744; `oc new-project userX-message-printer` - create a new project for the message printer example
&#9744; `oc get csv` - make sure the Camel K and Serverless is running in your namespace 
> We will elaborate more on the Serverless and Knative during the workshop. 

&#9744; create a [telegram-simple-source.kamelet.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-simple-source.kamelet.yaml) \
&#9744; `oc apply -f telegram-simple-source.kamelet.yaml` - create the telegram source kamelet
> More explanation for the kamelet file will be present in the workshop.

&#9744; `oc get kamelets` - check if the source kamelet is ready \
&#9744; Create a [telegram-channel.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-channel.yaml) on the cluster \
&#9744; `oc apply -f telegram-channel.yaml` - create a Knative InMemory Channel \
&#9744; create a [telegram-source-binding.yaml](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/telegram-source-binding.yaml) that binds the Knative channel to the telegram source \
&#9744; `oc apply -f telegram-source-binding.yaml` - create the binding between the Knative channel and the telegram source \
&#9744; `oc get integrations` - check the status of the kamelet binding \
&#9744; kamel run [printer.groovy](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/03-knative-example/telegram-example/printer-example/printer.groovy) - create the integration that prints out the messages sent to the telegram bot 
> We will explain it in details during the workshop.
> You should see the printer running in one pod first

&#9744; Send some messages to your telegram bot \
&#9744; `kamel logs printer` - check the logs of the printer
> You can also go to the OpenShift web console and check the logs of Printer pod.

&#9744; Stop sending messages to the telegram bot \
&#9744; Printer pod autoscales to zero \
&#9744; `oc delete project userX-message-printer` - clean up the namespace
