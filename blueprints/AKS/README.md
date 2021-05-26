# Azure AKS Monitor Example

## Prerequisites:

  * Cloudify Manager with Latest Azure and Cloudify-web-monitoring Plugins.

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

through Azure Portal you can deploy `kube-hello-change.yaml` that will install a flask application that you can change the response time for URL


```shell
cfy install agent_pool.yaml -b ClusterAgentPool -i managed_cluster_name='testmonitoraks' -i agent_pool_name='agentpool'
```


```shell
cfy install monitor.yaml -b Monitor -i node_agent_pool_deployment_name='ClusterAgentPool' -i scalable_entity_name='node_agent_pool' \
-i url='<the url of the installed deployment of flask application>'
```
