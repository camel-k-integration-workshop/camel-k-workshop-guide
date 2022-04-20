# Camel K Workshop

## What is it about
This workshop aims to help gain your first hands-on experience with Camel K and the important concepts such as Kamelets, KameletBindings and Knative.



## Architecture overview

#### The workshop consists of 3 separate exercises. 

1. In the first one, the goal is to create the simplest route file to create a "Hello World" message and log it to the terminal in the set time interval.

{{< figure src="../images/camelk_workshop01_arch.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}


2. The second exercise's goal is to create an integration using a Kamelet - new concept introduced in Camel K that allow users to connect to external systems via a simplified interface, hiding all the low level details about how those connections are implemented. To showcase the use of it, we will connect to the database of Chuck Norris jokes using just one command. Then we will send the joke to the terminal first, and then we will also send it as a Telegram message. In order to do that, Telegram account and Telegram bot will be required. 

{{< figure src="../images/camelk_workshop02_arch.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}


3. The third and last exercise will teach you about how to utilize Knative to create serverless applications that scale depending on the workload. This time we'll be sending messages to the Telegram bot and watch it's behavior, i.e. how it scales up and down depending on the frequency of receiving new messages.

{{< figure src="../images/camelk_workshop03_arch.png?width=50pc&classes=border,shadow" title="Click image to enlarge" >}}


## Collaboration
This workshop was created by Rui Zhang, Tala Ismail, Fabian Popp and Adrian Luberda.  
Feel free to create a pull request or an issue in [GitHub](https://github.com/camel-k-integration-workshop/camel-k-workshop).