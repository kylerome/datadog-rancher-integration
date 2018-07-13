# Datadog on Rancher 2.0

[Datadog](https://www.datadoghq.com/) is a popular hosted monitoring solution for aggregating and analyzing metrics and events for distributed systems.  From infrastructure integrations to collaborative dashboards, Datadog gives you a clean single pane view into the information that is most important to you.  To make Datadog easy to use with Rancher 2.0, we have modified the Datadog [Helm](https://helm.sh/) chart to make it a simple deployment through Rancher's catalog feature that will function across Rancher projects within a cluster.

## Prerequisites
1. Datadog API Key (you can use an existing secret with your API key, or let the chart make one for you)
1. By default Rancher Kubernetes Engine (RKE) does not allow unauthenticated access to the kubelet API which Datadog relies on for many of its metrics.  When installing the cluster with RKE we need to provide extra arguments to the kubelet service.
   ```yaml
    services:
      kubelet:
        extra_args:
          read-only-port: 10255
   ```
   __NOTE:__ You should make sure this port is properly firewalled
1. A Kubernetes 1.8+ cluster attached to a Rancher installation
## Setup & Configuration
1. The [Datadog Rancher Chart](https://github.com/rancher/charts/tree/master/charts/datadog/v1.0.0) is available by default in the Rancher library, there is also a Datadog chart in Helm stable but we suggest using the Rancher library chart for ease of use.  The Rancher library is enabled by default, if disabled this setting can be modified under Global->Catalogs.

![Catalog](https://github.com/kylerome/datadog-rancher-integration/blob/master/docs/images/Chart.png)

2. The charts configuration options have been made available through the UI in Rancher by adding a [questions.yaml](https://github.com/rancher/charts/blob/master/charts/datadog/v1.0.0/questions.yml) file, to learn more about them please refer to the [values.yaml](https://github.com/rancher/charts/blob/master/charts/datadog/v1.0.0/values.yaml) file which has additional information and links describing the variables.

![Catalog](https://github.com/kylerome/datadog-rancher-integration/blob/master/docs/images/AgentConfiguration.png)

## Dashboards

If you plan to send mutliple clusters of data to the same datadog endpoint, it's useful to add the cluster name as a host tag (e.g. `kube-cluster-name:CLUSTERNAME`) when configuring the Helm chart.  This will allow you to sort data by scope to a specific cluster, as well as group data by cluster within a dashboard.  In the below dashboard we have grouped node data by cluster in a few of the default widgets for the clusters 'dash-1' and dash-2'.

![Dashboard](https://github.com/kylerome/datadog-rancher-integration/blob/master/docs/images/datadogDashboard.PNG)
