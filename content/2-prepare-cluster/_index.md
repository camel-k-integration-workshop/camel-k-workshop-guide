+++
title = "Prepare your cluster"
weight = 5
+++

## Cluster Preparation

Before you start you have to install a number of operators you'll use during the workshop. These two are `Red Hat Integration - Camel K` for providing Camel services in your cluster and `Red Hat OpenShift Serverless` to make our application truly serverless and scalable. But fear not, both are managed by Kubernetes [operators](https://cloud.redhat.com/learn/topics/operators) on OpenShift.

### Install and prepare Camel K Operator

- In the Web Console, go to **Operators > OperatorHub** and search for `Red Hat Integration - Camel K` (You may need to disable search filters)
- Install the `Red Hat Integration - Camel K Operator` with default settings
- Go to **Installed Operators > Red Hat Integration - Camel K Operator** and click on the **Create Instance** tile in the `camel-k-workshop` project  <span style="color:red">!!!!check if this step is needed!!!!!</span>.  
- Done!

### Install and prepare OpenShift Serverless operator

- In the Web Console, go to **Operators > OperatorHub** and search for `Red Hat OpenShift Serverless` (You may need to disable search filters)
- Install the `Red Hat OpenShift Serverless Operator` with default settings
- Go to **Installed Operators > Red Hat Integration - Camel K Operator** and click on the **Create Instance** tile in the `camel-k-workshop` project  <span style="color:red">!!!!check if this step is needed!!!!!</span>.  
- Done!

### Login to OpenShift from your local machine 

- If you don't already have the oc client installed, you can download the matching version for your operating system [here](https://docs.openshift.com/container-platform/4.8/cli_reference/openshift_cli/getting-started-cli.html)
- Log into your OpenShift Webconsole with you cluster admin credentials 
- In the top right corner, click on your username and then **Copy login command** to copy your login token
- On you local machine either: 
  * open a terminal and log in with the `oc` command you copied **OR**
  * use the integrated terminal in VSCode to log in with the `oc` command you copied  

Your cluster is now prepared for the next step, proceed to the **Task 1 - Hello World**.