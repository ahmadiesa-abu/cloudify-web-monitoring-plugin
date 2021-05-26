# Azure AKS Monitor Example

## Prerequisites:

  * Cloudify Manager with Latest Azure and Cloudify-web-monitoring Plugins.


### Description:

Check will measure HTTP server response time and will trigger a scale up workflow if that response time is above a threshold. The workflow will scale the cluster in AKS adding a worker to it.
After the cooldown timer has passed and the low threshold is reached Cloudify will trigger a scale down workflow for AKS cluster.


### Creating secrets

Replace <value> with actual values, without the <>

```shell
cfy secrets create azure_subscription_id --secret-string <value>
cfy secrets create azure_tenant_id --secret-string <value>
cfy secrets create azure_client_id --secret-string <value>
cfy secrets create azure_client_secret --secret-string <value>
```

### Running the example

To install the AKS cluster that we will be monitoring :

```shell
cfy install blueprint.yaml -b Cluster
```

then you can add a deployment on that cluster that installs a service to measure the response time for

through Azure Portal - Kubernetes service - Services and ingresses - you can add `kube-hello-change.yaml` that will install a flask application that you can change the response time for URL

To install the monitoring deployment that will be triggered every 1 minute and check the response time for the URL :

```shell
cfy install monitor.yaml -b Monitor -i node_agent_pool_deployment_name='Cluster' -i scalable_entity_name='node_agent_pool' \
-i url='<the url of the installed deployment of flask application>'
```

To trigger scale up you can change the response time from the URL by '<URL>/change/2' , that will make the response time higher than the threshold 
