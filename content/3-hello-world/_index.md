+++
title = "Task 1 - Hello World"
weight = 7
+++

[This example](https://github.com/nexus-Six/camelk-integration-workshop/tree/master/01-helloworld-example) demonstrates a simple Camel K integration that periodically prints a "Hello World from Camel K". Let's recap the simple architecture of this example:

{{< figure src="../images/camelk_workshop01_arch.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}

### Let's begin!

&#9744; Make sure you have the terminal in VSCode opened and you are logged to OpenShift \
&#9744; `oc new-project helloworld` - create a new project with the name 'helloworld' \
&#9744; `oc get csv` - you should see the Camel K operator running \
&#9744; Create a [helloworld.groovy](https://github.com/nexus-Six/camelk-integration-workshop/blob/master/01-helloworld-example/helloworld.groovy) file 

> We will elaborate on the integration file during the workshop 

&#9744; `kamel run helloworld.groovy` - run the integration using `kamel`
> It might take up to 3 minutes for the integration to run. 

&#9744; `oc get integrations` - check if the integration is running \
&#9744; `kamel logs helloworld` - get the logs of the running integration
> You will see the hello world message printing out in the terminal every 3 seconds
> If you run `kamel run helloworld.groovy --logs` in the beginning, you will see the logs showing in the terminal as well

&#9744; `kamel run helloworld.groovy --dev` - alternatively, run the integration in the `dev mode` \
&#9744; change the `from('timer:tick?period=3000')` to `from('timer:tick?period=5000')` in the `helloworld.groovy` file 
> The running integration will reload, a few seconds later you will see the hello world message printing out in the terminal every 5 seconds 

&#9744; `oc delete project helloworld` - clean up the namespace