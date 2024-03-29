
# Appdynamics Kubernetes Extension Helm Charts
## Begin by creating the Docker image as detailed in [documentation](https://github.com/AppdAgents/kubernetes-snapshot-extension-1/blob/master/README.md) or you may opt to download the necessary tar file directly from [Here](https://appdagents.github.io/k8s-extension-charts/k8s-ext-docker-1.0.tar) 
### Add K8S Extension Charts helm repo
```bash
helm repo add k8s-extension-charts https://appdagents.github.io/k8s-extension-charts
```
### Create values yaml to override default ones
```yaml
# AppDynamics controller info (VALUES TO BE PROVIDED BY THE USER)
controllerInfo:
  #<controller dns>
  host:
  #<controller port> e.g. "8090"
  port:
  #<account name>
  accountName:
  #<global account name>  obtained from  Settings --> License --> Global Account Name
  globalAccount:
  sslEnabled:  #"true" if https, otherwise "false"
  restApiUrl: #<protocol://controller dns>:<port>/controller/ e.g. https://myappd.com:8090/controller/
  controllerAPIUser:
  controllerURL:
  # controller secret key obtained from --> Settings --> License --> Access key
  accessKey:
  #<event service endpoint in format protocol://host:port>
  eventsApiURL:
  # Events API Key obtained from AppDynamics --> Analytics --> Configuration API Keys --> Add
  # The API Key you create needs to be able to Manage and Publish Custom Analytics Events
  eventsApiKey:

extensionConfig:
  # APPLICATION_NAME env var
  appName:
  appTierName:
  imageUrl: 
  imagePullPolicy: IfNotPresent
  #server or cluster #K8S_API_MODE env var
  apiMode: "cluster"
  metricLimt: "4000"
  uniqueHostId: "K8s-Monitor"
  labels:
    app: k8s-monitor
  imagePullSecrets: null
  # Path to your kubectl Client configuration
  kubeClientConfig: "~/.kube/config"
  #Add comma seperated tags/lables which needs to captured these will captured from resource metadata
  customTags: hall
  nodes:  # list of nodes to collect metrics for. If all nodes need to be monitored, set name to "all"
    - name: "all"
  # list of namespaces to collect metrics for. If all namespaces need to be monitored, set name to "all"
  namespaces:
    - name: "all"
  dashboardNameSuffix: "SUMMARY"
```
### Install k8s-extension using helm chart
```bash
helm install "<my-k8-extension-helm-release-name>"> k8s-extension-charts/k8s-extension -f <values-file>.yaml --namespace <namespace>
```
### Note:
For more details and config options please visit official [documentation](https://github.com/AppdAgents/kubernetes-snapshot-extension-1/blob/master/README.md)
